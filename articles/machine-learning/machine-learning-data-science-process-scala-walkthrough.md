---
title: "aaaData ciência usando Scala e Spark no Azure | Microsoft Docs"
description: "Como toouse Scala para tarefas com de aprendizado de máquina supervisionada Olá Spark MLlib e Spark ML pacotes escalonáveis em um cluster Spark no HDInsight."
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
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="e0b6c-103">Ciência de Dados usando o Scala e o Spark no Azure</span><span class="sxs-lookup"><span data-stu-id="e0b6c-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="e0b6c-104">Este artigo mostra como toouse Scala para tarefas de aprendizado de máquina supervisionado com hello MLlib escalonável Spark e Spark ML pacotes em um cluster Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="e0b6c-105">Orienta você pelas tarefas de saudação que constituem Olá [processo de ciência de dados](http://aka.ms/datascienceprocess): inclusão de dados e exploração, visualização, engenharia de recurso, modelagem e consumo de modelo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="e0b6c-106">modelos Olá artigo Olá incluem Regressão logística e linear, florestas aleatórias e árvores ampliadas gradiente (GBTs), além de tootwo comum supervisionado tarefas de aprendizado de máquina:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="e0b6c-107">Problema de regressão: previsão do valor de dica de saudação ($) para uma viagem de táxi</span><span class="sxs-lookup"><span data-stu-id="e0b6c-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="e0b6c-108">Classificação binária: previsão da gorjeta ou não (1/0) para uma corrida de táxi</span><span class="sxs-lookup"><span data-stu-id="e0b6c-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="e0b6c-109">processo de modelagem de saudação requer treinamento e avaliação em um conjunto de dados de teste e métricas de precisão relevantes.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="e0b6c-110">Neste artigo, você pode aprender como toostore esses modelos no armazenamento de BLOBs do Azure e como tooscore e avaliar o desempenho previsível.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="e0b6c-111">Este artigo também aborda hello mais avançados tópicos de como toooptimize modelos usando validação cruzada e parâmetro hyper limpeza.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="e0b6c-112">dados de saudação usados são um exemplo hello 2013 NYC táxi viagem e passagens do conjunto de dados disponível no GitHub.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="e0b6c-113">[Scala](http://www.scala-lang.org/), um idioma com base na máquina virtual Java com hello, integra conceitos de linguagem funcional e orientada a objeto.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="e0b6c-114">É uma linguagem escalonável toodistributed adequado de processamento na nuvem Olá, e é executado no Azure Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="e0b6c-115">[Spark](http://spark.apache.org/) é tooboost Olá desempenho de aplicativos de análise de dados grandes do processamento de uma estrutura de processamento paralelo de código-fonte aberto que dá suporte na memória.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="e0b6c-116">mecanismo de processamento do Spark Olá é construído para velocidade, facilidade de uso e análise sofisticada.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="e0b6c-117">As funcionalidades de computação distribuídas na memória do Spark fazem dele uma boa escolha para algoritmos iterativos em cálculos de gráfico e aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="e0b6c-118">Olá [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) pacote fornece um conjunto uniforme de APIs de alto nível criado com base em dados quadros que podem ajudá-lo a criar e ajustar prática pipelines de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="e0b6c-119">[MLlib](http://spark.apache.org/mllib/) é a biblioteca de aprendizado de máquina escalonável do Spark, que oferece recursos de modelagem ambiente distribuído toothis.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="e0b6c-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) é Olá hospedado no Azure oferta do código-fonte aberto Spark.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="e0b6c-121">Também inclui suporte para blocos de anotações do Jupyter Scala no cluster do Spark Olá, e pode executar tootransform Spark SQL de consultas interativas, filtrar e visualizar os dados armazenados no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="e0b6c-122">Olá Scala trechos de código neste artigo que fornecem soluções hello e mostram gráficos relevantes Olá dados de saudação toovisualize executar em blocos de anotações do Jupyter instalados nos clusters do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="e0b6c-123">etapas de modelagem Olá nestes tópicos tiver o código que mostra a você como tootrain, avaliar, salvar e consumir cada tipo de modelo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="e0b6c-124">etapas de instalação Hello e o código neste artigo são para o Azure HDInsight 3.4 Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="e0b6c-125">No entanto, Olá código neste artigo e Olá [Scala de anotações do Jupyter](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) são genéricos e deve funcionar em qualquer cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="e0b6c-126">Olá instalação de cluster e etapas de gerenciamento podem ser ligeiramente diferentes da que é mostrado neste artigo, se você não estiver usando o HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="e0b6c-127">Para um tópico que mostra como as tarefas de toocomplete de Python em vez de Scala toouse para um processo de ciência de dados de ponta a ponta, consulte [ciência de dados usando o Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e0b6c-128">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0b6c-128">Prerequisites</span></span>
* <span data-ttu-id="e0b6c-129">Você precisa ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-129">You must have an Azure subscription.</span></span> <span data-ttu-id="e0b6c-130">Se ainda não tiver uma, [obtenha uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="e0b6c-131">Você precisa de uma saudação de toocomplete de cluster Azure HDInsight 3.4 Spark 1.6 procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="e0b6c-132">toocreate um cluster, consulte as instruções de saudação em [Introdução: criar o Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="e0b6c-133">Definir tipo de cluster hello e versão em Olá **Selecionar tipo de Cluster** menu.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![Configuração de tipo de cluster do HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="e0b6c-135">Para obter uma descrição de dados de viagem táxi Olá NYC e instruções sobre como tooexecute código de um bloco de anotações do Jupyter no cluster do Spark hello, consulte a seções relevantes Olá [visão geral de ciência de dados usando o Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="e0b6c-136">Execute o código de Scala de um bloco de anotações do Jupyter no cluster do Spark Olá</span><span class="sxs-lookup"><span data-stu-id="e0b6c-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="e0b6c-137">Você pode iniciar um bloco de anotações do Jupyter de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="e0b6c-138">Localizar o cluster do Spark Olá em seu painel e clique tooenter página de gerenciamento de saudação para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="e0b6c-139">Em seguida, clique em **painéis do Cluster**e, em seguida, clique em **Jupyter Notebook** tooopen notebook de saudação associada Olá Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![Painel do cluster e notebooks Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="e0b6c-141">Você também pode acessar blocos de anotações do Jupyter em https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="e0b6c-142">Substituir *clustername* com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="e0b6c-143">Senha de saudação é necessária para o administrador conta tooaccess Olá Jupyter blocos de anotações.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![Vá tooJupyter notebooks usando o nome do cluster Olá](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="e0b6c-145">Selecione **Scala** toosee um diretório com alguns exemplos de blocos de anotações predefinidos Olá que use PySpark API.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="e0b6c-146">Olá exploração de modelagem e pontuação usando notebook Scala.ipynb que contém exemplos de código Olá para este conjunto de tópicos do Spark está disponível em [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="e0b6c-147">Você pode carregar notebook Olá diretamente do GitHub toohello servidor de Jupyter Notebook em seu cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="e0b6c-148">Na home page Jupyter, clique em Olá **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="e0b6c-149">No Explorador de arquivos Olá, cole Olá GitHub (conteúdo bruto) URL do bloco de anotações do hello Scala e, em seguida, clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="e0b6c-150">o bloco de anotações do Hello Scala estará disponível em Olá URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="e0b6c-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="e0b6c-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="e0b6c-152">Configuração: contextos predefinidos de Spark e Hive, palavras mágicas Spark e bibliotecas Spark</span><span class="sxs-lookup"><span data-stu-id="e0b6c-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="e0b6c-153">Contextos predefinidos de Spark e Hive</span><span class="sxs-lookup"><span data-stu-id="e0b6c-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="e0b6c-154">kernels do Spark Olá que são fornecidos com blocos de anotações do Jupyter tem contextos predefinidos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="e0b6c-155">Você não precisa tooexplicitly conjunto Olá Spark ou Hive contextos antes de começar a trabalhar com o aplicativo hello que você está desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="e0b6c-156">Olá contextos predefinidos são:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-156">hello preset contexts are:</span></span>

* <span data-ttu-id="e0b6c-157">`sc` para SparkContext</span><span class="sxs-lookup"><span data-stu-id="e0b6c-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="e0b6c-158">`sqlContext` para HiveContext</span><span class="sxs-lookup"><span data-stu-id="e0b6c-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="e0b6c-159">Palavras mágicas do Spark</span><span class="sxs-lookup"><span data-stu-id="e0b6c-159">Spark magics</span></span>
<span data-ttu-id="e0b6c-160">Olá kernel Spark fornece algumas predefinidas "magics", que são comandos especiais que podem ser chamados com `%%`.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="e0b6c-161">Dois desses comandos são usados em Olá exemplos de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="e0b6c-162">`%%local`Especifica que código Olá nas linhas subsequentes será executado localmente.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="e0b6c-163">código de saudação deve ser código Scala válido.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="e0b6c-164">`%%sql -o <variable name>` executa uma consulta do Hive no `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="e0b6c-165">Se hello `-o` parâmetro for passado, o resultado de saudação de consulta de saudação é mantido no hello `%%local` Scala contexto como um quadro de dados Spark.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="e0b6c-166">Para obter mais informações sobre kernels Olá para blocos de anotações do Jupyter e seus predefinido "magics" que você chamar com `%%` (por exemplo, `%%local`), consulte [Kernels disponíveis para blocos de anotações do Jupyter com HDInsight Spark Linux clusters em HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="e0b6c-167">Importar bibliotecas</span><span class="sxs-lookup"><span data-stu-id="e0b6c-167">Import libraries</span></span>
<span data-ttu-id="e0b6c-168">Importar Olá Spark, MLlib e outras bibliotecas que você precisará usando Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="e0b6c-169">Ingestão de dados</span><span class="sxs-lookup"><span data-stu-id="e0b6c-169">Data ingestion</span></span>
<span data-ttu-id="e0b6c-170">primeira etapa Olá Olá processo de ciência de dados é dados de saudação tooingest que você deseja tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="e0b6c-171">Colocar dados saudação de fontes externas ou sistemas onde ele reside em seu ambiente de modelagem e exploração de dados.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="e0b6c-172">Neste artigo, você ingestão de dados de saudação são um exemplo de 0,1% que se unidas Olá táxi viagem e passagens do arquivo de (armazenado como um arquivo. tsv).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="e0b6c-173">ambiente de modelagem e exploração de dados Olá é Spark.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="e0b6c-174">Esta seção contém Olá Olá de toocomplete código série de tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="e0b6c-175">Definir os caminhos de diretório para o armazenamento de dados e de modelos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="e0b6c-176">Ler no conjunto de dados entrada hello (armazenado como um arquivo. tsv).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="e0b6c-177">Defina um esquema para dados hello e limpar hello.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="e0b6c-178">Criar um quadro de dados limpo e armazená-lo em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="e0b6c-179">Registre dados saudação como uma tabela temporária no SQLContext.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="e0b6c-180">Consultar a tabela de saudação e importar resultados de saudação para um quadro de dados.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="e0b6c-181">Definir caminhos de diretório para locais de armazenamento no armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="e0b6c-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="e0b6c-182">Spark pode ler e gravar tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="e0b6c-183">Você pode usar Spark tooprocess qualquer um dos seus dados existentes e armazenar os resultados de saudação novamente no armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="e0b6c-184">modelos de toosave ou arquivos no armazenamento de Blob, você precisará tooproperly especificar caminho hello.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="e0b6c-185">Contêiner de padrão de saudação de referência anexado cluster do Spark toohello usando um caminho que começa com `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="e0b6c-186">Faça referência a outros locais usando `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="e0b6c-187">Hello exemplo de código a seguir especifica local Olá Olá toobe de dados de entrada de leitura e Olá caminho tooBlob armazenamento de cluster do Spark toohello anexado qual modelo Olá será salvo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="e0b6c-188">Importar dados, criar um RDD e definir um quadro de dados de acordo com o esquema de toohello</span><span class="sxs-lookup"><span data-stu-id="e0b6c-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
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

    # CAST VARIABLES ACCORDING toohello SCHEMA
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

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="e0b6c-189">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-189">**Output:**</span></span>

<span data-ttu-id="e0b6c-190">Célula de saudação do tempo toorun: 8 segundos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="e0b6c-191">Consultar a tabela de saudação e importar resultados de um quadro de dados</span><span class="sxs-lookup"><span data-stu-id="e0b6c-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="e0b6c-192">Em seguida, a tabela de saudação de consulta de passagens, passageiro e dados de dica; Filtrar dados corrompidos e distantes; e imprima várias linhas.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="e0b6c-193">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-193">**Output:**</span></span>

| <span data-ttu-id="e0b6c-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="e0b6c-194">fare_amount</span></span> | <span data-ttu-id="e0b6c-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="e0b6c-195">passenger_count</span></span> | <span data-ttu-id="e0b6c-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="e0b6c-196">tip_amount</span></span> | <span data-ttu-id="e0b6c-197">tipped</span><span class="sxs-lookup"><span data-stu-id="e0b6c-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="e0b6c-198">13,5</span><span class="sxs-lookup"><span data-stu-id="e0b6c-198">13.5</span></span> |<span data-ttu-id="e0b6c-199">1.0</span><span class="sxs-lookup"><span data-stu-id="e0b6c-199">1.0</span></span> |<span data-ttu-id="e0b6c-200">2,9</span><span class="sxs-lookup"><span data-stu-id="e0b6c-200">2.9</span></span> |<span data-ttu-id="e0b6c-201">1.0</span><span class="sxs-lookup"><span data-stu-id="e0b6c-201">1.0</span></span> |
|        <span data-ttu-id="e0b6c-202">16,0</span><span class="sxs-lookup"><span data-stu-id="e0b6c-202">16.0</span></span> |<span data-ttu-id="e0b6c-203">2,0</span><span class="sxs-lookup"><span data-stu-id="e0b6c-203">2.0</span></span> |<span data-ttu-id="e0b6c-204">3.4</span><span class="sxs-lookup"><span data-stu-id="e0b6c-204">3.4</span></span> |<span data-ttu-id="e0b6c-205">1.0</span><span class="sxs-lookup"><span data-stu-id="e0b6c-205">1.0</span></span> |
|        <span data-ttu-id="e0b6c-206">10,5</span><span class="sxs-lookup"><span data-stu-id="e0b6c-206">10.5</span></span> |<span data-ttu-id="e0b6c-207">2,0</span><span class="sxs-lookup"><span data-stu-id="e0b6c-207">2.0</span></span> |<span data-ttu-id="e0b6c-208">1.0</span><span class="sxs-lookup"><span data-stu-id="e0b6c-208">1.0</span></span> |<span data-ttu-id="e0b6c-209">1.0</span><span class="sxs-lookup"><span data-stu-id="e0b6c-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="e0b6c-210">Visualização e exploração de dados</span><span class="sxs-lookup"><span data-stu-id="e0b6c-210">Data exploration and visualization</span></span>
<span data-ttu-id="e0b6c-211">Depois de você colocar dados saudação em Spark, Olá próxima etapa no hello processo de ciência de dados é toogain uma compreensão mais profunda dos dados Olá por meio de exploração e visualização.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="e0b6c-212">Nesta seção, você pode examinar dados táxi de saudação por meio de consultas do SQL.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="e0b6c-213">Em seguida, importar Olá resultados em um tooplot de quadro de dados Olá recursos potenciais para inspeção visual e variáveis de destino usando o recurso de visualização automática de saudação do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="e0b6c-214">Usar o local e dados do SQL tooplot magic</span><span class="sxs-lookup"><span data-stu-id="e0b6c-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="e0b6c-215">Por padrão, a saída de hello qualquer trecho de código que você executa em um bloco de anotações do Jupyter está disponível no contexto de saudação da sessão de saudação que é mantido em nós de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="e0b6c-216">Se você quiser toosave nós de trabalho de toohello uma viagem para cada cálculo, e se todos os hello dados necessários para a computação está disponível localmente no nó do servidor Olá Jupyter (que é o nó principal Olá), você pode usar o hello `%%local` magic toorun código de saudação trecho de código no servidor do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="e0b6c-217">**Palavra mágica do SQL** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="e0b6c-218">Olá kernel HDInsight Spark dá suporte a consultas estilo embutido fácil SQLContext.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="e0b6c-219">saudação (`-o VARIABLE_NAME`) argumento persiste saída Olá de consulta do SQL hello como um quadro de dados no servidor do Jupyter Olá Pandas.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="e0b6c-220">Isso significa que ele estarão disponível no modo local hello.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="e0b6c-221">`%%local` **palavra mágica**.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-221">`%%local` **magic**.</span></span> <span data-ttu-id="e0b6c-222">Olá `%%local` magic executa código Olá localmente no servidor do Jupyter hello, que é o nó principal de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="e0b6c-223">Normalmente, você usa `%%local` magic em conjunto com hello `%%sql` magic com hello `-o` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="e0b6c-224">Olá `-o` parâmetro persistir Olá saída de hello SQL consulta localmente e, em seguida, `%%local` magic acionaria o próximo conjunto de saudação do toorun de trecho de código localmente contra a saída da saudação de consultas SQL Olá persistido localmente.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="e0b6c-225">Consultar dados saudação usando SQL</span><span class="sxs-lookup"><span data-stu-id="e0b6c-225">Query hello data by using SQL</span></span>
<span data-ttu-id="e0b6c-226">Essa consulta recupera viagens de táxi Olá pela quantidade de passagens, contagem de passageiro e quantidade de dica.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="e0b6c-227">Em Olá código a seguir, Olá `%%local` magic cria um quadro de dados local, sqlResults.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="e0b6c-228">Você pode usar sqlResults tooplot usando matplotlib.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="e0b6c-229">A palavra mágica local é usada várias vezes neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="e0b6c-230">Se seu conjunto de dados for grande, por favor, exemplo toocreate um quadro de dados que pode caber na memória local.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="e0b6c-231">Plotar dados Olá</span><span class="sxs-lookup"><span data-stu-id="e0b6c-231">Plot hello data</span></span>
<span data-ttu-id="e0b6c-232">Você pode plotar usando código Python após o quadro de dados Olá no contexto local como um quadro de dados Pandas.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="e0b6c-233">kernel do Spark Olá automaticamente visualiza saída Olá de consultas SQL (HiveQL) depois de executar código hello.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="e0b6c-234">Você pode escolher entre vários tipos de visualizações:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="e0b6c-235">Tabela</span><span class="sxs-lookup"><span data-stu-id="e0b6c-235">Table</span></span>
* <span data-ttu-id="e0b6c-236">Pizza</span><span class="sxs-lookup"><span data-stu-id="e0b6c-236">Pie</span></span>
* <span data-ttu-id="e0b6c-237">Linha</span><span class="sxs-lookup"><span data-stu-id="e0b6c-237">Line</span></span>
* <span data-ttu-id="e0b6c-238">Área</span><span class="sxs-lookup"><span data-stu-id="e0b6c-238">Area</span></span>
* <span data-ttu-id="e0b6c-239">Barra</span><span class="sxs-lookup"><span data-stu-id="e0b6c-239">Bar</span></span>

<span data-ttu-id="e0b6c-240">Aqui está a dados de Olá Olá código tooplot:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-240">Here's hello code tooplot hello data:</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="e0b6c-241">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-241">**Output:**</span></span>

![Histograma do valor da gorjeta](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Valor de gorjeta por contagem de passageiros](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Valor de gorjeta por valor de tarifa](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="e0b6c-245">Criar recursos, transformar recursos e depois preparar os dados para entrada em funções de modelagem</span><span class="sxs-lookup"><span data-stu-id="e0b6c-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="e0b6c-246">Para funções de modelagem baseado na árvore do Spark ML e MLlib, você tem destino tooprepare e recursos usando uma variedade de técnicas, como agrupamento, indexação, ativa uma codificação e vetorização.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="e0b6c-247">Aqui estão Olá toofollow de procedimentos nesta seção:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="e0b6c-248">Criar um novo recurso **reunindo** horários em blocos de tempo de tráfego.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="e0b6c-249">Aplicar **hot uma codificação e indexação** toocategorical recursos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="e0b6c-250">**Exemplo e dividir o conjunto de dados de Olá** em frações de treinamento e teste.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="e0b6c-251">**Especificar os recursos e a variável de treinamento**e depois criar RDDs (conjuntos de dados distribuídos e resilientes) de ponto de sinalização de entrada para treinamentos de codificação indexada e one-hot, ou quadros de dados.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="e0b6c-252">Automaticamente **categorizar e vectorize recursos e destinos** toouse como entradas para modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="e0b6c-253">Criar um novo recurso reunindo horários em blocos de tempo de tráfego</span><span class="sxs-lookup"><span data-stu-id="e0b6c-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="e0b6c-254">Este código mostra como os buckets de toocreate um novo recurso guardando horas em vez de tráfego e como toocache Olá resultante quadro de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="e0b6c-255">Onde os quadros de dados e RDDs forem usados repetidamente, cache leva tooimproved tempos de execução.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="e0b6c-256">Da mesma forma, você vai cache quadros de dados e RDDs em vários estágios de saudação procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

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

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="e0b6c-257">Indexação e codificação one-hot de recursos categóricos</span><span class="sxs-lookup"><span data-stu-id="e0b6c-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="e0b6c-258">Olá modelagem e prever a funções de MLlib exigem recursos com entrada de dados categóricos toobe indexado ou codificado toouse anterior.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="e0b6c-259">Esta seção mostra como tooindex ou codificar recursos categóricos para entrada em Olá funções da modelagem.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="e0b6c-260">Você precisa tooindex ou codifica seus modelos de maneiras diferentes, dependendo do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="e0b6c-261">Por exemplo, modelos de regressão logística e lineares exigem codificação one-hot.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="e0b6c-262">Por exemplo, um recurso com três categorias pode ser expandido em três colunas de recurso.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="e0b6c-263">Cada coluna contém 0 ou 1, dependendo da categoria de saudação de uma observação.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="e0b6c-264">MLlib fornece Olá [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) função hot uma codificação.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="e0b6c-265">Este codificador mapeia uma coluna da coluna de tooa de índices de rótulo dos vetores de binários no máximo um único um valor.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="e0b6c-266">Com essa codificação, os algoritmos que esperam recursos com valores numéricos, como a regressão logística, podem ser aplicada toocategorical recursos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="e0b6c-267">Aqui você transformar exemplos de tooshow apenas quatro variáveis, que são cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="e0b6c-268">Também é possível indexar outras variáveis, como dia da semana, representadas por valores numéricos, como variáveis categóricas.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="e0b6c-269">Para indexação, use `StringIndexer()` e para codificação one-hot, use as funções `OneHotEncoder()` da MLlib.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="e0b6c-270">Aqui está o hello tooindex de código e codificar recursos categóricos:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-270">Here is hello code tooindex and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
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

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="e0b6c-271">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-271">**Output:**</span></span>

<span data-ttu-id="e0b6c-272">Célula de saudação do tempo toorun: 4 segundos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="e0b6c-273">Exemplo e dividir Olá conjunto de dados em frações de treinamento e teste</span><span class="sxs-lookup"><span data-stu-id="e0b6c-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="e0b6c-274">Esse código cria uma amostragem aleatória de dados de saudação (25%, neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="e0b6c-275">Embora a amostragem não é necessária para este exemplo devido tamanho toohello saudação do conjunto de dados, o artigo de saudação mostra como você pode criar amostra para que você saiba como toouse-lo para seus próprios problemas quando necessário.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="e0b6c-276">Quando as amostras são grandes, isso pode economizar um tempo significativo durante o treinamento de modelos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="e0b6c-277">Em seguida, dividir o exemplo hello em uma parte de treinamento (75%, neste exemplo) e um teste parte toouse (25%, neste exemplo) de classificação e modelagem de regressão.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="e0b6c-278">Adicione uma linha de tooeach de número aleatório (entre 0 e 1) (em uma coluna de "rand") que pode ser usado tooselect validação cruzada dobras durante o treinamento.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

    # RECORD hello START TIME
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

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="e0b6c-279">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-279">**Output:**</span></span>

<span data-ttu-id="e0b6c-280">Célula de saudação do tempo toorun: 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="e0b6c-281">Especificar os recursos e a variável de treinamento, bem como criar treinamentos de codificação indexada e one-hot e entrada de testes denominada RDDs pontuais ou quadros de dados</span><span class="sxs-lookup"><span data-stu-id="e0b6c-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="e0b6c-282">Esta seção contém código que mostra como tooindex categórica e dados de texto como um rótulo do ponto de tipo de dados, codificação-lo, você pode usar outros modelos de classificação e de teste e tootrain MLlib de regressão logística.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="e0b6c-283">Objetos de ponto rotulados são RDDs formatados de uma maneira para que sejam exigidos como dados de entrada pela maioria dos algoritmos de aprendizado de máquina na MLlib.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="e0b6c-284">Um [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) é um vetor local, denso ou esparso, associado a um rótulo/resposta.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="e0b6c-285">Nesse código, você pode especificar variável (dependente) de destino hello e modelos de tootrain Olá recursos toouse.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="e0b6c-286">Depois, você cria treinamentos de codificação indexada e one-hot e RDDs de ponto de entrada de teste ou quadros de dados.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="e0b6c-287">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-287">**Output:**</span></span>

<span data-ttu-id="e0b6c-288">Célula de saudação do tempo toorun: 4 segundos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="e0b6c-289">Categorizar automaticamente e vectorize toouse de recursos e destinos como entradas para modelos de aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="e0b6c-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="e0b6c-290">Use Spark ML toocategorize toouse de destino e os recursos do hello em funções de modelagem baseado na árvore.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="e0b6c-291">código de saudação conclui duas tarefas:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="e0b6c-292">Cria um destino binário para classificação, atribuindo um valor de 0 ou 1 ponto de dados de tooeach entre 0 e 1 usando um valor de limite de 0,5.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="e0b6c-293">Categoriza automaticamente os recursos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-293">Automatically categorizes features.</span></span> <span data-ttu-id="e0b6c-294">Se o número de saudação de valores numéricos distintos para qualquer recurso for menor que 32, esse recurso é categorizado.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="e0b6c-295">Este é o código de saudação para essas duas tarefas.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-295">Here's hello code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

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

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="e0b6c-296">Modelo de classificação binária: prevê se uma gorjeta será paga ou não</span><span class="sxs-lookup"><span data-stu-id="e0b6c-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="e0b6c-297">Nesta seção, você deve criar três tipos de toopredict de modelos de classificação binária ou não uma dica deve ser pago:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="e0b6c-298">Um **modelo de regressão logística** usando Olá Spark ML `LogisticRegression()` função</span><span class="sxs-lookup"><span data-stu-id="e0b6c-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="e0b6c-299">Um **modelo de classificação de floresta aleatório** usando Olá Spark ML `RandomForestClassifier()` função</span><span class="sxs-lookup"><span data-stu-id="e0b6c-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="e0b6c-300">Um **modelo de classificação de árvore de ampliação gradiente** usando Olá MLlib `GradientBoostedTrees()` função</span><span class="sxs-lookup"><span data-stu-id="e0b6c-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="e0b6c-301">Criar um modelo de regressão logística</span><span class="sxs-lookup"><span data-stu-id="e0b6c-301">Create a logistic regression model</span></span>
<span data-ttu-id="e0b6c-302">Em seguida, crie um modelo de regressão logística usando Olá Spark ML `LogisticRegression()` função.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="e0b6c-303">Criar modelo Olá compilar o código em uma série de etapas:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="e0b6c-304">**Treinar modelo de saudação** dados com um conjunto de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="e0b6c-305">**Avaliar modelo Olá** em um conjunto de dados de teste com métricas.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="e0b6c-306">**Salvar modelo Olá** no armazenamento de Blob para consumo futuro.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="e0b6c-307">**Modelo de saudação de pontuação** em relação aos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="e0b6c-308">**Plotar resultados Olá** com receptor operacional curvas característica (ROC).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="e0b6c-309">Este é o código de saudação para estes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-309">Here's hello code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="e0b6c-310">Carregar, pontuação e salvar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-310">Load, score, and save hello results.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="e0b6c-311">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-311">**Output:**</span></span>

<span data-ttu-id="e0b6c-312">ROC nos dados de teste = 0,9827381497557599</span><span class="sxs-lookup"><span data-stu-id="e0b6c-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="e0b6c-313">Use o Python no local Pandas dados quadros tooplot Olá ROC em curva.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
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


<span data-ttu-id="e0b6c-314">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-314">**Output:**</span></span>

![Curva ROC de gorjeta ou não](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="e0b6c-316">Criar um modelo de classificação de floresta aleatória</span><span class="sxs-lookup"><span data-stu-id="e0b6c-316">Create a random forest classification model</span></span>
<span data-ttu-id="e0b6c-317">Em seguida, crie um modelo de classificação aleatória de floresta usando Olá Spark ML `RandomForestClassifier()` de função e, em seguida, avaliar o modelo de saudação nos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="e0b6c-318">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-318">**Output:**</span></span>

<span data-ttu-id="e0b6c-319">ROC nos dados de teste = 0,9847103571552683</span><span class="sxs-lookup"><span data-stu-id="e0b6c-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="e0b6c-320">Criar um modelo de classificação GBT</span><span class="sxs-lookup"><span data-stu-id="e0b6c-320">Create a GBT classification model</span></span>
<span data-ttu-id="e0b6c-321">Em seguida, crie um modelo de classificação GBT por meio do MLlib `GradientBoostedTrees()` de função e, em seguida, avaliar o modelo de saudação nos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="e0b6c-322">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-322">**Output:**</span></span>

<span data-ttu-id="e0b6c-323">Área sob a curva ROC = 0,9846895479241554</span><span class="sxs-lookup"><span data-stu-id="e0b6c-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="e0b6c-324">Modelo de regressão: prever o valor da gorjeta</span><span class="sxs-lookup"><span data-stu-id="e0b6c-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="e0b6c-325">Nesta seção, você deve criar dois tipos de valor de dica regressão modelos toopredict hello:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="e0b6c-326">Um **modelo de regressão linear regularizada** usando Olá Spark ML `LinearRegression()` função.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="e0b6c-327">Você salvar o modelo de saudação e avaliar modelo Olá em dados de teste.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="e0b6c-328">Um **Impulsionamento de gradiente modelo de regressão de árvore** usando Olá Spark ML `GBTRegressor()` função.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="e0b6c-329">Criar um modelo de regressão linear regularizada</span><span class="sxs-lookup"><span data-stu-id="e0b6c-329">Create a regularized linear regression model</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="e0b6c-330">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-330">**Output:**</span></span>

<span data-ttu-id="e0b6c-331">Célula de saudação do tempo toorun: 13 segundos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-331">Time toorun hello cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="e0b6c-332">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-332">**Output:**</span></span>

<span data-ttu-id="e0b6c-333">R-sqr nos dados de teste = 0,5960320470835743</span><span class="sxs-lookup"><span data-stu-id="e0b6c-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="e0b6c-334">Em seguida, consulta Olá resultados de teste como um quadro de dados e usar toovisualize AutoVizWidget e matplotlib-lo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="e0b6c-335">código de saudação cria um quadro de dados local saudação do resultado da consulta e plota dados saudação.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="e0b6c-336">Olá `%%local` mágico cria um quadro de dados local, `sqlResults`, que você pode usar tooplot com matplotlib.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="e0b6c-337">Essa palavra mágica do Spark será usada várias vezes neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="e0b6c-338">Se a quantidade de saudação de dados for grande, você deve exemplo toocreate um quadro de dados que pode caber na memória local.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="e0b6c-339">Crie plotagens usando matplotlib do Python.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-339">Create plots by using Python matplotlib.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="e0b6c-340">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-340">**Output:**</span></span>

![Valor da gorjeta: real vs. previsto](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="e0b6c-342">Criar um modelo de regressão GBT</span><span class="sxs-lookup"><span data-stu-id="e0b6c-342">Create a GBT regression model</span></span>
<span data-ttu-id="e0b6c-343">Criar um modelo de regressão GBT usando Olá Spark ML `GBTRegressor()` de função e, em seguida, avaliar o modelo de saudação nos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="e0b6c-344">[GBTs (árvores com aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="e0b6c-345">Árvores de decisão de treinar GBTs iterativamente toominimize uma função de perda.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="e0b6c-346">Você pode usar GBTs para regressão e classificação.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="e0b6c-347">Elas podem manipular recursos categóricos, não exigem o dimensionamento de recursos e são capazes de capturar não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="e0b6c-348">Use-as também em uma configuração de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="e0b6c-349">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-349">**Output:**</span></span>

<span data-ttu-id="e0b6c-350">R-sqr do teste é: 0,7655383534596654</span><span class="sxs-lookup"><span data-stu-id="e0b6c-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="e0b6c-351">Utilitários de modelagem avançada para otimização</span><span class="sxs-lookup"><span data-stu-id="e0b6c-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="e0b6c-352">Nesta seção, use utilitários de aprendizado de máquina que os desenvolvedores usam frequentemente para otimização do modelo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="e0b6c-353">Especificamente, você pode otimizar os modelos de AM de três maneiras diferentes usando a limpeza de parâmetro e a validação cruzada:</span><span class="sxs-lookup"><span data-stu-id="e0b6c-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="e0b6c-354">Dividir dados saudação em conjuntos de treinamento e validação, otimizar modelo hello usando a limpeza de parâmetro hyper em um conjunto de treinamento e avaliar em um conjunto de validação (regressão linear)</span><span class="sxs-lookup"><span data-stu-id="e0b6c-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="e0b6c-355">Otimizar o modelo hello usando a validação cruzada e hyper-varredura de parâmetro por meio CrossValidator função do Spark ML (classificação binária)</span><span class="sxs-lookup"><span data-stu-id="e0b6c-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="e0b6c-356">Otimizar modelo hello usando código personalizado de validação cruzada e limpeza de parâmetro toouse qualquer conjunto de função e o parâmetro (regressão linear) de aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="e0b6c-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="e0b6c-357">**Validação cruzada** é uma técnica que avalia como um modelo treinado em um conjunto conhecido de dados será generalizar toopredict Olá recursos de conjuntos de dados no qual ele não foi treinado.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="e0b6c-358">Olá geral ideia essa técnica é que um modelo é treinado em um conjunto de dados de dados conhecidos e, em seguida, hello precisão de suas previsões é testado em relação a um conjunto de dados independente.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="e0b6c-359">Uma implementação comum é toodivide um conjunto de dados em *k*-dobra e, em seguida, treinar o modelo de saudação de forma round robin em apenas uma das partições de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="e0b6c-360">**Otimização de Hyper-parâmetro** Olá problema de escolher um conjunto de hyper-parâmetros para um algoritmo de aprendizado, geralmente com a meta de saudação de otimizar uma medida de desempenho do algoritmo Olá em um conjunto de dados independente.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="e0b6c-361">Um parâmetro hyper-é um valor que você deve especificar fora Olá procedimento de treinamento de modelo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="e0b6c-362">Suposições sobre valores de parâmetro hyper podem afetar flexibilidade hello e a precisão do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="e0b6c-363">Árvores de decisão têm hyper-parâmetros, por exemplo, como Olá desejado profundidade e número de folhas na árvore de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="e0b6c-364">Configure de um termo de penalidade de classificação incorreta para uma SVM (máquina de vetor de suporte).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="e0b6c-365">Uma otimização de hyper-parâmetro de tooperform de maneira comum é toouse uma pesquisa de grade, também chamado de um **varredura de parâmetro**.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="e0b6c-366">Em uma pesquisa de grade, uma pesquisa detalhada é executada por meio de valores de saudação de um subconjunto especificado de espaço de parâmetro hyper Olá para um algoritmo de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="e0b6c-367">Validação cruzada pode fornecer um toosort de métrica de desempenho os resultados ideais de Olá produzido pelo algoritmo de pesquisa de grade hello.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="e0b6c-368">Se você usar a limpeza de hyper-parâmetro de validação cruzada, você pode ajudar a problemas de limite como sobreajuste um tootraining de dados de modelo.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="e0b6c-369">Dessa forma, o modelo Olá retém Olá capacidade tooapply toohello conjunto geral de dados do qual Olá dados de treinamento foi extraídos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="e0b6c-370">Otimizar um modelo de regressão linear com a limpeza de hiperparâmetro</span><span class="sxs-lookup"><span data-stu-id="e0b6c-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="e0b6c-371">Em seguida, dividir os dados em conjuntos de treinamento e validação, use hyper-varredura de parâmetro em um treinamento defina toooptimize Olá modelo e avaliar em um conjunto de validação (regressão linear).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="e0b6c-372">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-372">**Output:**</span></span>

<span data-ttu-id="e0b6c-373">R-sqr do teste é: 0,6226484708501209</span><span class="sxs-lookup"><span data-stu-id="e0b6c-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="e0b6c-374">Otimizar o modelo de classificação binária hello usando a limpeza de validação cruzada e parâmetro hyper</span><span class="sxs-lookup"><span data-stu-id="e0b6c-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="e0b6c-375">Esta seção mostra como toooptimize uma classificação binária de modelo usando a validação cruzada e parâmetro hyper limpeza.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="e0b6c-376">Isso usa Olá Spark ML `CrossValidator` função.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-376">This uses hello Spark ML `CrossValidator` function.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="e0b6c-377">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-377">**Output:**</span></span>

<span data-ttu-id="e0b6c-378">Célula de saudação do tempo toorun: 33 segundos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="e0b6c-379">Otimizar o modelo de regressão linear hello usando código personalizado de validação cruzada e limpeza de parâmetro</span><span class="sxs-lookup"><span data-stu-id="e0b6c-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="e0b6c-380">Em seguida, otimizar modelo hello usando código personalizado e identificar os melhores parâmetros de modelo Olá usando o critério de saudação de precisão mais alta.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="e0b6c-381">Em seguida, crie o modelo final hello, avaliar modelo Olá em dados de teste e Salvar modelo Olá no armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="e0b6c-382">Por fim, carregar modelo hello, classificar dados de teste e avaliar a precisão.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
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


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
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

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="e0b6c-383">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="e0b6c-383">**Output:**</span></span>

<span data-ttu-id="e0b6c-384">Célula de saudação do tempo toorun: 61 segundos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="e0b6c-385">Consumir automaticamente modelos da aprendizado de máquina compilados no Spark com o Scala</span><span class="sxs-lookup"><span data-stu-id="e0b6c-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="e0b6c-386">Para obter uma visão geral dos tópicos que orientam você pelas tarefas de saudação que compõem o processo de ciência de dados Olá no Azure, consulte [processo de ciência de dados de equipe](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="e0b6c-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="e0b6c-387">[Explicações passo a passo do processo de ciência de dados da equipe](data-science-process-walkthroughs.md) descreve outras orientações de ponta a ponta que demonstram etapas Olá Olá processo de ciência de dados de equipe para cenários específicos.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="e0b6c-388">Olá explicações passo a passo também ilustra como toocombine de nuvem e ferramentas no local e serviços em um fluxo de trabalho ou pipeline toocreate um aplicativo inteligente.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="e0b6c-389">[Pontuação de modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md) mostra como toouse Scala código tooautomatically carregar e pontuação novos conjuntos de dados com modelos de aprendizado de máquina interna do Spark e salva no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="e0b6c-390">Você pode siga instruções Olá fornecidas e simplesmente substitua Olá código Python Scala código neste artigo para consumo automatizado.</span><span class="sxs-lookup"><span data-stu-id="e0b6c-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

