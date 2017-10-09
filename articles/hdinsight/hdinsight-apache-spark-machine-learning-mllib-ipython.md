---
title: aaaMachine aprendizado exemplo com MLlib Spark no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse Spark MLlib toocreate um aplicativo de aprendizado de máquina que analisa um conjunto de dados usando a classificação por meio de regressão logística."
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
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="9a139-104">Use o Spark MLlib toobuild uma aplicativo de aprendizado de máquina e analisar um conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="9a139-104">Use Spark MLlib toobuild a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="9a139-105">Saiba como toouse Spark **MLlib** toocreate um aplicativo toodo simples análise de previsão em um conjunto de dados aberto do aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="9a139-105">Learn how toouse Spark **MLlib** toocreate a machine learning application toodo simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="9a139-106">Das bibliotecas aprendizado de máquina internas do Spark, este exemplo usa *classificação* por meio de regressão logística.</span><span class="sxs-lookup"><span data-stu-id="9a139-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="9a139-107">Este exemplo também está disponível como um notebook Jupyter em um cluster do Spark (Linux) que você pode criar no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9a139-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="9a139-108">experiência de notebook Olá permite executar trechos de Python de saudação do bloco de anotações de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="9a139-108">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="9a139-109">tutorial de saudação do toofollow de dentro de um bloco de anotações, criar um Spark cluster e iniciar um bloco de anotações do Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="9a139-109">toofollow hello tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="9a139-110">Em seguida, execute o bloco de anotações de saudação **aprendizado de máquina do Spark - análise preditiva em dados de inspeção de alimentos com MLlib.ipynb** em Olá **Python** pasta.</span><span class="sxs-lookup"><span data-stu-id="9a139-110">Then, run hello notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under hello **Python** folder.</span></span>
>
>

