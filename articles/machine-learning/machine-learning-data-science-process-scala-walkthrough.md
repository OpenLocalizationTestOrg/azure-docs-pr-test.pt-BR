---
title: "Ciência de dados usando o Scala e Spark no Azure | Microsoft Docs"
description: "Como usar o Scala para tarefas de aprendizado de máquina supervisionadas com a MLlib escalonável do Spark e os pacotes de AM do Spark em um cluster Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: b2419f53bdc3236d7de76b89f2a0a76704e85391
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="bba8b-103">Ciência de Dados usando o Scala e o Spark no Azure</span><span class="sxs-lookup"><span data-stu-id="bba8b-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="bba8b-104">Este artigo mostra como usar o Scala para tarefas de aprendizado de máquina supervisionadas com a MLlib escalonável do Spark e os pacotes de AM do Spark em um cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-104">This article shows you how to use Scala for supervised machine learning tasks with the Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="bba8b-105">Ele explica as tarefas que constituem o [Processo Ciência de Dados](http://aka.ms/datascienceprocess): ingestão e exploração de dados, visualização, engenharia de recursos, modelagem e consumo de modelo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-105">It walks you through the tasks that constitute the [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="bba8b-106">Os modelos no artigo incluem regressão logística e linear, florestas aleatórias e GBTs (árvores com aumento de gradiente), além de duas tarefas comuns de aprendizado de máquina supervisionadas:</span><span class="sxs-lookup"><span data-stu-id="bba8b-106">The models in the article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition to two common supervised machine learning tasks:</span></span>

* <span data-ttu-id="bba8b-107">Problema de regressão: previsão do valor da gorjeta (US$) para uma corrida de táxi</span><span class="sxs-lookup"><span data-stu-id="bba8b-107">Regression problem: Prediction of the tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="bba8b-108">Classificação binária: previsão da gorjeta ou não (1/0) para uma corrida de táxi</span><span class="sxs-lookup"><span data-stu-id="bba8b-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="bba8b-109">O processo de modelagem requer treinamento e avaliação em um conjunto de dados de teste e métricas de precisão relevantes.</span><span class="sxs-lookup"><span data-stu-id="bba8b-109">The modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="bba8b-110">Neste artigo, você pode aprender a armazenar esses modelos no armazenamento de Blobs do Azure e a pontuar e avaliar seu desempenho preditivo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-110">In this article, you can learn how to store these models in Azure Blob storage and how to score and evaluate their predictive performance.</span></span> <span data-ttu-id="bba8b-111">Este artigo também aborda os tópicos mais avançados de como otimizar modelos usando a validação cruzada e limpeza de hiperparâmetro.</span><span class="sxs-lookup"><span data-stu-id="bba8b-111">This article also covers the more advanced topics of how to optimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="bba8b-112">Os dados usados são uma amostra do conjunto de dados de corridas e tarifas de táxi em Nova York de 2013, disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="bba8b-112">The data used is a sample of the 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="bba8b-113">[Scala](http://www.scala-lang.org/), uma linguagem baseada na máquina virtual Java, integra conceitos de linguagem funcional e orientada a objetos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-113">[Scala](http://www.scala-lang.org/), a language based on the Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="bba8b-114">Trata-se de uma linguagem escalonável que é bastante adequada ao processamento distribuído na nuvem e executada em clusters Azure Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-114">It's a scalable language that is well suited to distributed processing in the cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="bba8b-115">[Spark](http://spark.apache.org/) é uma estrutura de processamento paralelo de software livre que dá suporte ao processamento na memória para melhorar o desempenho de aplicativos analíticos de Big Data.</span><span class="sxs-lookup"><span data-stu-id="bba8b-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing to boost the performance of big data analytics applications.</span></span> <span data-ttu-id="bba8b-116">O mecanismo de processamento do Spark foi desenvolvido para velocidade, facilidade de uso e análise sofisticada.</span><span class="sxs-lookup"><span data-stu-id="bba8b-116">The Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="bba8b-117">As funcionalidades de computação distribuídas na memória do Spark fazem dele uma boa escolha para algoritmos iterativos em cálculos de gráfico e aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="bba8b-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="bba8b-118">O pacote [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) fornece um conjunto uniforme de APIs de alto nível criadas com base em quadros de dados, que podem ajudar você a criar e ajustar pipelines práticos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="bba8b-118">The [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="bba8b-119">[MLlib](http://spark.apache.org/mllib/) é a biblioteca de aprendizado de máquina escalonável do Spark, que oferece recursos de modelagem para esse ambiente distribuído.</span><span class="sxs-lookup"><span data-stu-id="bba8b-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities to this distributed environment.</span></span>

<span data-ttu-id="bba8b-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) é a oferta do Spark de software livre hospedada no Azure.</span><span class="sxs-lookup"><span data-stu-id="bba8b-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is the Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="bba8b-121">Ele também inclui suporte para notebooks Scala do Jupyter no cluster Spark, e pode executar consultas interativas do Spark SQL para transformar, filtrar e visualizar dados armazenados no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="bba8b-121">It also includes support for Jupyter Scala notebooks on the Spark cluster, and can run Spark SQL interactive queries to transform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="bba8b-122">Os trechos de código Scala neste artigo que fornecem as soluções e mostram as plotagens relevantes para visualizar os dados executados em notebooks Jupyter instalados nos clusters Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-122">The Scala code snippets in this article that provide the solutions and show the relevant plots to visualize the data run in Jupyter notebooks installed on the Spark clusters.</span></span> <span data-ttu-id="bba8b-123">As etapas de modelagem nestes tópicos contêm código que mostra como treinar, avaliar, salvar e consumir cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-123">The modeling steps in these topics have code that shows you how to train, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="bba8b-124">As etapas de configuração e o código neste artigo são para o Azure HDInsight 3.4 Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="bba8b-124">The setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="bba8b-125">No entanto, os códigos neste artigo e no [Notebook Jupyter para Scala](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) são genéricos e devem funcionar em qualquer cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-125">However, the code in this article and in the [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="bba8b-126">As etapas de configuração e gerenciamento do cluster poderão ser ligeiramente diferentes do que é mostrado neste artigo se você não estiver usando o HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-126">The cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="bba8b-127">Para ver um tópico que mostre como usar o Python, em vez do Scala, para concluir as tarefas em um processo completo de Ciência de dados, confira [Visão geral da Ciência de dados usando Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bba8b-127">For a topic that shows you how to use Python rather than Scala to complete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="bba8b-128">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bba8b-128">Prerequisites</span></span>
* <span data-ttu-id="bba8b-129">Você precisa ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="bba8b-129">You must have an Azure subscription.</span></span> <span data-ttu-id="bba8b-130">Se ainda não tiver uma, [obtenha uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="bba8b-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="bba8b-131">Você precisa de um cluster Azure HDInsight 3.4 Spark 1.6 para concluir os procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="bba8b-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster to complete the following procedures.</span></span> <span data-ttu-id="bba8b-132">Para criar um cluster, veja as instruções em [Introdução: criar um Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="bba8b-132">To create a cluster, see the instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="bba8b-133">Defina o tipo de cluster e a versão no menu **Selecionar Tipo de Cluster** .</span><span class="sxs-lookup"><span data-stu-id="bba8b-133">Set the cluster type and version on the **Select Cluster Type** menu.</span></span>

![Configuração de tipo de cluster do HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="bba8b-135">Para obter uma descrição dos dados da corrida de táxi na cidade de Nova York e obter instruções sobre como executar código em um notebook Jupyter no cluster Spark, confira as seções relevantes de [Visão geral da Ciência de dados usando Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bba8b-135">For a description of the NYC taxi trip data and instructions on how to execute code from a Jupyter notebook on the Spark cluster, see the relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-the-spark-cluster"></a><span data-ttu-id="bba8b-136">Executar código em um notebook Jupyter no cluster Spark</span><span class="sxs-lookup"><span data-stu-id="bba8b-136">Execute Scala code from a Jupyter notebook on the Spark cluster</span></span>
<span data-ttu-id="bba8b-137">É possível iniciar o notebook Jupyter no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bba8b-137">You can launch a Jupyter notebook from the Azure portal.</span></span> <span data-ttu-id="bba8b-138">Encontre o cluster Spark no painel e clique nele para entrar na página de gerenciamento de seu cluster.</span><span class="sxs-lookup"><span data-stu-id="bba8b-138">Find the Spark cluster on your dashboard, and then click it to enter the management page for your cluster.</span></span> <span data-ttu-id="bba8b-139">Em seguida, clique em **Painéis do Cluster** e clique em **Notebook Jupyter** para abrir o notebook associado ao cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** to open the notebook associated with the Spark cluster.</span></span>

![Painel do cluster e notebooks Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="bba8b-141">Você também pode acessar blocos de anotações do Jupyter em https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="bba8b-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="bba8b-142">Substitua *clustername* pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="bba8b-142">Replace *clustername* with the name of your cluster.</span></span> <span data-ttu-id="bba8b-143">Você precisa da senha de sua conta de administrador para acessar os notebooks Jupyter.</span><span class="sxs-lookup"><span data-stu-id="bba8b-143">You need the password for your administrator account to access the Jupyter notebooks.</span></span>

![Acesse os notebooks Jupyter usando o nome do cluster](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="bba8b-145">Selecione **Scala** para ver um diretório com alguns exemplos de notebooks predefinidos que usam a API PySpark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-145">Select **Scala** to see a directory that has a few examples of prepackaged notebooks that use the PySpark API.</span></span> <span data-ttu-id="bba8b-146">O notebook Exploration Modeling and Scoring using Scala.ipynb, que contém os exemplos de código para este conjunto de tópicos Spark, está disponível no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="bba8b-146">The Exploration Modeling and Scoring using Scala.ipynb notebook that contains the code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="bba8b-147">Você pode carregar o notebook diretamente do GitHub para o servidor do Notebook Jupyter em seu cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-147">You can upload the notebook directly from GitHub to the Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="bba8b-148">Na home page do Jupyter, clique no botão **Carregar** .</span><span class="sxs-lookup"><span data-stu-id="bba8b-148">On your Jupyter home page, click the **Upload** button.</span></span> <span data-ttu-id="bba8b-149">No gerenciador de arquivos, cole a URL do GitHub (conteúdo bruto) do notebook Scala e clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="bba8b-149">In the file explorer, paste the GitHub (raw content) URL of the Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="bba8b-150">O notebook Scala está disponível na seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="bba8b-150">The Scala notebook is available at the following URL:</span></span>

[<span data-ttu-id="bba8b-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="bba8b-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="bba8b-152">Configuração: contextos predefinidos de Spark e Hive, palavras mágicas Spark e bibliotecas Spark</span><span class="sxs-lookup"><span data-stu-id="bba8b-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="bba8b-153">Contextos predefinidos de Spark e Hive</span><span class="sxs-lookup"><span data-stu-id="bba8b-153">Preset Spark and Hive contexts</span></span>
    # SET THE START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="bba8b-154">Os kernels Spark fornecidos com os notebooks Jupyter têm contextos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-154">The Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="bba8b-155">Não é necessário definir explicitamente os contextos Spark ou Hive antes de começar a trabalhar com o aplicativo que você está desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-155">You don't need to explicitly set the Spark or Hive contexts before you start working with the application you are developing.</span></span> <span data-ttu-id="bba8b-156">Os contextos de predefinição são:</span><span class="sxs-lookup"><span data-stu-id="bba8b-156">The preset contexts are:</span></span>

* <span data-ttu-id="bba8b-157">`sc` para SparkContext</span><span class="sxs-lookup"><span data-stu-id="bba8b-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="bba8b-158">`sqlContext` para HiveContext</span><span class="sxs-lookup"><span data-stu-id="bba8b-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="bba8b-159">Palavras mágicas do Spark</span><span class="sxs-lookup"><span data-stu-id="bba8b-159">Spark magics</span></span>
<span data-ttu-id="bba8b-160">O kernel do Spark fornece algumas "palavras mágicas" predefinidas, que são comandos especiais que você pode chamar com `%%`.</span><span class="sxs-lookup"><span data-stu-id="bba8b-160">The Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="bba8b-161">Dois desses comandos são usados nos exemplos de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="bba8b-161">Two of these commands are used in the following code samples.</span></span>

* <span data-ttu-id="bba8b-162">`%%local` especifica que o código nas linhas posteriores será executado localmente.</span><span class="sxs-lookup"><span data-stu-id="bba8b-162">`%%local` specifies that the code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="bba8b-163">Deve ser um código Scala válido.</span><span class="sxs-lookup"><span data-stu-id="bba8b-163">The code must be valid Scala code.</span></span>
* <span data-ttu-id="bba8b-164">`%%sql -o <variable name>` executa uma consulta do Hive no `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="bba8b-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="bba8b-165">Se o parâmetro `-o` for transmitido, o resultado da consulta será persistido no contexto `%%local` do Scala como um quadro de dados do Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-165">If the `-o` parameter is passed, the result of the query is persisted in the `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="bba8b-166">Para saber mais sobre os kernels para notebooks Jupyter e as "palavras mágicas" predefinidas chamadas com `%%` (por exemplo, `%%local`) confira [Kernels disponíveis para notebooks Jupyter com clusters do Apache Spark no HDInsight Linux](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="bba8b-166">For more information about the kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="bba8b-167">Importar bibliotecas</span><span class="sxs-lookup"><span data-stu-id="bba8b-167">Import libraries</span></span>
<span data-ttu-id="bba8b-168">Importe o Spark, a MLlib e outras bibliotecas necessárias usando o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="bba8b-168">Import the Spark, MLlib, and other libraries you'll need by using the following code.</span></span>

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a><span data-ttu-id="bba8b-169">Ingestão de dados</span><span class="sxs-lookup"><span data-stu-id="bba8b-169">Data ingestion</span></span>
<span data-ttu-id="bba8b-170">A primeira etapa no processo de Ciência de dados é ingerir os dados que você deseja analisar.</span><span class="sxs-lookup"><span data-stu-id="bba8b-170">The first step in the Data Science process is to ingest the data that you want to analyze.</span></span> <span data-ttu-id="bba8b-171">Traga os dados de fontes ou sistemas externos onde eles residem para seu ambiente de modelagem e a exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="bba8b-171">You bring the data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="bba8b-172">Neste artigo, os dados ingeridos são uma junção de 0,1% do exemplo arquivo sobre gorjeta e tarifa de táxi (armazenado como um arquivo .tsv).</span><span class="sxs-lookup"><span data-stu-id="bba8b-172">In this article, the data you ingest is a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="bba8b-173">O ambiente de exploração e modelagem de dados é Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-173">The data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="bba8b-174">Esta seção contém o código para concluir a seguinte série de tarefas:</span><span class="sxs-lookup"><span data-stu-id="bba8b-174">This section contains the code to complete the following series of tasks:</span></span>

1. <span data-ttu-id="bba8b-175">Definir os caminhos de diretório para o armazenamento de dados e de modelos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="bba8b-176">Ler o conjunto de dados (armazenado como um arquivo .tsv).</span><span class="sxs-lookup"><span data-stu-id="bba8b-176">Read in the input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="bba8b-177">Definir um esquema para os dados e limpar os dados.</span><span class="sxs-lookup"><span data-stu-id="bba8b-177">Define a schema for the data and clean the data.</span></span>
4. <span data-ttu-id="bba8b-178">Criar um quadro de dados limpo e armazená-lo em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="bba8b-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="bba8b-179">Registrar os dados como uma tabela temporária no SQLContext.</span><span class="sxs-lookup"><span data-stu-id="bba8b-179">Register the data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="bba8b-180">Consultar a tabela e importar os resultados em um quadro de dados.</span><span class="sxs-lookup"><span data-stu-id="bba8b-180">Query the table and import the results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="bba8b-181">Definir caminhos de diretório para locais de armazenamento no armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="bba8b-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="bba8b-182">O Spark pode ler e gravar no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="bba8b-182">Spark can read and write to Azure Blob storage.</span></span> <span data-ttu-id="bba8b-183">Você pode usar o Spark para processar todos os dados existentes e, depois, armazenar os resultados novamente no armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="bba8b-183">You can use Spark to process any of your existing data, and then store the results again in Blob storage.</span></span>

<span data-ttu-id="bba8b-184">Para salvar arquivos ou modelos no armazenamento de Blobs, você precisa especificar o caminho corretamente.</span><span class="sxs-lookup"><span data-stu-id="bba8b-184">To save models or files in Blob storage, you need to properly specify the path.</span></span> <span data-ttu-id="bba8b-185">Faça referência ao contêiner padrão anexado ao cluster Spark usando um caminho que começa com `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="bba8b-185">Reference the default container attached to the Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="bba8b-186">Faça referência a outros locais usando `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="bba8b-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="bba8b-187">O exemplo de código a seguir especifica o local dos dados de entrada a serem lidos e o caminho para o armazenamento de blobs que é anexado ao cluster Spark no qual o modelo será salvo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-187">The following code sample specifies the location of the input data to be read and the path to Blob storage that is attached to the Spark cluster where the model will be saved.</span></span>

    # SET PATHS TO DATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET THE MODEL STORAGE DIRECTORY PATH
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-to-the-schema"></a><span data-ttu-id="bba8b-188">Importar dados, criar um RDD e definir um quadro de dados de acordo com o esquema</span><span class="sxs-lookup"><span data-stu-id="bba8b-188">Import data, create an RDD, and define a data frame according to the schema</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE SCHEMA BASED ON THE HEADER OF THE FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING TO THE SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE THE CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER THE DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="bba8b-189">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-189">**Output:**</span></span>

<span data-ttu-id="bba8b-190">Tempo de execução da célula: oito segundos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-190">Time to run the cell: 8 seconds.</span></span>

### <a name="query-the-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="bba8b-191">Consultar a tabela e importar os resultados em um quadro de dados</span><span class="sxs-lookup"><span data-stu-id="bba8b-191">Query the table and import results in a data frame</span></span>
<span data-ttu-id="bba8b-192">Em seguida, consulte a tabela de tarifas, os dados do passageiro e da gorjeta; filtre dados corrompidos e externos e imprima várias linhas.</span><span class="sxs-lookup"><span data-stu-id="bba8b-192">Next, query the table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY THE DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY THE TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="bba8b-193">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-193">**Output:**</span></span>

| <span data-ttu-id="bba8b-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="bba8b-194">fare_amount</span></span> | <span data-ttu-id="bba8b-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="bba8b-195">passenger_count</span></span> | <span data-ttu-id="bba8b-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="bba8b-196">tip_amount</span></span> | <span data-ttu-id="bba8b-197">tipped</span><span class="sxs-lookup"><span data-stu-id="bba8b-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="bba8b-198">13,5</span><span class="sxs-lookup"><span data-stu-id="bba8b-198">13.5</span></span> |<span data-ttu-id="bba8b-199">1.0</span><span class="sxs-lookup"><span data-stu-id="bba8b-199">1.0</span></span> |<span data-ttu-id="bba8b-200">2,9</span><span class="sxs-lookup"><span data-stu-id="bba8b-200">2.9</span></span> |<span data-ttu-id="bba8b-201">1.0</span><span class="sxs-lookup"><span data-stu-id="bba8b-201">1.0</span></span> |
|        <span data-ttu-id="bba8b-202">16,0</span><span class="sxs-lookup"><span data-stu-id="bba8b-202">16.0</span></span> |<span data-ttu-id="bba8b-203">2,0</span><span class="sxs-lookup"><span data-stu-id="bba8b-203">2.0</span></span> |<span data-ttu-id="bba8b-204">3.4</span><span class="sxs-lookup"><span data-stu-id="bba8b-204">3.4</span></span> |<span data-ttu-id="bba8b-205">1.0</span><span class="sxs-lookup"><span data-stu-id="bba8b-205">1.0</span></span> |
|        <span data-ttu-id="bba8b-206">10,5</span><span class="sxs-lookup"><span data-stu-id="bba8b-206">10.5</span></span> |<span data-ttu-id="bba8b-207">2,0</span><span class="sxs-lookup"><span data-stu-id="bba8b-207">2.0</span></span> |<span data-ttu-id="bba8b-208">1.0</span><span class="sxs-lookup"><span data-stu-id="bba8b-208">1.0</span></span> |<span data-ttu-id="bba8b-209">1.0</span><span class="sxs-lookup"><span data-stu-id="bba8b-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="bba8b-210">Visualização e exploração de dados</span><span class="sxs-lookup"><span data-stu-id="bba8b-210">Data exploration and visualization</span></span>
<span data-ttu-id="bba8b-211">Depois de trazer os dados para o Spark, a próxima etapa no processo de Ciência de dados será obter uma compreensão mais profunda dos dados por meio de exploração e visualização.</span><span class="sxs-lookup"><span data-stu-id="bba8b-211">After you bring the data into Spark, the next step in the Data Science process is to gain a deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="bba8b-212">Nesta seção, você examinará os dados de táxi usando consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="bba8b-212">In this section, you examine the taxi data by using SQL queries.</span></span> <span data-ttu-id="bba8b-213">Depois, importará os resultados em um quadro de dados a fim de plotar as variáveis de destino e os recursos potenciais para inspeção visual usando o recurso de visualização automática do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="bba8b-213">Then, import the results into a data frame to plot the target variables and prospective features for visual inspection by using the auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-to-plot-data"></a><span data-ttu-id="bba8b-214">Usar local e palavra mágica do SQL para plotar dados</span><span class="sxs-lookup"><span data-stu-id="bba8b-214">Use local and SQL magic to plot data</span></span>
<span data-ttu-id="bba8b-215">Por padrão, a saída de qualquer trecho de código executado em um notebook Jupyter é disponibilizada no contexto da sessão que é persistida nos nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="bba8b-215">By default, the output of any code snippet that you run from a Jupyter notebook is available within the context of the session that is persisted on the worker nodes.</span></span> <span data-ttu-id="bba8b-216">Se desejar salvar uma corrida nos nós de trabalho para cada cálculo e, se todos os dados necessários para o cálculo estiverem disponíveis localmente no nó do servidor do Jupyter (que é o nó de cabeçalho), você poderá usar a palavra mágica `%%local` para executar o trecho de código no servidor do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="bba8b-216">If you want to save a trip to the worker nodes for every computation, and if all the data that you need for your computation is available locally on the Jupyter server node (which is the head node), you can use the `%%local` magic to run the code snippet on the Jupyter server.</span></span>

* <span data-ttu-id="bba8b-217">**Palavra mágica do SQL** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="bba8b-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="bba8b-218">O kernel HDInsight Spark dá suporte a consultas do HiveQL fáceis e embutidas no SQLContext.</span><span class="sxs-lookup"><span data-stu-id="bba8b-218">The HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="bba8b-219">O argumento (`-o VARIABLE_NAME`) persiste a saída da consulta SQL como um quadro de dados do Pandas no servidor do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="bba8b-219">The (`-o VARIABLE_NAME`) argument persists the output of the SQL query as a Pandas data frame on the Jupyter server.</span></span> <span data-ttu-id="bba8b-220">Isso significa que ele estará disponível no modo local.</span><span class="sxs-lookup"><span data-stu-id="bba8b-220">This means it'll be available in the local mode.</span></span>
* <span data-ttu-id="bba8b-221">`%%local` **palavra mágica**.</span><span class="sxs-lookup"><span data-stu-id="bba8b-221">`%%local` **magic**.</span></span> <span data-ttu-id="bba8b-222">A palavra mágica `%%local` executa o código localmente no servidor do Jupyter, que é o nó de cabeçalho do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bba8b-222">The `%%local` magic runs the code locally on the Jupyter server, which is the head node of the HDInsight cluster.</span></span> <span data-ttu-id="bba8b-223">Normalmente, você usa a palavra mágica `%%local` em conjunto com a palavra mágica `%%sql` com o parâmetro `-o`.</span><span class="sxs-lookup"><span data-stu-id="bba8b-223">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with the `-o` parameter.</span></span> <span data-ttu-id="bba8b-224">O parâmetro `-o` persistiria a saída da consulta SQL localmente e, em seguida, as palavras mágicas `%%local` disparariam o próximo conjunto de trechos de código para serem executados localmente na saída das consultas SQL que é persistida localmente.</span><span class="sxs-lookup"><span data-stu-id="bba8b-224">The `-o` parameter would persist the output of the SQL query locally, and then `%%local` magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally.</span></span>

### <a name="query-the-data-by-using-sql"></a><span data-ttu-id="bba8b-225">Consultar os dados usando SQL</span><span class="sxs-lookup"><span data-stu-id="bba8b-225">Query the data by using SQL</span></span>
<span data-ttu-id="bba8b-226">Essa consulta recupera as corridas de táxi por valor da tarifa, contagem de passageiros e valor da gorjeta.</span><span class="sxs-lookup"><span data-stu-id="bba8b-226">This query retrieves the taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN THE SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="bba8b-227">No código a seguir, a palavra mágica `%%local` cria um quadro de dados locais, sqlResults.</span><span class="sxs-lookup"><span data-stu-id="bba8b-227">In the following code, the `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="bba8b-228">Você pode usar sqlResults para plotar usando matplotlib.</span><span class="sxs-lookup"><span data-stu-id="bba8b-228">You can use sqlResults to plot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="bba8b-229">A palavra mágica local é usada várias vezes neste artigo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="bba8b-230">Se o conjunto de dados for grande, obtenha a amostra para criar um quadro de dados que possa se ajustar na memória local.</span><span class="sxs-lookup"><span data-stu-id="bba8b-230">If your data set is large, please sample to create a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-the-data"></a><span data-ttu-id="bba8b-231">Plotar os dados</span><span class="sxs-lookup"><span data-stu-id="bba8b-231">Plot the data</span></span>
<span data-ttu-id="bba8b-232">Você poderá plotar usando o código Python quando o quadro de dados estiver no contexto local como um quadro de dados Panda.</span><span class="sxs-lookup"><span data-stu-id="bba8b-232">You can plot by using Python code after the data frame is in local context as a Pandas data frame.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES.
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="bba8b-233">O kernel do Spark visualiza automaticamente a saída das consultas SQL (HiveQL) depois que você executa o código.</span><span class="sxs-lookup"><span data-stu-id="bba8b-233">The Spark kernel automatically visualizes the output of SQL (HiveQL) queries after you run the code.</span></span> <span data-ttu-id="bba8b-234">Você pode escolher entre vários tipos de visualizações:</span><span class="sxs-lookup"><span data-stu-id="bba8b-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="bba8b-235">Tabela</span><span class="sxs-lookup"><span data-stu-id="bba8b-235">Table</span></span>
* <span data-ttu-id="bba8b-236">Pizza</span><span class="sxs-lookup"><span data-stu-id="bba8b-236">Pie</span></span>
* <span data-ttu-id="bba8b-237">Linha</span><span class="sxs-lookup"><span data-stu-id="bba8b-237">Line</span></span>
* <span data-ttu-id="bba8b-238">Área</span><span class="sxs-lookup"><span data-stu-id="bba8b-238">Area</span></span>
* <span data-ttu-id="bba8b-239">Barra</span><span class="sxs-lookup"><span data-stu-id="bba8b-239">Bar</span></span>

<span data-ttu-id="bba8b-240">Este é o código para plotar os dados:</span><span class="sxs-lookup"><span data-stu-id="bba8b-240">Here's the code to plot the data:</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


<span data-ttu-id="bba8b-241">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-241">**Output:**</span></span>

![Histograma do valor da gorjeta](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Valor de gorjeta por contagem de passageiros](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Valor de gorjeta por valor de tarifa](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="bba8b-245">Criar recursos, transformar recursos e depois preparar os dados para entrada em funções de modelagem</span><span class="sxs-lookup"><span data-stu-id="bba8b-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="bba8b-246">Para as funções de modelagem baseadas em árvore no SparkML e na MLlib, você precisa preparar o destino e os recursos usando várias técnicas, como agrupamento, indexação, codificação one-hot e vetorização.</span><span class="sxs-lookup"><span data-stu-id="bba8b-246">For tree-based modeling functions from Spark ML and MLlib, you have to prepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="bba8b-247">Veja os procedimentos desta seção:</span><span class="sxs-lookup"><span data-stu-id="bba8b-247">Here are the procedures to follow in this section:</span></span>

1. <span data-ttu-id="bba8b-248">Criar um novo recurso **reunindo** horários em blocos de tempo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="bba8b-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="bba8b-249">Aplicar **indexação e codificação one-hot** em recursos categóricos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-249">Apply **indexing and one-hot encoding** to categorical features.</span></span>
3. <span data-ttu-id="bba8b-250">**Criar amostras e dividir o conjunto de dados** em frações de teste e treinamento.</span><span class="sxs-lookup"><span data-stu-id="bba8b-250">**Sample and split the data set** into training and test fractions.</span></span>
4. <span data-ttu-id="bba8b-251">**Especificar os recursos e a variável de treinamento**e depois criar RDDs (conjuntos de dados distribuídos e resilientes) de ponto de sinalização de entrada para treinamentos de codificação indexada e one-hot, ou quadros de dados.</span><span class="sxs-lookup"><span data-stu-id="bba8b-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="bba8b-252">**Categorizar e vetorizar recursos e destinos** automaticamente para uso como entradas para modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="bba8b-252">Automatically **categorize and vectorize features and targets** to use as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="bba8b-253">Criar um novo recurso reunindo horários em blocos de tempo de tráfego</span><span class="sxs-lookup"><span data-stu-id="bba8b-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="bba8b-254">Este código mostra como criar um novo recurso reunindo horários em blocos de tempo de tráfego e como armazenar em cache o quadro de dados resultante na memória.</span><span class="sxs-lookup"><span data-stu-id="bba8b-254">This code shows you how to create a new feature by binning hours into traffic time buckets and how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="bba8b-255">Quando RDDs e quadros de dados são usados repetidamente, o armazenamento em cache leva a tempos de execução melhores.</span><span class="sxs-lookup"><span data-stu-id="bba8b-255">Where RDDs and data frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="bba8b-256">Da mesma forma, você armazenará os RDDs e os quadros de dados em cache em vários estágios nos procedimentos finais.</span><span class="sxs-lookup"><span data-stu-id="bba8b-256">Accordingly, you'll cache RDDs and data frames at several stages in the following procedures.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE THE DATA FRAME IN MEMORY AND MATERIALIZE THE DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="bba8b-257">Indexação e codificação one-hot de recursos categóricos</span><span class="sxs-lookup"><span data-stu-id="bba8b-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="bba8b-258">As funções de modelagem e previsão de MLlib exigem que recursos com dados de entrada categóricos sejam indexados ou codificados antes do uso.</span><span class="sxs-lookup"><span data-stu-id="bba8b-258">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="bba8b-259">Esta seção mostra a você como indexar ou codificar recursos categóricos para entrada nas funções de modelagem.</span><span class="sxs-lookup"><span data-stu-id="bba8b-259">This section shows you how to index or encode categorical features for input into the modeling functions.</span></span>

<span data-ttu-id="bba8b-260">Dependendo do modelo, você precisa indexá-lo ou codificá-lo de maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="bba8b-260">You need to index or encode your models in different ways, depending on the model.</span></span> <span data-ttu-id="bba8b-261">Por exemplo, modelos de regressão logística e lineares exigem codificação one-hot.</span><span class="sxs-lookup"><span data-stu-id="bba8b-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="bba8b-262">Por exemplo, um recurso com três categorias pode ser expandido em três colunas de recurso.</span><span class="sxs-lookup"><span data-stu-id="bba8b-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="bba8b-263">Cada coluna conteria 0 ou 1, dependendo da categoria de uma observação.</span><span class="sxs-lookup"><span data-stu-id="bba8b-263">Each column would contain 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="bba8b-264">A MLlib fornece a função [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) para executar a codificação one-hot.</span><span class="sxs-lookup"><span data-stu-id="bba8b-264">MLlib provides the [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="bba8b-265">Esse codificador mapeia uma coluna de índices de rótulo para uma coluna de vetores binários com, no máximo, um valor único.</span><span class="sxs-lookup"><span data-stu-id="bba8b-265">This encoder maps a column of label indices to a column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="bba8b-266">Com essa codificação, os algoritmos que esperam recursos numéricos valiosos, como a regressão logística, são aplicados em recursos categóricos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied to categorical features.</span></span>

<span data-ttu-id="bba8b-267">Aqui, você transforma apenas quatro variáveis para mostrar exemplos, que são cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bba8b-267">Here you transform only four variables to show examples, which are character strings.</span></span> <span data-ttu-id="bba8b-268">Também é possível indexar outras variáveis, como dia da semana, representadas por valores numéricos, como variáveis categóricas.</span><span class="sxs-lookup"><span data-stu-id="bba8b-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="bba8b-269">Para indexação, use `StringIndexer()` e para codificação one-hot, use as funções `OneHotEncoder()` da MLlib.</span><span class="sxs-lookup"><span data-stu-id="bba8b-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="bba8b-270">Aqui está o código para indexar e codificar recursos categóricos:</span><span class="sxs-lookup"><span data-stu-id="bba8b-270">Here is the code to index and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="bba8b-271">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-271">**Output:**</span></span>

<span data-ttu-id="bba8b-272">Tempo de execução da célula: quatro segundos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-272">Time to run the cell: 4 seconds.</span></span>

### <a name="sample-and-split-the-data-set-into-training-and-test-fractions"></a><span data-ttu-id="bba8b-273">Criar amostras e dividir o conjunto de dados em frações de teste e treinamento</span><span class="sxs-lookup"><span data-stu-id="bba8b-273">Sample and split the data set into training and test fractions</span></span>
<span data-ttu-id="bba8b-274">Esse código cria uma amostragem aleatória dos dados (25% neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="bba8b-274">This code creates a random sampling of the data (25%, in this example).</span></span> <span data-ttu-id="bba8b-275">Embora a amostragem não seja necessário para este exemplo, devido ao tamanho do conjunto de dados, o artigo demonstra como é possível obter amostras para que você saiba como usá-lo para seu próprio problema, quando for necessário.</span><span class="sxs-lookup"><span data-stu-id="bba8b-275">Although sampling is not required for this example due to the size of the data set, the article shows you how you can sample so that you know how to use it for your own problems when needed.</span></span> <span data-ttu-id="bba8b-276">Quando as amostras são grandes, isso pode economizar um tempo significativo durante o treinamento de modelos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="bba8b-277">Em seguida, dividimos o exemplo em uma parte de treinamento (75% neste exemplo) e uma parte de teste (25% neste exemplo) para usar na classificação e na modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="bba8b-277">Next, split the sample into a training part (75%, in this example) and a testing part (25%, in this example) to use in classification and regression modeling.</span></span>

<span data-ttu-id="bba8b-278">Adicione um número aleatório (entre 0 e 1) à linha de alcance (em uma coluna "rand") que pode ser usado para selecionar partições de validação cruzada durante o treinamento.</span><span class="sxs-lookup"><span data-stu-id="bba8b-278">Add a random number (between 0 and 1) to each row (in a "rand" column) that can be used to select cross-validation folds during training.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT THE SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="bba8b-279">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-279">**Output:**</span></span>

<span data-ttu-id="bba8b-280">Tempo de execução da célula: dois segundos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-280">Time to run the cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="bba8b-281">Especificar os recursos e a variável de treinamento, bem como criar treinamentos de codificação indexada e one-hot e entrada de testes denominada RDDs pontuais ou quadros de dados</span><span class="sxs-lookup"><span data-stu-id="bba8b-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="bba8b-282">Esta seção contém código que mostra como indexar dados de texto categóricos como um tipo de dados de ponto rotulado e codificá-lo para que ele possa ser usado para treinar e testar a regressão logística de MLlib e outros modelos de classificação.</span><span class="sxs-lookup"><span data-stu-id="bba8b-282">This section contains code that shows you how to index categorical text data as a labeled point data type, and encode it so you can use it to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="bba8b-283">Objetos de ponto rotulados são RDDs formatados de uma maneira para que sejam exigidos como dados de entrada pela maioria dos algoritmos de aprendizado de máquina na MLlib.</span><span class="sxs-lookup"><span data-stu-id="bba8b-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="bba8b-284">Um [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) é um vetor local, denso ou esparso, associado a um rótulo/resposta.</span><span class="sxs-lookup"><span data-stu-id="bba8b-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="bba8b-285">Nesse código, você pode especificar a variável de destino (dependente) e os recursos a serem usados para treinar modelos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-285">In this code, you specify the target (dependent) variable and the features to use to train models.</span></span> <span data-ttu-id="bba8b-286">Depois, você cria treinamentos de codificação indexada e one-hot e RDDs de ponto de entrada de teste ou quadros de dados.</span><span class="sxs-lookup"><span data-stu-id="bba8b-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY THE TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="bba8b-287">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-287">**Output:**</span></span>

<span data-ttu-id="bba8b-288">Tempo de execução da célula: quatro segundos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-288">Time to run the cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-to-use-as-inputs-for-machine-learning-models"></a><span data-ttu-id="bba8b-289">Categorizar e vetorizar recursos e destinos automaticamente para uso como entradas para modelos de aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="bba8b-289">Automatically categorize and vectorize features and targets to use as inputs for machine learning models</span></span>
<span data-ttu-id="bba8b-290">Use o AM do Spark para categorize o destino e os recursos para uso em funções de modelagem baseadas em árvore.</span><span class="sxs-lookup"><span data-stu-id="bba8b-290">Use Spark ML to categorize the target and features to use in tree-based modeling functions.</span></span> <span data-ttu-id="bba8b-291">O código conclui duas tarefas:</span><span class="sxs-lookup"><span data-stu-id="bba8b-291">The code completes two tasks:</span></span>

* <span data-ttu-id="bba8b-292">Cria um destino binário para classificação atribuindo um valor de 0 ou 1 para cada ponto de dados entre 0 e 1 usando um valor de limite de 0,5.</span><span class="sxs-lookup"><span data-stu-id="bba8b-292">Creates a binary target for classification by assigning a value of 0 or 1 to each data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="bba8b-293">Categoriza automaticamente os recursos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-293">Automatically categorizes features.</span></span> <span data-ttu-id="bba8b-294">Se o número de valores numéricos distintos para qualquer um dos recursos for menor do que 32, esse recurso será categorizado.</span><span class="sxs-lookup"><span data-stu-id="bba8b-294">If the number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="bba8b-295">Este é o código para essas duas tarefas.</span><span class="sxs-lookup"><span data-stu-id="bba8b-295">Here's the code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE THE TARGET FOR THE BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR THE REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="bba8b-296">Modelo de classificação binária: prevê se uma gorjeta será paga ou não</span><span class="sxs-lookup"><span data-stu-id="bba8b-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="bba8b-297">Nesta seção, você cria três tipos de modelo de classificação binária para prever se uma gorjeta será paga ou não:</span><span class="sxs-lookup"><span data-stu-id="bba8b-297">In this section, you create three types of binary classification models to predict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="bba8b-298">Um **modelo de regressão logística`LogisticRegression()` usando a função**  do ML do Spark</span><span class="sxs-lookup"><span data-stu-id="bba8b-298">A **logistic regression model** by using the Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="bba8b-299">Um **modelo de classificação de floresta aleatória** usando a função `RandomForestClassifier()` da AM do Spark</span><span class="sxs-lookup"><span data-stu-id="bba8b-299">A **random forest classification model** by using the Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="bba8b-300">Um **modelo de classificação de árvore de aumento gradiente** usando a função `GradientBoostedTrees()` da MLlib</span><span class="sxs-lookup"><span data-stu-id="bba8b-300">A **gradient boosting tree classification model** by using the MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="bba8b-301">Criar um modelo de regressão logística</span><span class="sxs-lookup"><span data-stu-id="bba8b-301">Create a logistic regression model</span></span>
<span data-ttu-id="bba8b-302">Em seguida, crie um modelo de regressão logística usando a função `LogisticRegression()` da AM do Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-302">Next, create a logistic regression model by using the Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="bba8b-303">Crie o código de compilação de modelo usando uma série de etapas:</span><span class="sxs-lookup"><span data-stu-id="bba8b-303">You create the model building code in a series of steps:</span></span>

1. <span data-ttu-id="bba8b-304">**Treinar os dados do modelo** com um conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="bba8b-304">**Train the model** data with one parameter set.</span></span>
2. <span data-ttu-id="bba8b-305">**Avaliar o modelo** em um conjunto de dados de teste com métricas.</span><span class="sxs-lookup"><span data-stu-id="bba8b-305">**Evaluate the model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="bba8b-306">**Salvar modelo** no armazenamento de Blobs para consumo futuro.</span><span class="sxs-lookup"><span data-stu-id="bba8b-306">**Save the model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="bba8b-307">**Pontuar o modelo** em relação aos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="bba8b-307">**Score the model** against test data.</span></span>
5. <span data-ttu-id="bba8b-308">**Plotar os resultados** com curvas ROC (característica de operação de recepção).</span><span class="sxs-lookup"><span data-stu-id="bba8b-308">**Plot the results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="bba8b-309">Veja o código para esses procedimentos:</span><span class="sxs-lookup"><span data-stu-id="bba8b-309">Here's the code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON THE TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE THE MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="bba8b-310">Carregue, pontue e salve os resultados.</span><span class="sxs-lookup"><span data-stu-id="bba8b-310">Load, score, and save the results.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD THE SAVED MODEL AND SCORE THE TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON THE TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="bba8b-311">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-311">**Output:**</span></span>

<span data-ttu-id="bba8b-312">ROC nos dados de teste = 0,9827381497557599</span><span class="sxs-lookup"><span data-stu-id="bba8b-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="bba8b-313">Use o Python em quadros de dados locais Panda para plotar a curva ROC.</span><span class="sxs-lookup"><span data-stu-id="bba8b-313">Use Python on local Pandas data frames to plot the ROC curve.</span></span>

    # QUERY THE RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT THE ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT THE ROC CURVE
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


<span data-ttu-id="bba8b-314">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-314">**Output:**</span></span>

![Curva ROC de gorjeta ou não](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="bba8b-316">Criar um modelo de classificação de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="bba8b-316">Create a random forest classification model</span></span>
<span data-ttu-id="bba8b-317">Em seguida, criamos um modelo de classificação de floresta aleatória usando a função `RandomForestClassifier()` da AM do Spark e avaliamos o modelo nos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="bba8b-317">Next, create a random forest classification model by using the Spark ML `RandomForestClassifier()` function, and then evaluate the model on test data.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE THE RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT THE MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE THE MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="bba8b-318">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-318">**Output:**</span></span>

<span data-ttu-id="bba8b-319">ROC nos dados de teste = 0,9847103571552683</span><span class="sxs-lookup"><span data-stu-id="bba8b-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="bba8b-320">Criar um modelo de classificação GBT</span><span class="sxs-lookup"><span data-stu-id="bba8b-320">Create a GBT classification model</span></span>
<span data-ttu-id="bba8b-321">Em seguida, criamos um modelo de classificação GBT usando a função `GradientBoostedTrees()` da MLlib e avaliamos o modelo nos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="bba8b-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate the model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN THE MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE THE MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE THE MODEL ON TEST INSTANCES AND THE COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS TO EVALUATE THE MODEL ON THE TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="bba8b-322">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-322">**Output:**</span></span>

<span data-ttu-id="bba8b-323">Área sob a curva ROC = 0,9846895479241554</span><span class="sxs-lookup"><span data-stu-id="bba8b-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="bba8b-324">Modelo de regressão: prever o valor da gorjeta</span><span class="sxs-lookup"><span data-stu-id="bba8b-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="bba8b-325">Nesta seção, você criará dois tipos de modelo de regressão para prever o valor da gorjeta:</span><span class="sxs-lookup"><span data-stu-id="bba8b-325">In this section, you create two types of regression models to predict the tip amount:</span></span>

* <span data-ttu-id="bba8b-326">Um **modelo de regressão linear regularizado** usando a função `LinearRegression()` da AM do Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-326">A **regularized linear regression model** by using the Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="bba8b-327">Você salvará o modelo e avaliará o modelo nos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="bba8b-327">You'll save the model and evaluate the model on test data.</span></span>
* <span data-ttu-id="bba8b-328">Um **modelo de regressão de árvore de aumento gradiente** usando a função `GBTRegressor()` da AM do Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-328">A **gradient-boosting tree regression model** by using the Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="bba8b-329">Criar um modelo de regressão linear regularizada</span><span class="sxs-lookup"><span data-stu-id="bba8b-329">Create a regularized linear regression model</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING THE SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT THE MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE THE MODEL OVER THE TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE THE MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT THE COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="bba8b-330">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-330">**Output:**</span></span>

<span data-ttu-id="bba8b-331">Tempo de execução da célula: 13 segundos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-331">Time to run the cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="bba8b-332">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-332">**Output:**</span></span>

<span data-ttu-id="bba8b-333">R-sqr nos dados de teste = 0,5960320470835743</span><span class="sxs-lookup"><span data-stu-id="bba8b-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="bba8b-334">Em seguida, consulte os resultados do teste como um quadro de dados e use AutoVizWidget e matplotlib para visualizá-los.</span><span class="sxs-lookup"><span data-stu-id="bba8b-334">Next, query the test results as a data frame and use AutoVizWidget and matplotlib to visualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="bba8b-335">O código cria um quadro de dados local da saída da consulta e plota os dados.</span><span class="sxs-lookup"><span data-stu-id="bba8b-335">The code creates a local data frame from the query output and plots the data.</span></span> <span data-ttu-id="bba8b-336">A palavra mágica `%%local` cria um quadro de dados local, `sqlResults`, que pode ser usado para plotar com matplotlib.</span><span class="sxs-lookup"><span data-stu-id="bba8b-336">The `%%local` magic creates a local data frame, `sqlResults`, which you can use to plot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="bba8b-337">Essa palavra mágica do Spark será usada várias vezes neste artigo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="bba8b-338">Se a quantidade de dados for grande, você deverá obter uma amostra para criar um quadro de dados que se ajuste à memória local.</span><span class="sxs-lookup"><span data-stu-id="bba8b-338">If the amount of data is large, you should sample to create a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="bba8b-339">Crie plotagens usando matplotlib do Python.</span><span class="sxs-lookup"><span data-stu-id="bba8b-339">Create plots by using Python matplotlib.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT THE RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="bba8b-340">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-340">**Output:**</span></span>

![Valor da gorjeta: real vs. previsto](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="bba8b-342">Criar um modelo de regressão GBT</span><span class="sxs-lookup"><span data-stu-id="bba8b-342">Create a GBT regression model</span></span>
<span data-ttu-id="bba8b-343">Crie um modelo de regressão GBT usando a função `GBTRegressor()` da AM do Spark e avalie o modelo nos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="bba8b-343">Create a GBT regression model by using the Spark ML `GBTRegressor()` function, and then evaluate the model on test data.</span></span>

<span data-ttu-id="bba8b-344">[GBTs (árvores com aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="bba8b-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="bba8b-345">As GBTs treinam árvores de decisão iterativamente para minimizar uma função de perda.</span><span class="sxs-lookup"><span data-stu-id="bba8b-345">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="bba8b-346">Você pode usar GBTs para regressão e classificação.</span><span class="sxs-lookup"><span data-stu-id="bba8b-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="bba8b-347">Elas podem manipular recursos categóricos, não exigem o dimensionamento de recursos e são capazes de capturar não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="bba8b-348">Use-as também em uma configuração de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="bba8b-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="bba8b-349">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-349">**Output:**</span></span>

<span data-ttu-id="bba8b-350">R-sqr do teste é: 0,7655383534596654</span><span class="sxs-lookup"><span data-stu-id="bba8b-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="bba8b-351">Utilitários de modelagem avançada para otimização</span><span class="sxs-lookup"><span data-stu-id="bba8b-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="bba8b-352">Nesta seção, use utilitários de aprendizado de máquina que os desenvolvedores usam frequentemente para otimização do modelo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="bba8b-353">Especificamente, você pode otimizar os modelos de AM de três maneiras diferentes usando a limpeza de parâmetro e a validação cruzada:</span><span class="sxs-lookup"><span data-stu-id="bba8b-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="bba8b-354">Dividir os dados em conjuntos de treinamento e validação, otimizar o modelo usando a limpeza de hiperparâmetro em um conjunto de treinamento e avaliar um conjunto de validação (regressão linear)</span><span class="sxs-lookup"><span data-stu-id="bba8b-354">Split the data into train and validation sets, optimize the model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="bba8b-355">Otimizar o modelo usando a validação cruzada e a limpeza de hiperparâmetro com a função CrossValidator do SparkML (classificação binária)</span><span class="sxs-lookup"><span data-stu-id="bba8b-355">Optimize the model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="bba8b-356">Otimizar o modelo usando o código personalizado de validação cruzada e limpeza de parâmetro para utilizar qualquer função de aprendizado de máquina e o conjunto de parâmetros (regressão linear)</span><span class="sxs-lookup"><span data-stu-id="bba8b-356">Optimize the model by using custom cross-validation and parameter-sweeping code to use any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="bba8b-357">**Validação cruzada** é uma técnica que avalia quão bem um modelo treinado em um conjunto de dados conhecido será generalizado para prever os recursos dos conjuntos de dados nos quais ele não foi treinado.</span><span class="sxs-lookup"><span data-stu-id="bba8b-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize to predict the features of data sets on which it has not been trained.</span></span> <span data-ttu-id="bba8b-358">A ideia geral por trás dessa técnica é que um modelo é treinado em um conjunto de dados conhecidos em e, em seguida, a precisão de suas previsões é testada em relação a um conjunto de dados independente.</span><span class="sxs-lookup"><span data-stu-id="bba8b-358">The general idea behind this technique is that a model is trained on a data set of known data, and then the accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="bba8b-359">Uma implementação comum é dividir um conjunto de dados em partições *k*e, em seguida, treinar o modelo em um estilo round-robin em todas, exceto uma das partições.</span><span class="sxs-lookup"><span data-stu-id="bba8b-359">A common implementation is to divide a data set into *k*-folds, and then train the model in a round-robin fashion on all but one of the folds.</span></span>

<span data-ttu-id="bba8b-360">**Otimização do hiperparâmetro** é o problema de escolher um conjunto de hiperparâmetros para um algoritmo de aprendizado, normalmente com o objetivo de otimizar uma medida de desempenho do algoritmo em um conjunto de dados independente.</span><span class="sxs-lookup"><span data-stu-id="bba8b-360">**Hyper-parameter optimization** is the problem of choosing a set of hyper-parameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="bba8b-361">Um hiperparâmetro é um valor que você deve especificar fora do procedimento de treinamento do modelo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-361">A hyper-parameter is a value that you must specify outside the model training procedure.</span></span> <span data-ttu-id="bba8b-362">As suposições sobre esses valores de hiperparâmetro podem afetar a flexibilidade e a precisão do modelo.</span><span class="sxs-lookup"><span data-stu-id="bba8b-362">Assumptions about hyper-parameter values can affect the flexibility and accuracy of the model.</span></span> <span data-ttu-id="bba8b-363">As árvores de decisão têm hiperparâmetros, por exemplo, como a profundidade desejada e o número de folhas na árvore.</span><span class="sxs-lookup"><span data-stu-id="bba8b-363">Decision trees have hyper-parameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="bba8b-364">Configure de um termo de penalidade de classificação incorreta para uma SVM (máquina de vetor de suporte).</span><span class="sxs-lookup"><span data-stu-id="bba8b-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="bba8b-365">Uma maneira comum de executar a otimização de hiperparâmetro é uma pesquisa de grade, também chamada de **parâmetro de limpeza**.</span><span class="sxs-lookup"><span data-stu-id="bba8b-365">A common way to perform hyper-parameter optimization is to use a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="bba8b-366">Em uma pesquisa de grade, uma pesquisa detalhada é executada nos valores de um subconjunto especificado do espaço do hiperparâmetro para um algoritmo de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="bba8b-366">In a grid search, an exhaustive search is performed through the values of a specified subset of the hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="bba8b-367">A validação cruzada pode fornecer uma métrica de desempenho para classificar os resultados ideais produzidos pelo algoritmo de pesquisa de grade.</span><span class="sxs-lookup"><span data-stu-id="bba8b-367">Cross-validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="bba8b-368">Se você usar a limpeza de hiperparâmetro para validação cruzada, poderá ajudar a limitar problemas como sobreajuste de um modelo aos dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="bba8b-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model to training data.</span></span> <span data-ttu-id="bba8b-369">Dessa forma, o modelo retém a capacidade de aplicar ao conjunto geral de dados do qual os dados de treinamento foram extraídos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-369">This way, the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="bba8b-370">Otimizar um modelo de regressão linear com a limpeza de hiperparâmetro</span><span class="sxs-lookup"><span data-stu-id="bba8b-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="bba8b-371">Em seguida, divida os dados em conjuntos de treinamento e validação, use a limpeza de hiperparâmetro em um conjunto de treinamento para otimizar o modelo e avalie um conjunto de validação (regressão linear).</span><span class="sxs-lookup"><span data-stu-id="bba8b-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set to optimize the model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE THE ESTIMATOR FUNCTION: `THE LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE THE PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET), AND THEN THE SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="bba8b-372">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-372">**Output:**</span></span>

<span data-ttu-id="bba8b-373">R-sqr do teste é: 0,6226484708501209</span><span class="sxs-lookup"><span data-stu-id="bba8b-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-the-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="bba8b-374">Otimizar o modelo de classificação binária usando a limpeza de hiperparâmetro e a validação cruzada</span><span class="sxs-lookup"><span data-stu-id="bba8b-374">Optimize the binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="bba8b-375">Esta seção mostra como otimizar um modelo de classificação binária usando a limpeza de hiperparâmetro e a validação cruzada.</span><span class="sxs-lookup"><span data-stu-id="bba8b-375">This section shows you how to optimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="bba8b-376">Isso usa a função `CrossValidator` de AM do Spark.</span><span class="sxs-lookup"><span data-stu-id="bba8b-376">This uses the Spark ML `CrossValidator` function.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS TO USE WITH THE TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE THE ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY THE NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE THE TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE THE TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="bba8b-377">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-377">**Output:**</span></span>

<span data-ttu-id="bba8b-378">Tempo de execução da célula: 33 segundos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-378">Time to run the cell: 33 seconds.</span></span>

### <a name="optimize-the-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="bba8b-379">Otimizar o modelo de regressão linear usando código personalizado de validação cruzada e limpeza de parâmetro</span><span class="sxs-lookup"><span data-stu-id="bba8b-379">Optimize the linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="bba8b-380">Em seguida, otimize o modelo usando código personalizado e identifique os melhores parâmetros do modelo usando o critério de precisão mais alta.</span><span class="sxs-lookup"><span data-stu-id="bba8b-380">Next, optimize the model by using custom code, and identify the best model parameters by using the criterion of highest accuracy.</span></span> <span data-ttu-id="bba8b-381">Em seguida, criamos o modelo final, avaliamos o modelo nos dados de teste e salvamos o modelo no armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="bba8b-381">Then, create the final model, evaluate the model on test data, and save the model in Blob storage.</span></span> <span data-ttu-id="bba8b-382">Por fim, carregue o modelo, pontue os dados de teste e avalie sua precisão.</span><span class="sxs-lookup"><span data-stu-id="bba8b-382">Finally, load the model, score test data, and evaluate accuracy.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE PARAMETER GRID AND THE NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY THE NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND THE PARAMETER GRID TO GET AND IDENTIFY THE BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 to (nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 to (numModels-1)) {
            for (nParams <- 0 to (numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET THE BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 to (numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE THE BEST MODEL WITH THE BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE THE BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON THE TRAINING SET WITH THE BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


    # LOAD THE MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST THE MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="bba8b-383">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="bba8b-383">**Output:**</span></span>

<span data-ttu-id="bba8b-384">Tempo de execução da célula: 61 segundos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-384">Time to run the cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="bba8b-385">Consumir automaticamente modelos da aprendizado de máquina compilados no Spark com o Scala</span><span class="sxs-lookup"><span data-stu-id="bba8b-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="bba8b-386">Para obter uma visão geral dos tópicos que explicam as tarefas que compõem o processo de Ciência de dados no Azure, confira [Processo de Ciência de Dados de Equipe](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="bba8b-386">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="bba8b-387">[Passo a passo do processo de ciência de dados de equipe](data-science-process-walkthroughs.md) descreve outras orientações de ponta a ponta que demonstram as etapas no Processo de ciência de dados de equipe para cenários específicos.</span><span class="sxs-lookup"><span data-stu-id="bba8b-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="bba8b-388">As orientações também mostram como combinar ferramentas e serviços de nuvem e locais em um fluxo de trabalho ou pipeline para criar um aplicativo inteligente.</span><span class="sxs-lookup"><span data-stu-id="bba8b-388">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>

<span data-ttu-id="bba8b-389">[Pontuar modelos de aprendizado de máquina criados no Spark](machine-learning-data-science-spark-model-consumption.md) mostra como usar o código Scala para carregar e pontuar automaticamente novos conjuntos de dados com modelos de aprendizado de máquina compilados no Spark e salvos no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="bba8b-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how to use Scala code to automatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="bba8b-390">Você pode seguir as instruções fornecidas nele e simplesmente substituir o código Python pelo código Scala neste artigo para o consumo automatizado.</span><span class="sxs-lookup"><span data-stu-id="bba8b-390">You can follow the instructions provided there, and simply replace the Python code with Scala code in this article for automated consumption.</span></span>

