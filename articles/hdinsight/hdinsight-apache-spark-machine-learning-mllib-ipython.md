---
title: "Exemplo de aprendizado de máquina com MLlib do Spark no HDInsight – Azure | Microsoft Docs"
description: "Saiba como usar o Spark MLlib para criar um aplicativo de aprendizado de máquina que analisa um conjunto de dados usando a classificação por meio de regressão logística."
keywords: "aprendizado de máquina do spark, exemplo de aprendizado de máquina do spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: e563d4f51c9e27b20df47eca6d3eb00ac79e854f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="bd26f-104">Use o Spark MLlib para compilar uma aplicativo de aprendizado de máquina e analisar um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="bd26f-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="bd26f-105">Saiba como usar o **MLlib** do Spark para criar uma aplicativo de aprendizado de máquina para fazer a análise preditiva simples em um conjunto de dados aberto.</span><span class="sxs-lookup"><span data-stu-id="bd26f-105">Learn how to use Spark **MLlib** to create a machine learning application to do simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="bd26f-106">Das bibliotecas aprendizado de máquina internas do Spark, este exemplo usa *classificação* por meio de regressão logística.</span><span class="sxs-lookup"><span data-stu-id="bd26f-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="bd26f-107">Este exemplo também está disponível como um notebook Jupyter em um cluster do Spark (Linux) que você pode criar no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bd26f-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="bd26f-108">A experiência de bloco de anotações permite executar os trechos de código Python no próprio bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="bd26f-108">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="bd26f-109">Para acompanhar o tutorial de dentro de um bloco de anotações, crie um cluster Spark e inicie um bloco de anotações do Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="bd26f-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="bd26f-110">Em seguida, execute o bloco de anotações **Machine Learning do Spark – análise preditiva nos dados de inspeção de alimentos usando MLlib.ipynb** na pasta **Python**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="bd26f-111">MLlib é uma biblioteca Spark principal que fornece vários utilitários úteis para tarefas de aprendizado de máquina, incluindo utilitários adequados para:</span><span class="sxs-lookup"><span data-stu-id="bd26f-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="bd26f-112">classificação</span><span class="sxs-lookup"><span data-stu-id="bd26f-112">Classification</span></span>
* <span data-ttu-id="bd26f-113">Regressão</span><span class="sxs-lookup"><span data-stu-id="bd26f-113">Regression</span></span>
* <span data-ttu-id="bd26f-114">Clustering</span><span class="sxs-lookup"><span data-stu-id="bd26f-114">Clustering</span></span>
* <span data-ttu-id="bd26f-115">Modelagem de tópico</span><span class="sxs-lookup"><span data-stu-id="bd26f-115">Topic modeling</span></span>
* <span data-ttu-id="bd26f-116">Decomposição de valor singular (SVD) e análise de componente principal (PCA)</span><span class="sxs-lookup"><span data-stu-id="bd26f-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="bd26f-117">Teste de hipótese e cálculo de estatísticas de exemplo</span><span class="sxs-lookup"><span data-stu-id="bd26f-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="bd26f-118">O que são a classificação e regressão logística?</span><span class="sxs-lookup"><span data-stu-id="bd26f-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="bd26f-119">*Classificação*, uma tarefa popular de aprendizado de máquina, é o processo de classificação de dados de entrada em categorias.</span><span class="sxs-lookup"><span data-stu-id="bd26f-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="bd26f-120">É o trabalho de um algoritmo de classificação para descobrir como atribuir "rótulos" a dados de entrada que você fornece.</span><span class="sxs-lookup"><span data-stu-id="bd26f-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="bd26f-121">Por exemplo, você pode pensar em um algoritmo de aprendizado de máquina que aceite informações sobre estoque como entrada e divida o estoque em duas categorias: estoque que você deve vender e estoque que deve ser mantido.</span><span class="sxs-lookup"><span data-stu-id="bd26f-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="bd26f-122">Regressão logística é o algoritmo usado para classificação.</span><span class="sxs-lookup"><span data-stu-id="bd26f-122">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="bd26f-123">A API de regressão logística do Spark é útil para *classificação binária*ou para classificação de dados de entrada em um dos dois grupos.</span><span class="sxs-lookup"><span data-stu-id="bd26f-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="bd26f-124">Para obter mais informações sobre a regressão logística, consulte [Wikipédia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="bd26f-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="bd26f-125">Em resumo, o processo de regressão logística produz uma *função logística* que pode ser usada para prever a probabilidade de um vetor de entrada pertencer a um grupo ou outro.</span><span class="sxs-lookup"><span data-stu-id="bd26f-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="bd26f-126">Exemplo de análise preditiva em dados de inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="bd26f-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="bd26f-127">Neste exemplo, você usa o Spark para executar uma análise preditiva sobre os dados de inspeção de alimentos (**Food_Inspections1.csv**) que foi adquirido por meio do [portal de dados da cidade de Chicago](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="bd26f-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="bd26f-128">Esse conjunto de dados contém informações sobre inspeções de estabelecimentos de alimentos realizadas em Chicago, incluindo informações sobre cada estabelecimento de alimentos inspecionado, as violações encontradas (se houver) e os resultados da inspeção.</span><span class="sxs-lookup"><span data-stu-id="bd26f-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span></span> <span data-ttu-id="bd26f-129">O arquivo de dados CSV já está disponível na conta de armazenamento associada ao cluster em **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="bd26f-130">Nas etapas a seguir, você desenvolverá um modelo para ver o que é necessário para ser aprovado ou reprovado em uma inspeção de alimentos.</span><span class="sxs-lookup"><span data-stu-id="bd26f-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="bd26f-131">Comece a criar um aplicativo de aprendizado de máquina MMLib do Spark</span><span class="sxs-lookup"><span data-stu-id="bd26f-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="bd26f-132">No [portal do Azure](https://portal.azure.com/), no quadro inicial, clique no bloco do cluster Spark (se você o tiver fixado no quadro inicial).</span><span class="sxs-lookup"><span data-stu-id="bd26f-132">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="bd26f-133">Você também pode navegar até o cluster em **Procurar Tudo** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-133">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="bd26f-134">Na folha do cluster Spark, clique em **Painel do Cluster** e em **Notebook Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-134">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="bd26f-135">Se você receber uma solicitação, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="bd26f-135">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bd26f-136">Você também pode acessar o Bloco de Notas Jupyter de seu cluster abrindo a seguinte URL no navegador.</span><span class="sxs-lookup"><span data-stu-id="bd26f-136">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="bd26f-137">Substitua **CLUSTERNAME** pelo nome do cluster:</span><span class="sxs-lookup"><span data-stu-id="bd26f-137">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="bd26f-138">Crie um notebook.</span><span class="sxs-lookup"><span data-stu-id="bd26f-138">Create a notebook.</span></span> <span data-ttu-id="bd26f-139">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="bd26f-140">![Criar um bloco de anotações do Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Criar um novo bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="bd26f-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="bd26f-141">Um novo bloco de anotações é criado e aberto com o nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="bd26f-141">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="bd26f-142">Clique no nome do bloco de anotações na parte superior e digite um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="bd26f-142">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="bd26f-143">![Fornecer um nome para o bloco de anotações](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Fornecer um nome para o bloco de anotações")</span><span class="sxs-lookup"><span data-stu-id="bd26f-143">![Provide a name for the notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for the notebook")</span></span>
1. <span data-ttu-id="bd26f-144">Por ter criado um notebook usando o kernel PySpark, não será necessário criar nenhum contexto explicitamente.</span><span class="sxs-lookup"><span data-stu-id="bd26f-144">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="bd26f-145">Os contextos do Spark e do Hive são criados automaticamente para você ao executar a primeira célula do código.</span><span class="sxs-lookup"><span data-stu-id="bd26f-145">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="bd26f-146">Você pode começar a criar seu aplicativo de aprendizado de máquina importando os tipos necessários para este cenário.</span><span class="sxs-lookup"><span data-stu-id="bd26f-146">You can start building your machine learning application by importing the types required for this scenario.</span></span> <span data-ttu-id="bd26f-147">Para fazer isso, coloque o cursor na célula e pressione **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-147">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="bd26f-148">Construir um dataframe de entrada</span><span class="sxs-lookup"><span data-stu-id="bd26f-148">Construct an input dataframe</span></span>
<span data-ttu-id="bd26f-149">Podemos usar `sqlContext` para executar transformações de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="bd26f-149">We can use `sqlContext` to perform transformations on structured data.</span></span> <span data-ttu-id="bd26f-150">A primeira tarefa é carregar os dados de exemplo ((**Food_Inspections1.csv**)) em um dataframe do *Spark SQL*.</span><span class="sxs-lookup"><span data-stu-id="bd26f-150">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="bd26f-151">Como os dados brutos estão em um formato CSV, precisamos usar o contexto do Spark para efetuar pull de cada linha do arquivo na memória como texto não estruturado; em seguida, use a biblioteca CSV do Python para analisar cada linha individualmente.</span><span class="sxs-lookup"><span data-stu-id="bd26f-151">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="bd26f-152">Agora temos o arquivo CSV como um RDD.</span><span class="sxs-lookup"><span data-stu-id="bd26f-152">We now have the CSV file as an RDD.</span></span>  <span data-ttu-id="bd26f-153">Recuperaremos uma linha de RDD para compreender o esquema dos dados.</span><span class="sxs-lookup"><span data-stu-id="bd26f-153">To understand the schema of the data, we retrieve one row from the RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="bd26f-154">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd26f-154">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of the plumbing section of the Municipal Code of Chicago and Rules and Regulation of the Board of Health. OBSEVERD THE 3 COMPARTMENT SINK BACKING UP INTO THE 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding to protect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED TO REPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN THE REAR CHILDREN AREA,IN THE KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED TO REPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY THE 15MOS AREA. NEED TO BE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY THE EXPOSED HAND SINK IN THE KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: The floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED TO ELEVATE ALL FOOD ITEMS 6INCH OFF THE FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="bd26f-155">A saída anterior nos dá uma ideia do esquema do arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="bd26f-155">The preceding output gives us an idea of the schema of the input file.</span></span> <span data-ttu-id="bd26f-156">Ele inclui o nome de cada estabelecimento, o tipo de estabelecimento, o endereço, os dados da inspeção e a localização, entre outras informações.</span><span class="sxs-lookup"><span data-stu-id="bd26f-156">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> <span data-ttu-id="bd26f-157">Selecionaremos algumas colunas que serão úteis para nossa análise de previsão e agrupar os resultados como um dataframe, que usaremos então para criar uma tabela temporária.</span><span class="sxs-lookup"><span data-stu-id="bd26f-157">Let's select a few columns that are useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="bd26f-158">Agora temos um *dataframe*, `df` no qual podemos executar nossa análise.</span><span class="sxs-lookup"><span data-stu-id="bd26f-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="bd26f-159">Também temos uma chamada de tabela temporária **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="bd26f-160">Incluímos quatro colunas de interesse no dataframe: **id**, **nome**, **resultados** e **violações**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-160">We've included four columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="bd26f-161">Vamos obter uma pequena amostra dos dados:</span><span class="sxs-lookup"><span data-stu-id="bd26f-161">Let's get a small sample of the data:</span></span>

        df.show(5)

    <span data-ttu-id="bd26f-162">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd26f-162">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-the-data"></a><span data-ttu-id="bd26f-163">Entender os dados</span><span class="sxs-lookup"><span data-stu-id="bd26f-163">Understand the data</span></span>
1. <span data-ttu-id="bd26f-164">Vamos começar a ter uma ideia do que o nosso conjunto de dados contém.</span><span class="sxs-lookup"><span data-stu-id="bd26f-164">Let's start to get a sense of what our dataset contains.</span></span> <span data-ttu-id="bd26f-165">Por exemplo, quais são os diferentes valores na coluna **resultados** ?</span><span class="sxs-lookup"><span data-stu-id="bd26f-165">For example, what are the different values in the **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="bd26f-166">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd26f-166">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. <span data-ttu-id="bd26f-167">Uma rápida visualização pode nos ajudar a entender a distribuição desses resultados.</span><span class="sxs-lookup"><span data-stu-id="bd26f-167">A quick visualization can help us reason about the distribution of these outcomes.</span></span> <span data-ttu-id="bd26f-168">Já temos os dados em uma tabela temporária **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-168">We already have the data in a temporary table **CountResults**.</span></span> <span data-ttu-id="bd26f-169">Você pode executar a seguinte consulta SQL em relação à tabela para entender melhor como os resultados são distribuídos.</span><span class="sxs-lookup"><span data-stu-id="bd26f-169">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="bd26f-170">A mágica do `%%sql` seguido pelo `-o countResultsdf` assegura que a saída da consulta seja mantida localmente no servidor Jupyter (normalmente o nó principal do cluster).</span><span class="sxs-lookup"><span data-stu-id="bd26f-170">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="bd26f-171">A saída é mantida como uma estrutura de dados [Pandas](http://pandas.pydata.org/) com o nome especificado **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-171">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span>

    <span data-ttu-id="bd26f-172">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd26f-172">You should see an output like the following:</span></span>

    <span data-ttu-id="bd26f-173">![Saída da consulta SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Saída da consulta SQL")</span><span class="sxs-lookup"><span data-stu-id="bd26f-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="bd26f-174">Para saber mais sobre a palavra mágica `%%sql`, e outras palavras mágicas disponíveis com o kernel PySpark, confira [Kernels disponíveis em notebooks Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="bd26f-174">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="bd26f-175">Você também pode usar Matplotlib, uma biblioteca usada para construir a visualização de dados para criar um gráfico.</span><span class="sxs-lookup"><span data-stu-id="bd26f-175">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="bd26f-176">Como o gráfico deve ser criado a partir do dataframe **countResultsdf** mantido localmente, o trecho de código deve começar com a mágica `%%local`.</span><span class="sxs-lookup"><span data-stu-id="bd26f-176">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="bd26f-177">Isso garante que o código seja executado localmente no servidor do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="bd26f-177">This ensures that the code is run locally on the Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="bd26f-178">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd26f-178">You should see an output like the following:</span></span>

    <span data-ttu-id="bd26f-179">![Saída do aplicativo de aprendizado de máquina do Spark – gráfico de pizza com cinco conjuntos de resultados de inspeção distintos](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Saída do resultado de aprendizado de máquina de Spark")</span><span class="sxs-lookup"><span data-stu-id="bd26f-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="bd26f-180">Você pode ver que uma inspeção pode ter cinco resultados distintos:</span><span class="sxs-lookup"><span data-stu-id="bd26f-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="bd26f-181">Negócios não localizados</span><span class="sxs-lookup"><span data-stu-id="bd26f-181">Business not located</span></span>
   * <span data-ttu-id="bd26f-182">Reprovado</span><span class="sxs-lookup"><span data-stu-id="bd26f-182">Fail</span></span>
   * <span data-ttu-id="bd26f-183">Aprovado</span><span class="sxs-lookup"><span data-stu-id="bd26f-183">Pass</span></span>
   * <span data-ttu-id="bd26f-184">Aprovar c/ condições</span><span class="sxs-lookup"><span data-stu-id="bd26f-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="bd26f-185">Fora de negócio</span><span class="sxs-lookup"><span data-stu-id="bd26f-185">Out of Business</span></span>

     <span data-ttu-id="bd26f-186">Vamos desenvolver um modelo que possa adivinhar o resultado de uma inspeção de alimentos, considerando as violações.</span><span class="sxs-lookup"><span data-stu-id="bd26f-186">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span></span> <span data-ttu-id="bd26f-187">Como a regressão logística é um método de classificação binária, faz sentido agrupar os dados em duas categorias: **Reprovado** e **Aprovado**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-187">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="bd26f-188">Um "Aprovar c/Condições" ainda é uma aprovação, portanto, ao treinar o modelo, consideramos os dois resultados equivalentes.</span><span class="sxs-lookup"><span data-stu-id="bd26f-188">A "Pass w/ Conditions" is still a Pass, so when we train the model, we consider the two results equivalent.</span></span> <span data-ttu-id="bd26f-189">Dados com os outros resultados ("Negócios Não Localizados" ou "Fora de Negócio") não são úteis, então os removeremos do nosso conjunto de treinamento.</span><span class="sxs-lookup"><span data-stu-id="bd26f-189">Data with the other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="bd26f-190">Isso deve ser estar ok, já que essas duas categorias compõem uma porcentagem muito pequena dos resultados de qualquer forma.</span><span class="sxs-lookup"><span data-stu-id="bd26f-190">This should be okay since these two categories make up a very small percentage of the results anyway.</span></span>
1. <span data-ttu-id="bd26f-191">Vamos prosseguir e converter nosso dataframe existente (`df`) em um novo dataframe em que cada inspeção é representada como um par de violações de rótulo.</span><span class="sxs-lookup"><span data-stu-id="bd26f-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="bd26f-192">No nosso caso, um rótulo de `0.0` representa uma falha, um rótulo de `1.0` representa um sucesso e um rótulo de `-1.0` representa alguns resultados diferentes desses dois.</span><span class="sxs-lookup"><span data-stu-id="bd26f-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="bd26f-193">Filtraremos esses outros resultados ao calcular o novo quadro de dados.</span><span class="sxs-lookup"><span data-stu-id="bd26f-193">We filter those other results out when computing the new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="bd26f-194">Para ver a aparência dos dados rotulados, recuperaremos uma linha.</span><span class="sxs-lookup"><span data-stu-id="bd26f-194">To see what the labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="bd26f-195">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd26f-195">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="bd26f-196">Criar um modelo de regressão logística do dataframe de entrada</span><span class="sxs-lookup"><span data-stu-id="bd26f-196">Create a logistic regression model from the input dataframe</span></span>
<span data-ttu-id="bd26f-197">Nossa tarefa final é converter os dados rotulados para um formato que possa ser analisado pela regressão logística.</span><span class="sxs-lookup"><span data-stu-id="bd26f-197">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="bd26f-198">A entrada para um algoritmo de regressão logística deve ser um conjunto de *pares de vetor de recurso de rótulo*, em que o “vetor de recurso” é um vetor de números que representa o ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="bd26f-198">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span></span> <span data-ttu-id="bd26f-199">Portanto, precisamos converter a coluna "violações", que é semiestruturada e contém muitos comentários em texto livre, para uma matriz de números reais que um computador facilmente entenderia.</span><span class="sxs-lookup"><span data-stu-id="bd26f-199">So, we need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="bd26f-200">Uma abordagem de aprendizado de máquina padrão para processamento de linguagem natural é atribuir a cada palavra distinta um “índice” e então passar um vetor para o algoritmo de aprendizado de máquina, de modo que o valor de cada índice contenha a frequência relativa da palavra na cadeia de texto.</span><span class="sxs-lookup"><span data-stu-id="bd26f-200">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="bd26f-201">O MLlib oferece uma maneira fácil de executar essa operação.</span><span class="sxs-lookup"><span data-stu-id="bd26f-201">MLlib provides an easy way to perform this operation.</span></span> <span data-ttu-id="bd26f-202">Primeiro, crie tokens de cada cadeia de caracteres de violações para obter as palavras individuais em cada cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="bd26f-202">First, "tokenize" each violations string to get the individual words in each string.</span></span> <span data-ttu-id="bd26f-203">Em seguida, use um `HashingTF` para converter cada conjunto de tokens em um vetor de recurso que pode ser passado para o algoritmo de regressão logística para construir um modelo.</span><span class="sxs-lookup"><span data-stu-id="bd26f-203">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="bd26f-204">Realizamos todas essas etapas em sequência, usando um "pipeline".</span><span class="sxs-lookup"><span data-stu-id="bd26f-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a><span data-ttu-id="bd26f-205">Avaliar o modelo em um conjunto de dados de teste separado</span><span class="sxs-lookup"><span data-stu-id="bd26f-205">Evaluate the model on a separate test dataset</span></span>
<span data-ttu-id="bd26f-206">Podemos usar o modelo criado anteriormente para *prever* quais serão os resultados das novas inspeções com base nas violações observadas.</span><span class="sxs-lookup"><span data-stu-id="bd26f-206">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="bd26f-207">Tentamos esse modelo no conjunto de dados **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-207">We trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="bd26f-208">Usaremos um segundo conjunto de dados, **Food_Inspections2.csv**, para *avaliar* a força deste modelo nos dados novos.</span><span class="sxs-lookup"><span data-stu-id="bd26f-208">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span></span> <span data-ttu-id="bd26f-209">Esse segundo conjunto de dados (**Food_Inspections2.csv**) já deve estar no contêiner de armazenamento padrão associado ao cluster.</span><span class="sxs-lookup"><span data-stu-id="bd26f-209">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="bd26f-210">O trecho de código a seguir cria um novo dataframe, **predictionsDf** que contém a previsão gerada pelo modelo.</span><span class="sxs-lookup"><span data-stu-id="bd26f-210">The following snippet creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="bd26f-211">O trecho de código também cria uma tabela temporária **Previsões** com base no dataframe.</span><span class="sxs-lookup"><span data-stu-id="bd26f-211">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="bd26f-212">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd26f-212">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. <span data-ttu-id="bd26f-213">Examine uma das previsões.</span><span class="sxs-lookup"><span data-stu-id="bd26f-213">Look at one of the predictions.</span></span> <span data-ttu-id="bd26f-214">Execute este trecho de código:</span><span class="sxs-lookup"><span data-stu-id="bd26f-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="bd26f-215">Há uma previsão para a primeira entrada no conjunto de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="bd26f-215">There is a prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="bd26f-216">O método `model.transform()` aplica a mesma transformação para novos dados com o mesmo esquema e chega a uma previsão de como classificar os dados.</span><span class="sxs-lookup"><span data-stu-id="bd26f-216">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="bd26f-217">Podemos fazer algumas estatísticas simples para ter uma ideia de quão precisas foram nossas previsões:</span><span class="sxs-lookup"><span data-stu-id="bd26f-217">We can do some simple statistics to get a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="bd26f-218">A saída se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bd26f-218">The output looks like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="bd26f-219">Usar regressão logística com o Spark fornece um modelo preciso da relação entre as descrições de violações em inglês e se um determinado negócio seria aprovado ou reprovado uma inspeção de alimentos.</span><span class="sxs-lookup"><span data-stu-id="bd26f-219">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="bd26f-220">Criar uma representação visual da previsão</span><span class="sxs-lookup"><span data-stu-id="bd26f-220">Create a visual representation of the prediction</span></span>
<span data-ttu-id="bd26f-221">Agora podemos construir uma visualização final para ajudar a justificar os resultados deste teste.</span><span class="sxs-lookup"><span data-stu-id="bd26f-221">We can now construct a final visualization to help us reason about the results of this test.</span></span>

1. <span data-ttu-id="bd26f-222">Vamos começar extraindo as diferentes previsões e os resultados da tabela temporária **Predictions** criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bd26f-222">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="bd26f-223">As consultas a seguir separam a saída como *true_positive*, *false_positive*, *true_negative* e *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="bd26f-223">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="bd26f-224">Nas consultas a seguir, vamos desligar as visualização usando `-q` e também salvar a saída (usando `-o`) como quadros de dados que podem ser usados com a mágica `%%local`.</span><span class="sxs-lookup"><span data-stu-id="bd26f-224">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="bd26f-225">Por fim, use o trecho de código a seguir para gerar a plotagem usando o **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-225">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="bd26f-226">Você deve ver o seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="bd26f-226">You should see the following output:</span></span>

    <span data-ttu-id="bd26f-227">![Saída do aplicativo de aprendizado de máquina do Spark – percentuais de gráfico de pizza de inspeções em alimentos com falha.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Saída do resultado de aprendizado de máquina do Spark")</span><span class="sxs-lookup"><span data-stu-id="bd26f-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="bd26f-228">Neste gráfico, um resultado "positivo" refere-se a uma reprovação na inspeção de alimentos, enquanto um resultado negativo refere-se a uma aprovação na inspeção.</span><span class="sxs-lookup"><span data-stu-id="bd26f-228">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="bd26f-229">Fechar o notebook</span><span class="sxs-lookup"><span data-stu-id="bd26f-229">Shut down the notebook</span></span>
<span data-ttu-id="bd26f-230">Depois de concluir a execução do aplicativo, você deve encerrar o bloco de anotações para liberar os recursos.</span><span class="sxs-lookup"><span data-stu-id="bd26f-230">After you have finished running the application, you should shut down the notebook to release the resources.</span></span> <span data-ttu-id="bd26f-231">Para isso, no menu **Arquivo** do bloco de anotações, clique em **Fechar e Interromper**.</span><span class="sxs-lookup"><span data-stu-id="bd26f-231">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="bd26f-232">Isso desliga e fecha o bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="bd26f-232">This shuts down and closes the notebook.</span></span>

## <span data-ttu-id="bd26f-233"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="bd26f-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="bd26f-234">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd26f-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="bd26f-235">Cenários</span><span class="sxs-lookup"><span data-stu-id="bd26f-235">Scenarios</span></span>
* [<span data-ttu-id="bd26f-236">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="bd26f-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* <span data-ttu-id="bd26f-237">
            [Spark com Machine Learning: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="bd26f-237">[Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data](hdinsight-apache-spark-ipython-notebook-machine-learning.md)</span></span>
* [<span data-ttu-id="bd26f-238">Streaming Spark: use o Spark no HDInsight para a criação de aplicativos streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="bd26f-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="bd26f-239">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd26f-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="bd26f-240">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="bd26f-240">Create and run applications</span></span>
* [<span data-ttu-id="bd26f-241">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="bd26f-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="bd26f-242">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="bd26f-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="bd26f-243">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="bd26f-243">Tools and extensions</span></span>
* [<span data-ttu-id="bd26f-244">Use o Plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="bd26f-244">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="bd26f-245">Usar o plug-in de Ferramentas do HDInsight para depurar aplicativos Spark remotamente</span><span class="sxs-lookup"><span data-stu-id="bd26f-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="bd26f-246">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd26f-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="bd26f-247">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd26f-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="bd26f-248">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="bd26f-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="bd26f-249">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd26f-249">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="bd26f-250">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="bd26f-250">Manage resources</span></span>
* [<span data-ttu-id="bd26f-251">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd26f-251">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="bd26f-252">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="bd26f-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
