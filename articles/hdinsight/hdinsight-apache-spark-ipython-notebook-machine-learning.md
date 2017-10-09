---
title: "aplicativos no Azure HDInsight de aprendizado de máquina de Apache Spark de aaaBuild | Microsoft Docs"
description: "Instruções passo a passo sobre como o aplicativo no HDInsight Spark de aprendizado de máquina do toobuild Apache Spark clusters usando anotações do Jupyter"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="eede5-103">Criar aplicativos de aprendizado de máquina do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="eede5-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="eede5-104">Saiba como toobuild um aplicativo de aprendizado de máquina do Apache Spark usando um Spark cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eede5-104">Learn how toobuild an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="eede5-105">Este artigo mostra como toouse Olá anotações do Jupyter com hello cluster toobuild e testar esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eede5-105">This article shows how toouse hello Jupyter notebook available with hello cluster toobuild and test this application.</span></span> <span data-ttu-id="eede5-106">aplicativo Hello usa dados de HVAC.csv do exemplo hello estão disponíveis em todos os clusters por padrão.</span><span class="sxs-lookup"><span data-stu-id="eede5-106">hello application uses hello sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="eede5-107">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="eede5-107">**Prerequisites:**</span></span>

<span data-ttu-id="eede5-108">Você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="eede5-108">You must have hello following:</span></span>

* <span data-ttu-id="eede5-109">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eede5-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="eede5-110">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="eede5-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="eede5-111"><a name="data"></a>Entender o conjunto de dados Olá</span><span class="sxs-lookup"><span data-stu-id="eede5-111"><a name="data"></a>Understand hello data set</span></span>
<span data-ttu-id="eede5-112">Antes de começar criando um aplicativo hello, vamos entenda a estrutura de saudação de dados Olá para que criamos aplicativo hello e tipo de saudação de análise que faremos nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="eede5-112">Before we start building hello application, let us understand hello structure of hello data for which we build hello application and hello kind of analysis we will do on hello data.</span></span> 

<span data-ttu-id="eede5-113">Neste artigo, podemos usar o exemplo hello **HVAC.csv** arquivo de dados que está disponível no hello conta de armazenamento do Azure que você associou com cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="eede5-113">In this article, we use hello sample **HVAC.csv** data file that is available in hello Azure Storage account that you associated with hello HDInsight cluster.</span></span> <span data-ttu-id="eede5-114">Na conta de armazenamento hello, arquivo hello está no **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="eede5-114">Within hello storage account, hello file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="eede5-115">Baixe e abra Olá CSV arquivo tooget um instantâneo dos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="eede5-115">Download and open hello CSV file tooget a snapshot of hello data.</span></span>  