<span data-ttu-id="9a139-111">MLlib é uma biblioteca Spark principal que fornece vários utilitários úteis para tarefas de aprendizado de máquina, incluindo utilitários adequados para:</span><span class="sxs-lookup"><span data-stu-id="9a139-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="9a139-112">classificação</span><span class="sxs-lookup"><span data-stu-id="9a139-112">Classification</span></span>
* <span data-ttu-id="9a139-113">Regressão</span><span class="sxs-lookup"><span data-stu-id="9a139-113">Regression</span></span>
* <span data-ttu-id="9a139-114">Clustering</span><span class="sxs-lookup"><span data-stu-id="9a139-114">Clustering</span></span>
* <span data-ttu-id="9a139-115">Modelagem de tópico</span><span class="sxs-lookup"><span data-stu-id="9a139-115">Topic modeling</span></span>
* <span data-ttu-id="9a139-116">Decomposição de valor singular (SVD) e análise de componente principal (PCA)</span><span class="sxs-lookup"><span data-stu-id="9a139-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="9a139-117">Teste de hipótese e cálculo de estatísticas de exemplo</span><span class="sxs-lookup"><span data-stu-id="9a139-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="9a139-118">O que são a classificação e regressão logística?</span><span class="sxs-lookup"><span data-stu-id="9a139-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="9a139-119">*Classificação*, uma tarefa de aprendizado de máquina popular é Olá o processo de classificação de dados de entrada em categorias.</span><span class="sxs-lookup"><span data-stu-id="9a139-119">*Classification*, a popular machine learning task, is hello process of sorting input data into categories.</span></span> <span data-ttu-id="9a139-120">É Olá trabalho de um toofigure de algoritmo de classificação como tooassign "rótulos" tooinput dados que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="9a139-120">It is hello job of a classification algorithm toofigure out how tooassign "labels" tooinput data that you provide.</span></span> <span data-ttu-id="9a139-121">Por exemplo, você pode pensar em um algoritmo de aprendizado de máquina que aceita informações sobre ações como entrada e divide Olá estoque em duas categorias: ações que você deve vender e ações que você deve manter.</span><span class="sxs-lookup"><span data-stu-id="9a139-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides hello stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="9a139-122">Regressão logística é um algoritmo Olá usado para classificação.</span><span class="sxs-lookup"><span data-stu-id="9a139-122">Logistic regression is hello algorithm that you use for classification.</span></span> <span data-ttu-id="9a139-123">A API de regressão logística do Spark é útil para *classificação binária*ou para classificação de dados de entrada em um dos dois grupos.</span><span class="sxs-lookup"><span data-stu-id="9a139-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="9a139-124">Para obter mais informações sobre a regressão logística, consulte [Wikipédia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="9a139-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="9a139-125">Em resumo, o processo de saudação de regressão logística produz um *função logística* que pode ser usado toopredict Olá probabilidade que um vetor de entrada pertence a um grupo ou outros hello.</span><span class="sxs-lookup"><span data-stu-id="9a139-125">In summary, hello process of logistic regression produces a *logistic function* that can be used toopredict hello probability that an input vector belongs in one group or hello other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="9a139-126">Exemplo de análise preditiva em dados de inspeção de alimentos</span><span class="sxs-lookup"><span data-stu-id="9a139-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="9a139-127">Neste exemplo, você usar a Spark tooperform alguma análise preditiva em dados de inspeção de alimentos (**Food_Inspections1.csv**) que foi adquirido por meio de saudação [portal de dados da cidade de Chicago](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="9a139-127">In this example, you use Spark tooperform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through hello [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="9a139-128">Este conjunto de dados contém informações sobre inspeções de estabelecimento de alimentos foram realizados em Chicago, incluindo informações sobre cada estabelecimento, violações de saudação encontrados (se houver) e Olá resultados de inspeção de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a139-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, hello violations found (if any), and hello results of hello inspection.</span></span> <span data-ttu-id="9a139-129">arquivo de dados CSV Olá já está disponível na conta de armazenamento Olá associada Olá cluster em **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="9a139-129">hello CSV data file is already available in hello storage account associated with hello cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="9a139-130">Nas etapas de saudação abaixo, desenvolver um modelo toosee que é necessário toopass ou falhar uma inspeção de alimentos.</span><span class="sxs-lookup"><span data-stu-id="9a139-130">In hello steps below, you develop a model toosee what it takes toopass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="9a139-131">Comece a criar um aplicativo de aprendizado de máquina MMLib do Spark</span><span class="sxs-lookup"><span data-stu-id="9a139-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="9a139-132">De saudação [portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial).</span><span class="sxs-lookup"><span data-stu-id="9a139-132">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="9a139-133">Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9a139-133">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="9a139-134">Na folha de cluster do Spark hello, clique em **painel Cluster**e, em seguida, clique em **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="9a139-134">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="9a139-135">Se solicitado, insira as credenciais de administrador de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9a139-135">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9a139-136">Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="9a139-136">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="9a139-137">Substituir **CLUSTERNAME** com nome de saudação do cluster:</span><span class="sxs-lookup"><span data-stu-id="9a139-137">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="9a139-138">Crie um notebook.</span><span class="sxs-lookup"><span data-stu-id="9a139-138">Create a notebook.</span></span> <span data-ttu-id="9a139-139">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="9a139-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="9a139-140">![Criar um bloco de anotações do Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Criar um novo bloco de anotações do Jupyter")</span><span class="sxs-lookup"><span data-stu-id="9a139-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="9a139-141">Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="9a139-141">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="9a139-142">Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="9a139-142">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="9a139-143">![Forneça um nome para o bloco de anotações de saudação](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "forneça um nome para o bloco de anotações de saudação")</span><span class="sxs-lookup"><span data-stu-id="9a139-143">![Provide a name for hello notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for hello notebook")</span></span>
1. <span data-ttu-id="9a139-144">Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente.</span><span class="sxs-lookup"><span data-stu-id="9a139-144">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="9a139-145">Olá Spark e Hive contextos são criados automaticamente para você quando você executar a primeira célula de código hello.</span><span class="sxs-lookup"><span data-stu-id="9a139-145">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="9a139-146">Você pode começar a criar seu aplicativo de aprendizado importando tipos de saudação necessários para este cenário de máquina.</span><span class="sxs-lookup"><span data-stu-id="9a139-146">You can start building your machine learning application by importing hello types required for this scenario.</span></span> <span data-ttu-id="9a139-147">toodo, portanto, coloque o cursor de saudação na célula hello e pressione **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="9a139-147">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="9a139-148">Construir um dataframe de entrada</span><span class="sxs-lookup"><span data-stu-id="9a139-148">Construct an input dataframe</span></span>
<span data-ttu-id="9a139-149">Podemos usar `sqlContext` tooperform transformações em dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="9a139-149">We can use `sqlContext` tooperform transformations on structured data.</span></span> <span data-ttu-id="9a139-150">Olá primeira tarefa é dados de exemplo hello tooload ((**Food_Inspections1.csv**)) em um Spark SQL *dataframe*.</span><span class="sxs-lookup"><span data-stu-id="9a139-150">hello first task is tooload hello sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="9a139-151">Como dados brutos hello estão em um formato CSV, é preciso toouse Olá Spark contexto toopull cada linha do arquivo de saudação na memória como texto não estruturado; em seguida, você use tooparse de biblioteca CSV do Python cada linha individualmente.</span><span class="sxs-lookup"><span data-stu-id="9a139-151">Because hello raw data is in a CSV format, we need toouse hello Spark context toopull every line of hello file into memory as unstructured text; then, you use Python's CSV library tooparse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="9a139-152">Agora temos arquivo CSV de saudação como um RDD.</span><span class="sxs-lookup"><span data-stu-id="9a139-152">We now have hello CSV file as an RDD.</span></span>  <span data-ttu-id="9a139-153">esquema de Olá toounderstand de dados hello, recuperamos uma linha de saudação RDD.</span><span class="sxs-lookup"><span data-stu-id="9a139-153">toounderstand hello schema of hello data, we retrieve one row from hello RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="9a139-154">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a139-154">You should see an output like hello following:</span></span>

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
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="9a139-155">Olá saída anterior nos dá uma ideia do esquema de saudação do arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="9a139-155">hello preceding output gives us an idea of hello schema of hello input file.</span></span> <span data-ttu-id="9a139-156">Ele inclui o nome de saudação do cada estabelecimento, o tipo de saudação do estabelecimento, endereço hello, dados de saudação do inspeções hello e localização Olá, entre outras coisas.</span><span class="sxs-lookup"><span data-stu-id="9a139-156">It includes hello name of every establishment, hello type of establishment, hello address, hello data of hello inspections, and hello location, among other things.</span></span> <span data-ttu-id="9a139-157">Vamos selecionar algumas colunas que são úteis para nosso análise de previsão e agrupar resultados de saudação como um dataframe, quais nós e usam toocreate uma tabela temporária.</span><span class="sxs-lookup"><span data-stu-id="9a139-157">Let's select a few columns that are useful for our predictive analysis and group hello results as a dataframe, which we then use toocreate a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="9a139-158">Agora temos um *dataframe*, `df` no qual podemos executar nossa análise.</span><span class="sxs-lookup"><span data-stu-id="9a139-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="9a139-159">Também temos uma chamada de tabela temporária **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="9a139-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="9a139-160">Há quatro colunas de interesse em Olá dataframe: **id**, **nome**, **resultados**, e **violações**.</span><span class="sxs-lookup"><span data-stu-id="9a139-160">We've included four columns of interest in hello dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="9a139-161">Vamos uma pequena amostra dos dados hello:</span><span class="sxs-lookup"><span data-stu-id="9a139-161">Let's get a small sample of hello data:</span></span>

        df.show(5)

    <span data-ttu-id="9a139-162">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a139-162">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a><span data-ttu-id="9a139-163">Compreender os dados de saudação</span><span class="sxs-lookup"><span data-stu-id="9a139-163">Understand hello data</span></span>
1. <span data-ttu-id="9a139-164">Vamos começar tooget uma ideia do que contém o nosso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="9a139-164">Let's start tooget a sense of what our dataset contains.</span></span> <span data-ttu-id="9a139-165">Por exemplo, quais são os diferentes valores Olá Olá **resultados** coluna?</span><span class="sxs-lookup"><span data-stu-id="9a139-165">For example, what are hello different values in hello **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="9a139-166">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a139-166">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="9a139-167">Uma visualização rápida pode nos ajudar a raciocinar sobre a distribuição de saudação desses resultados.</span><span class="sxs-lookup"><span data-stu-id="9a139-167">A quick visualization can help us reason about hello distribution of these outcomes.</span></span> <span data-ttu-id="9a139-168">Já temos dados saudação em uma tabela temporária **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="9a139-168">We already have hello data in a temporary table **CountResults**.</span></span> <span data-ttu-id="9a139-169">Você pode executar Olá Olá tabela tooget consulta SQL a seguir uma melhor compreensão de como os resultados de saudação são distribuídos.</span><span class="sxs-lookup"><span data-stu-id="9a139-169">You can run hello following SQL query against hello table tooget a better understanding of how hello results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="9a139-170">Olá `%%sql` mágico seguido `-o countResultsdf` garante que saída Olá de consulta de saudação é persistentes localmente no servidor de Jupyter de saudação (normalmente Olá nó principal do cluster Olá).</span><span class="sxs-lookup"><span data-stu-id="9a139-170">hello `%%sql` magic followed by `-o countResultsdf` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="9a139-171">saída de Hello é mantida como um [Pandas](http://pandas.pydata.org/) dataframe com hello especificado nome **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="9a139-171">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **countResultsdf**.</span></span>

    <span data-ttu-id="9a139-172">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a139-172">You should see an output like hello following:</span></span>

    <span data-ttu-id="9a139-173">![Saída da consulta SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Saída da consulta SQL")</span><span class="sxs-lookup"><span data-stu-id="9a139-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="9a139-174">Para obter mais informações sobre Olá `%%sql` mágico e outros magics disponíveis com o kernel do PySpark hello, consulte [Kernels disponíveis em blocos de anotações do Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="9a139-174">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="9a139-175">Você também pode usar Matplotlib, uma biblioteca usada tooconstruct visualização de dados, toocreate um gráfico.</span><span class="sxs-lookup"><span data-stu-id="9a139-175">You can also use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="9a139-176">Porque plotagem Olá deve ser criada de saudação localmente persistente **countResultsdf** dataframe, o trecho de código Olá deve começar com hello `%%local` mágica.</span><span class="sxs-lookup"><span data-stu-id="9a139-176">Because hello plot must be created from hello locally persisted **countResultsdf** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="9a139-177">Isso garante que o código de Olá é executado localmente no servidor do Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="9a139-177">This ensures that hello code is run locally on hello Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="9a139-178">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a139-178">You should see an output like hello following:</span></span>

    <span data-ttu-id="9a139-179">![Saída do aplicativo de aprendizado de máquina do Spark – gráfico de pizza com cinco conjuntos de resultados de inspeção distintos](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Saída do resultado de aprendizado de máquina de Spark")</span><span class="sxs-lookup"><span data-stu-id="9a139-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="9a139-180">Você pode ver que uma inspeção pode ter cinco resultados distintos:</span><span class="sxs-lookup"><span data-stu-id="9a139-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="9a139-181">Negócios não localizados</span><span class="sxs-lookup"><span data-stu-id="9a139-181">Business not located</span></span>
   * <span data-ttu-id="9a139-182">Reprovado</span><span class="sxs-lookup"><span data-stu-id="9a139-182">Fail</span></span>
   * <span data-ttu-id="9a139-183">Aprovado</span><span class="sxs-lookup"><span data-stu-id="9a139-183">Pass</span></span>
   * <span data-ttu-id="9a139-184">Aprovar c/ condições</span><span class="sxs-lookup"><span data-stu-id="9a139-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="9a139-185">Fora de negócio</span><span class="sxs-lookup"><span data-stu-id="9a139-185">Out of Business</span></span>

     <span data-ttu-id="9a139-186">Vamos desenvolva um modelo que pode adivinhar o resultado de saudação de uma inspeção de alimentos, violações de saudação determinado.</span><span class="sxs-lookup"><span data-stu-id="9a139-186">Let us develop a model that can guess hello outcome of a food inspection, given hello violations.</span></span> <span data-ttu-id="9a139-187">Como a regressão logística é um método de classificação binária, faz sentido toogroup nossos dados em duas categorias: **falha** e **passar**.</span><span class="sxs-lookup"><span data-stu-id="9a139-187">Since logistic regression is a binary classification method, it makes sense toogroup our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="9a139-188">Um "passar com condições de" ainda é uma passagem, portanto quando treinamos modelo hello, consideramos Olá dois resultados equivalente.</span><span class="sxs-lookup"><span data-stu-id="9a139-188">A "Pass w/ Conditions" is still a Pass, so when we train hello model, we consider hello two results equivalent.</span></span> <span data-ttu-id="9a139-189">Dados com hello outros resultados ("Business não localizada" ou "de negócios") não são úteis para removemos do nosso conjunto de treinamento.</span><span class="sxs-lookup"><span data-stu-id="9a139-189">Data with hello other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="9a139-190">Isso deve ser okey porque essas duas categorias compõem uma porcentagem muito pequena de resultados Olá mesmo assim.</span><span class="sxs-lookup"><span data-stu-id="9a139-190">This should be okay since these two categories make up a very small percentage of hello results anyway.</span></span>
1. <span data-ttu-id="9a139-191">Vamos prosseguir e converter nosso dataframe existente (`df`) em um novo dataframe em que cada inspeção é representada como um par de violações de rótulo.</span><span class="sxs-lookup"><span data-stu-id="9a139-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="9a139-192">No nosso caso, um rótulo de `0.0` representa uma falha, um rótulo de `1.0` representa um sucesso e um rótulo de `-1.0` representa alguns resultados diferentes desses dois.</span><span class="sxs-lookup"><span data-stu-id="9a139-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="9a139-193">Vamos filtrar esses outros resultados ao calcular o novo quadro de dados hello.</span><span class="sxs-lookup"><span data-stu-id="9a139-193">We filter those other results out when computing hello new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="9a139-194">toosee quais Olá rotulada dados parece, vamos recuperar uma linha.</span><span class="sxs-lookup"><span data-stu-id="9a139-194">toosee what hello labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="9a139-195">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a139-195">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a><span data-ttu-id="9a139-196">Criar um modelo de regressão logística de dataframe de entrada hello</span><span class="sxs-lookup"><span data-stu-id="9a139-196">Create a logistic regression model from hello input dataframe</span></span>
<span data-ttu-id="9a139-197">Nossa tarefa final é tooconvert Olá rotulada dados em um formato que pode ser analisado por regressão logística.</span><span class="sxs-lookup"><span data-stu-id="9a139-197">Our final task is tooconvert hello labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="9a139-198">algoritmo de regressão logística Olá tooa entrada deve ser um conjunto de *pares de vetor de recurso de rótulo*, onde hello "vetor de recurso" é um vetor de números que representam o ponto de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="9a139-198">hello input tooa logistic regression algorithm should be a set of *label-feature vector pairs*, where hello "feature vector" is a vector of numbers representing hello input point.</span></span> <span data-ttu-id="9a139-199">Portanto, é preciso tooconvert a coluna de violações"hello", o que é semi-estruturados e contém muitos comentários na matriz de tooan texto livre de números reais que uma máquina facilmente compreensível.</span><span class="sxs-lookup"><span data-stu-id="9a139-199">So, we need tooconvert hello "violations" column, which is semi-structured and contains many comments in free-text, tooan array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="9a139-200">Uma abordagem de aprendizado de máquina padrão para o idioma natural de processamento é tooassign cada palavra distinct "index" e, em seguida, passar uma algoritmo de aprendizagem, de modo que o valor de cada índice contém frequência relativa de saudação da palavra em texto de saudação de máquina do vetor toohello cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9a139-200">One standard machine learning approach for processing natural language is tooassign each distinct word an "index", and then pass a vector toohello machine learning algorithm such that each index's value contains hello relative frequency of that word in hello text string.</span></span>

<span data-ttu-id="9a139-201">MLlib fornece uma maneira fácil tooperform esta operação.</span><span class="sxs-lookup"><span data-stu-id="9a139-201">MLlib provides an easy way tooperform this operation.</span></span> <span data-ttu-id="9a139-202">Primeiro, "transformar" cada violações cadeia de caracteres tooget Olá palavras individuais em cada cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="9a139-202">First, "tokenize" each violations string tooget hello individual words in each string.</span></span> <span data-ttu-id="9a139-203">Em seguida, use um `HashingTF` tooconvert cada conjunto de tokens em um vetor de recurso que pode ser passado toohello tooconstruct de algoritmo de regressão logística de um modelo.</span><span class="sxs-lookup"><span data-stu-id="9a139-203">Then, use a `HashingTF` tooconvert each set of tokens into a feature vector that can then be passed toohello logistic regression algorithm tooconstruct a model.</span></span> <span data-ttu-id="9a139-204">Realizamos todas essas etapas em sequência, usando um "pipeline".</span><span class="sxs-lookup"><span data-stu-id="9a139-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a><span data-ttu-id="9a139-205">Avaliar modelo Olá em um conjunto de dados de teste separada</span><span class="sxs-lookup"><span data-stu-id="9a139-205">Evaluate hello model on a separate test dataset</span></span>
<span data-ttu-id="9a139-206">Podemos usar o modelo de saudação que criamos anteriormente muito*prever* quais Olá resultados da nova inspeções serão, com base em violações de saudação que foram observadas.</span><span class="sxs-lookup"><span data-stu-id="9a139-206">We can use hello model we created earlier too*predict* what hello results of new inspections will be, based on hello violations that were observed.</span></span> <span data-ttu-id="9a139-207">Esse modelo no conjunto de dados de saudação é treinado **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="9a139-207">We trained this model on hello dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="9a139-208">Vamos usar um segundo conjunto de dados, **Food_Inspections2.csv**, muito*avaliar* Olá intensidade desse modelo em dados novos.</span><span class="sxs-lookup"><span data-stu-id="9a139-208">Let us use a second dataset, **Food_Inspections2.csv**, too*evaluate* hello strength of this model on new data.</span></span> <span data-ttu-id="9a139-209">Esse segundo conjunto de dados (**Food_Inspections2.csv**) já deve estar no contêiner de armazenamento padrão de Olá associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="9a139-209">This second data set (**Food_Inspections2.csv**) should already be in hello default storage container associated with hello cluster.</span></span>

1. <span data-ttu-id="9a139-210">Olá, trecho a seguir cria um novo dataframe, **predictionsDf** que contém a previsão Olá gerado pelo modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a139-210">hello following snippet creates a new dataframe, **predictionsDf** that contains hello prediction generated by hello model.</span></span> <span data-ttu-id="9a139-211">trecho de saudação também cria uma tabela temporária chamada **previsões** com base em dataframe de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a139-211">hello snippet also creates a temporary table called **Predictions** based on hello dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="9a139-212">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a139-212">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="9a139-213">Examinar uma das previsões de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a139-213">Look at one of hello predictions.</span></span> <span data-ttu-id="9a139-214">Execute este trecho de código:</span><span class="sxs-lookup"><span data-stu-id="9a139-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="9a139-215">Há uma previsão para a primeira entrada hello no conjunto de dados de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a139-215">There is a prediction for hello first entry in hello test data set.</span></span>
1. <span data-ttu-id="9a139-216">Olá `model.transform()` método se aplica a saudação mesmo transformação tooany novos dados com hello mesmo esquema e chegar a uma previsão de como tooclassify Olá dados.</span><span class="sxs-lookup"><span data-stu-id="9a139-216">hello `model.transform()` method applies hello same transformation tooany new data with hello same schema, and arrive at a prediction of how tooclassify hello data.</span></span> <span data-ttu-id="9a139-217">Podemos fazer algumas estatísticas simples tooget uma noção da nossas previsões como precisas foram:</span><span class="sxs-lookup"><span data-stu-id="9a139-217">We can do some simple statistics tooget a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="9a139-218">saída de Hello semelhante ao seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9a139-218">hello output looks like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="9a139-219">Usando Regressão logística com Spark fornece um modelo preciso da relação de saudação entre descrições de violações em inglês e se um negócio deve passar ou falhar uma inspeção de alimentos.</span><span class="sxs-lookup"><span data-stu-id="9a139-219">Using logistic regression with Spark gives us an accurate model of hello relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-hello-prediction"></a><span data-ttu-id="9a139-220">Criar uma representação visual de previsão Olá</span><span class="sxs-lookup"><span data-stu-id="9a139-220">Create a visual representation of hello prediction</span></span>
<span data-ttu-id="9a139-221">Agora podemos construir um toohelp final visualização que nos argumentar sobre resultados de saudação desse teste.</span><span class="sxs-lookup"><span data-stu-id="9a139-221">We can now construct a final visualization toohelp us reason about hello results of this test.</span></span>

1. <span data-ttu-id="9a139-222">Vamos começar por meio da extração previsões diferentes hello e resultados de Olá **previsões** tabela temporária criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9a139-222">We start by extracting hello different predictions and results from hello **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="9a139-223">consultas a seguir Hello separam saída hello como *true_positive*, *false_positive*, *true_negative*, e *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="9a139-223">hello following queries separate hello output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="9a139-224">Em consultas de saudação abaixo, podemos desativar visualização usando `-q` e também salvar a saída de hello (usando `-o`) como quadros de dados que podem ser usados com hello `%%local` mágica.</span><span class="sxs-lookup"><span data-stu-id="9a139-224">In hello queries below, we turn off visualization by using `-q` and also save hello output (by using `-o`) as dataframes that can be then used with hello `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="9a139-225">Por fim, use Olá seguindo o trecho de código toogenerate Olá plotagem usando **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="9a139-225">Finally, use hello following snippet toogenerate hello plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="9a139-226">Você deve ver Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a139-226">You should see hello following output:</span></span>

    <span data-ttu-id="9a139-227">![Saída do aplicativo de aprendizado de máquina do Spark – percentuais de gráfico de pizza de inspeções em alimentos com falha.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Saída do resultado de aprendizado de máquina do Spark")</span><span class="sxs-lookup"><span data-stu-id="9a139-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="9a139-228">Neste gráfico, um resultado "positivo" refere-se inspeção de alimentos toohello falhado, enquanto um resultado negativo refere-se tooa passado inspeção.</span><span class="sxs-lookup"><span data-stu-id="9a139-228">In this chart, a "positive" result refers toohello failed food inspection, while a negative result refers tooa passed inspection.</span></span>

## <a name="shut-down-hello-notebook"></a><span data-ttu-id="9a139-229">Fechar o bloco de anotações de saudação</span><span class="sxs-lookup"><span data-stu-id="9a139-229">Shut down hello notebook</span></span>
<span data-ttu-id="9a139-230">Depois de terminar de executar o aplicativo hello, você deve desligar recursos de Olá Olá notebook toorelease.</span><span class="sxs-lookup"><span data-stu-id="9a139-230">After you have finished running hello application, you should shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="9a139-231">toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**.</span><span class="sxs-lookup"><span data-stu-id="9a139-231">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="9a139-232">Isso é desligado e fecha Olá notebook.</span><span class="sxs-lookup"><span data-stu-id="9a139-232">This shuts down and closes hello notebook.</span></span>

## <span data-ttu-id="9a139-233"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="9a139-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="9a139-234">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a139-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="9a139-235">Cenários</span><span class="sxs-lookup"><span data-stu-id="9a139-235">Scenarios</span></span>
* [<span data-ttu-id="9a139-236">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="9a139-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* <span data-ttu-id="9a139-237">
            [Spark com Machine Learning: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)</span><span class="sxs-lookup"><span data-stu-id="9a139-237">[Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data](hdinsight-apache-spark-ipython-notebook-machine-learning.md)</span></span>
* [<span data-ttu-id="9a139-238">Streaming Spark: use o Spark no HDInsight para a criação de aplicativos streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="9a139-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="9a139-239">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a139-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="9a139-240">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="9a139-240">Create and run applications</span></span>
* [<span data-ttu-id="9a139-241">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="9a139-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9a139-242">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="9a139-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="9a139-243">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="9a139-243">Tools and extensions</span></span>
* [<span data-ttu-id="9a139-244">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="9a139-244">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9a139-245">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="9a139-245">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="9a139-246">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a139-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="9a139-247">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a139-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9a139-248">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="9a139-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9a139-249">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="9a139-249">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="9a139-250">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="9a139-250">Manage resources</span></span>
* [<span data-ttu-id="9a139-251">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="9a139-251">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="9a139-252">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a139-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