<span data-ttu-id="eede5-116">![Exemplo de instantâneo dos dados usados para aprendizado de máquina do Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Exemplo de instantâneo dos dados usados para aprendizado de máquina do Spark")</span><span class="sxs-lookup"><span data-stu-id="eede5-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="eede5-117">dados saudação mostram a temperatura do destino hello e temperatura real de saudação do prédio com sistemas de ar Condicionado instalados.</span><span class="sxs-lookup"><span data-stu-id="eede5-117">hello data shows hello target temperature and hello actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="eede5-118">Vamos supor que Olá **sistema** coluna representa a ID de sistema hello e hello **SystemAge** coluna representa o número de saudação de sistema HVAC Olá foi em vigor na construção de saudação de anos.</span><span class="sxs-lookup"><span data-stu-id="eede5-118">Let's assume hello **System** column represents hello system ID and hello **SystemAge** column represents hello number of years hello HVAC system has been in place at hello building.</span></span>

<span data-ttu-id="eede5-119">Usamos este toopredict de dados se um edifício serão mais quentes ou colder com base em temperatura de destino hello, recebe uma ID de sistema e a idade do sistema.</span><span class="sxs-lookup"><span data-stu-id="eede5-119">We use this data toopredict whether a building will be hotter or colder based on hello target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="eede5-120"><a name="app"></a>Escrever um aplicativo de aprendizado de máquina do Spark usando o MLlib Spark</span><span class="sxs-lookup"><span data-stu-id="eede5-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="eede5-121">Neste aplicativo, usamos um pipeline de Spark ML tooperform uma classificação de documento.</span><span class="sxs-lookup"><span data-stu-id="eede5-121">In this application we use a Spark ML pipeline tooperform a document classification.</span></span> <span data-ttu-id="eede5-122">No pipeline de saudação é dividir o documento de saudação em palavras, converter palavras Olá em um vetor de recurso numérico e, por fim, criar um modelo de previsão usando rótulos e vetores de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="eede5-122">In hello pipeline, we split hello document into words, convert hello words into a numerical feature vector, and finally build a prediction model using hello feature vectors and labels.</span></span> <span data-ttu-id="eede5-123">Execute Olá aplicativo de hello toocreate as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="eede5-123">Perform hello following steps toocreate hello application.</span></span>

1. <span data-ttu-id="eede5-124">De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial).</span><span class="sxs-lookup"><span data-stu-id="eede5-124">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="eede5-125">Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="eede5-125">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="eede5-126">Na folha de cluster do Spark hello, clique em **painel Cluster**e, em seguida, clique em **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="eede5-126">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="eede5-127">Se solicitado, insira as credenciais de administrador de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="eede5-127">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="eede5-128">Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="eede5-128">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="eede5-129">Substituir **CLUSTERNAME** com nome de saudação do cluster:</span><span class="sxs-lookup"><span data-stu-id="eede5-129">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="eede5-130">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="eede5-130">Create a new notebook.</span></span> <span data-ttu-id="eede5-131">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="eede5-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="eede5-132">![Criar um exemplo de bloco de anotações do Jupyter para aprendizado de máquina do Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Criar um exemplo de bloco de anotações do Jupyter para aprendizado de máquina Spark")</span><span class="sxs-lookup"><span data-stu-id="eede5-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="eede5-133">Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="eede5-133">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="eede5-134">Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="eede5-134">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="eede5-135">![Fornecer um exemplo de nome de bloco de anotações do Jupyter para aprendizado de máquina Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Fornecer um exemplo de nome de bloco de anotações do Jupyter para aprendizado de máquina Spark")</span><span class="sxs-lookup"><span data-stu-id="eede5-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="eede5-136">Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente.</span><span class="sxs-lookup"><span data-stu-id="eede5-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="eede5-137">contextos de Spark e Hive Olá serão automaticamente criados para você quando você executar a primeira célula de código hello.</span><span class="sxs-lookup"><span data-stu-id="eede5-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="eede5-138">Você pode começar importando tipos Olá que são necessários para este cenário.</span><span class="sxs-lookup"><span data-stu-id="eede5-138">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="eede5-139">Cole Olá seguindo o trecho de código em uma célula vazia e, em seguida, pressione **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="eede5-139">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. <span data-ttu-id="eede5-140">Você agora deve carregar dados de saudação (hvac.csv), analisá-lo e usá-lo tootrain modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="eede5-140">You must now load hello data (hvac.csv), parse it, and use it tootrain hello model.</span></span> <span data-ttu-id="eede5-141">Para isso, você define uma função que verifica se a temperatura real Olá da criação de saudação do é maior do que a temperatura do destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="eede5-141">For this, you define a function that checks whether hello actual temperature of hello building is greater than hello target temperature.</span></span> <span data-ttu-id="eede5-142">Se a temperatura real Olá for maior, a construção de saudação é ativa, indicado pelo valor Olá **1.0**.</span><span class="sxs-lookup"><span data-stu-id="eede5-142">If hello actual temperature is greater, hello building is hot, denoted by hello value **1.0**.</span></span> <span data-ttu-id="eede5-143">Se a temperatura real Olá é menor, construção Olá fria, é indicado pelo valor de saudação **0,0**.</span><span class="sxs-lookup"><span data-stu-id="eede5-143">If hello actual temperature is lesser, hello building is cold, denoted by hello value **0.0**.</span></span> 
   
    <span data-ttu-id="eede5-144">Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="eede5-144">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="eede5-145">Configurar o pipeline de aprendizado de máquina do Spark Olá que consiste em três estágios: lr, hashingTF e tokenizer.</span><span class="sxs-lookup"><span data-stu-id="eede5-145">Configure hello Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="eede5-146">Para obter mais informações sobre o que é um pipeline e como ele funciona, confira <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Pipeline de aprendizado de máquina Spark</a>.</span><span class="sxs-lookup"><span data-stu-id="eede5-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="eede5-147">Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="eede5-147">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="eede5-148">Ajustar o documento de treinamento de toohello Olá pipeline.</span><span class="sxs-lookup"><span data-stu-id="eede5-148">Fit hello pipeline toohello training document.</span></span> <span data-ttu-id="eede5-149">Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="eede5-149">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="eede5-150">Verifique se Olá treinamento documento toocheckpoint seu progresso com o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="eede5-150">Verify hello training document toocheckpoint your progress with hello application.</span></span> <span data-ttu-id="eede5-151">Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="eede5-151">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="eede5-152">Isso deve dar a seguir Olá saída semelhante toohello:</span><span class="sxs-lookup"><span data-stu-id="eede5-152">This should give hello output similar toohello following:</span></span>
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    <span data-ttu-id="eede5-153">Voltar e verifique se a saída de hello no arquivo CSV bruto de saudação.</span><span class="sxs-lookup"><span data-stu-id="eede5-153">Go back and verify hello output against hello raw CSV file.</span></span> <span data-ttu-id="eede5-154">Por exemplo, arquivo CSV para Olá primeira linha hello tem esses dados:</span><span class="sxs-lookup"><span data-stu-id="eede5-154">For example, hello first row hello CSV file has this data:</span></span>

    <span data-ttu-id="eede5-155">![Exemplo de instantâneo dos dados de saída para aprendizado de máquina do Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Exemplo de instantâneo dos dados de saída para aprendizado de máquina do Spark")</span><span class="sxs-lookup"><span data-stu-id="eede5-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="eede5-156">Observe como a temperatura real Olá é menor do que a temperatura do destino Olá sugerindo construção hello está frio.</span><span class="sxs-lookup"><span data-stu-id="eede5-156">Notice how hello actual temperature is less than hello target temperature suggesting hello building is cold.</span></span> <span data-ttu-id="eede5-157">Portanto, na saída de treinamento hello, Olá valor para **rótulo** Olá primeira linha é **0,0**, que significa construção Olá não está ativa.</span><span class="sxs-lookup"><span data-stu-id="eede5-157">Hence in hello training output, hello value for **label** in hello first row is **0.0**, which means hello building is not hot.</span></span>

1. <span data-ttu-id="eede5-158">Prepare um conjunto de dados toorun Olá treinado em.</span><span class="sxs-lookup"><span data-stu-id="eede5-158">Prepare a data set toorun hello trained model against.</span></span> <span data-ttu-id="eede5-159">toodo assim, passar em uma ID de sistema e a idade do sistema (denotado como **SystemInfo** na saída de treinamento Olá), e Olá modelo seria prever se Olá compilando com idade de ID e do sistema que sistema poderiam ser mais quentes (indicado por 1.0) ou mais ( indicado pela 0.0).</span><span class="sxs-lookup"><span data-stu-id="eede5-159">toodo so, we would pass on a system ID and system age (denoted as **SystemInfo** in hello training output), and hello model would predict whether hello building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="eede5-160">Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="eede5-160">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="eede5-161">Por fim, fazer previsões sobre os dados de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="eede5-161">Finally, make predictions on hello test data.</span></span> <span data-ttu-id="eede5-162">Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="eede5-162">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="eede5-163">Você verá uma saída semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="eede5-163">You should see an output similar toohello following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="eede5-164">A primeira linha na previsão Olá Olá, você pode ver que para um sistema HVAC com ID 20 e o sistema de 25 anos, construção hello serão mais acessada (**previsão = 1.0**).</span><span class="sxs-lookup"><span data-stu-id="eede5-164">From hello first row in hello prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, hello building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="eede5-165">primeiro valor Olá para DenseVector (0.49999) corresponde toohello previsão 0,0 e valor de segundo hello (0.5001) corresponde a previsão toohello 1.0.</span><span class="sxs-lookup"><span data-stu-id="eede5-165">hello first value for DenseVector (0.49999) corresponds toohello  prediction 0.0 and hello second value (0.5001) corresponds toohello prediction 1.0.</span></span> <span data-ttu-id="eede5-166">Na saída de hello, embora Olá segundo valor só é ligeiramente maior, Olá modelo mostra **previsão = 1.0**.</span><span class="sxs-lookup"><span data-stu-id="eede5-166">In hello output, even though hello second value is only marginally higher, hello model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="eede5-167">Depois de terminar de executar o aplicativo hello, você deverá recursos de saudação do desligamento Olá notebook toorelease.</span><span class="sxs-lookup"><span data-stu-id="eede5-167">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="eede5-168">toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**.</span><span class="sxs-lookup"><span data-stu-id="eede5-168">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="eede5-169">Esta desligará e notebook Olá fechar.</span><span class="sxs-lookup"><span data-stu-id="eede5-169">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="eede5-170"><a name="anaconda"></a>Use a biblioteca Anaconda scikit-learn para aprendizado de máquina do Spark</span><span class="sxs-lookup"><span data-stu-id="eede5-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="eede5-171">Os clusters Apache Spark no HDInsight incluem bibliotecas Anaconda.</span><span class="sxs-lookup"><span data-stu-id="eede5-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="eede5-172">Isso também inclui Olá **scikit-Saiba** biblioteca para o aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="eede5-172">This also includes hello **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="eede5-173">biblioteca de saudação também inclui vários conjuntos de dados que você pode usar os aplicativos de exemplo toobuild diretamente de um bloco de anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="eede5-173">hello library also includes various data sets that you can use toobuild sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="eede5-174">Para exemplos sobre como usar o hello scikit-Saiba biblioteca, consulte [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="eede5-174">For examples on using hello scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="eede5-175"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="eede5-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="eede5-176">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="eede5-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="eede5-177">Cenários</span><span class="sxs-lookup"><span data-stu-id="eede5-177">Scenarios</span></span>
* [<span data-ttu-id="eede5-178">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="eede5-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="eede5-179">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="eede5-179">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="eede5-180">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="eede5-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="eede5-181">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="eede5-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="eede5-182">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="eede5-182">Create and run applications</span></span>
* [<span data-ttu-id="eede5-183">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="eede5-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="eede5-184">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="eede5-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="eede5-185">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="eede5-185">Tools and extensions</span></span>
* [<span data-ttu-id="eede5-186">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar maiores Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="eede5-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="eede5-187">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="eede5-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="eede5-188">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="eede5-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="eede5-189">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="eede5-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="eede5-190">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="eede5-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="eede5-191">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="eede5-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="eede5-192">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="eede5-192">Manage resources</span></span>
* [<span data-ttu-id="eede5-193">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="eede5-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="eede5-194">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="eede5-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
