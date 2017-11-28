---
title: "Criar aplicativos de aprendizado de máquina do Apache Spark no Azure HDInsight | Microsoft Docs"
description: "Instruções passo a passo sobre como criar aplicativos de aprendizado de máquina do Apache Spark em clusters do HDInsight Spark usando o bloco de anotações do Jupyter"
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
ms.openlocfilehash: 158ade4612104020e0231794e7123ea5cad6c459
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="3e3ac-103">Criar aplicativos de aprendizado de máquina do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e3ac-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="3e3ac-104">Aprenda a criar um aplicativo de aprendizado de máquina do Apache Spark usando um cluster do Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-104">Learn how to build an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="3e3ac-105">Este artigo mostra como usar o bloco de anotações do Jupyter disponível com o cluster para criar e testar esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-105">This article shows how to use the Jupyter notebook available with the cluster to build and test this application.</span></span> <span data-ttu-id="3e3ac-106">O aplicativo usa os dados de HVAC.csv de exemplo que estão disponíveis em todos os clusters por padrão.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-106">The application uses the sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="3e3ac-107">**Pré-requisitos:**</span><span class="sxs-lookup"><span data-stu-id="3e3ac-107">**Prerequisites:**</span></span>

<span data-ttu-id="3e3ac-108">Você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3e3ac-108">You must have the following:</span></span>

* <span data-ttu-id="3e3ac-109">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="3e3ac-110">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="3e3ac-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="3e3ac-111"><a name="data"></a>Entender o conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="3e3ac-111"><a name="data"></a>Understand the data set</span></span>
<span data-ttu-id="3e3ac-112">Antes de começarmos a criação do aplicativo, vamos entender a estrutura dos dados para os quais criaremos o aplicativo e o tipo de análise que vamos fazer nos dados.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-112">Before we start building the application, let us understand the structure of the data for which we build the application and the kind of analysis we will do on the data.</span></span> 

<span data-ttu-id="3e3ac-113">Neste artigo, usamos o exemplo arquivo de dados de exemplo **HVAC.csv** que está disponível na conta de Armazenamento do Azure que você associou ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-113">In this article, we use the sample **HVAC.csv** data file that is available in the Azure Storage account that you associated with the HDInsight cluster.</span></span> <span data-ttu-id="3e3ac-114">Na conta de armazenamento, o arquivo está em **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-114">Within the storage account, the file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="3e3ac-115">Baixe e abra o arquivo CSV para obter um instantâneo dos dados.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-115">Download and open the CSV file to get a snapshot of the data.</span></span>  

<span data-ttu-id="3e3ac-116">![Exemplo de instantâneo dos dados usados para aprendizado de máquina do Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Exemplo de instantâneo dos dados usados para aprendizado de máquina do Spark")</span><span class="sxs-lookup"><span data-stu-id="3e3ac-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="3e3ac-117">Os dados mostram a temperatura de destino e a temperatura real de um prédio com sistemas de HVAC instalados.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-117">The data shows the target temperature and the actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="3e3ac-118">Vamos supor que a coluna **System** representa a ID do sistema e a coluna **SystemAge** representa o número de anos que o sistema HVAC foi instalado no prédio.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-118">Let's assume the **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span></span>

<span data-ttu-id="3e3ac-119">Podemos usar esses dados para prever se um prédio será mais quente ou frio com base na temperatura de destino, uma ID de sistema e a idade do sistema.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-119">We use this data to predict whether a building will be hotter or colder based on the target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="3e3ac-120"><a name="app"></a>Escrever um aplicativo de aprendizado de máquina do Spark usando o MLlib Spark</span><span class="sxs-lookup"><span data-stu-id="3e3ac-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="3e3ac-121">Neste aplicativo, usamos um pipeline ML do Spark para executar uma classificação de documento.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-121">In this application we use a Spark ML pipeline to perform a document classification.</span></span> <span data-ttu-id="3e3ac-122">No pipeline, vamos dividir o documento em palavras, converter as palavras em um vetor de recurso numérico e, finalmente, criar um modelo de previsão usando as etiquetas e vetores de recurso.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-122">In the pipeline, we split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span></span> <span data-ttu-id="3e3ac-123">Execute as seguintes etapas para criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-123">Perform the following steps to create the application.</span></span>

1. <span data-ttu-id="3e3ac-124">No [Portal do Azure](https://portal.azure.com/), no quadro inicial, clique no bloco do cluster Spark (se você o tiver fixado no quadro inicial).</span><span class="sxs-lookup"><span data-stu-id="3e3ac-124">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="3e3ac-125">Você também pode navegar até o cluster em **Procurar Tudo** > **Clusters HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-125">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="3e3ac-126">Na folha do cluster Spark, clique em **Painel do Cluster** e em **Notebook Jupyter**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-126">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="3e3ac-127">Se você receber uma solicitação, insira as credenciais de administrador para o cluster.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-127">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3e3ac-128">Você também pode acessar o Bloco de Notas Jupyter de seu cluster abrindo a seguinte URL no navegador.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-128">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="3e3ac-129">Substitua **CLUSTERNAME** pelo nome do cluster:</span><span class="sxs-lookup"><span data-stu-id="3e3ac-129">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="3e3ac-130">Crie um novo bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-130">Create a new notebook.</span></span> <span data-ttu-id="3e3ac-131">Clique em **Novo** e em **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="3e3ac-132">![Criar um exemplo de bloco de anotações do Jupyter para aprendizado de máquina do Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Criar um exemplo de bloco de anotações do Jupyter para aprendizado de máquina Spark")</span><span class="sxs-lookup"><span data-stu-id="3e3ac-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="3e3ac-133">Um novo bloco de anotações é criado e aberto com o nome Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-133">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="3e3ac-134">Clique no nome do bloco de anotações na parte superior e digite um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-134">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="3e3ac-135">![Fornecer um exemplo de nome de bloco de anotações do Jupyter para aprendizado de máquina Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Fornecer um exemplo de nome de bloco de anotações do Jupyter para aprendizado de máquina Spark")</span><span class="sxs-lookup"><span data-stu-id="3e3ac-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="3e3ac-136">Por ter criado um notebook usando o kernel PySpark, não será necessário criar nenhum contexto explicitamente.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="3e3ac-137">Os contextos do Spark e do Hive serão criados automaticamente para você ao executar a primeira célula do código.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="3e3ac-138">Você pode começar importando os tipos que são obrigatórios para este cenário.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-138">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="3e3ac-139">Cole o trecho a seguir em uma célula vazia e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-139">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="3e3ac-140">Agora você deve carregar os dados (hvac.csv), analisá-los e usá-los para treinar o modelo.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-140">You must now load the data (hvac.csv), parse it, and use it to train the model.</span></span> <span data-ttu-id="3e3ac-141">Para isso, você define uma função que verifica se a temperatura real do prédio é maior que a temperatura de destino.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-141">For this, you define a function that checks whether the actual temperature of the building is greater than the target temperature.</span></span> <span data-ttu-id="3e3ac-142">Se a temperatura real é maior, o prédio está quente, indicado pelo valor **1,0**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-142">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span></span> <span data-ttu-id="3e3ac-143">Se a temperatura real é menor, o prédio está frio, indicado pelo valor **0,0**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-143">If the actual temperature is lesser, the building is cold, denoted by the value **0.0**.</span></span> 
   
    <span data-ttu-id="3e3ac-144">Cole o trecho a seguir em uma célula vazia e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-144">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List the structure of data for better understanding. Because the data will be
        # loaded as an array, this structure makes it easy to understand what each element
        # in the array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses the raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load the raw HVAC.csv file, parse it using the function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="3e3ac-145">Configure o pipeline de aprendizado de máquina Spark que consiste de três estágios: tokenizer, hashingTF e lr.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-145">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="3e3ac-146">Para obter mais informações sobre o que é um pipeline e como ele funciona, confira <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Pipeline de aprendizado de máquina Spark</a>.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="3e3ac-147">Cole o trecho a seguir em uma célula vazia e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-147">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="3e3ac-148">Ajuste o pipeline para o documento de treinamento.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-148">Fit the pipeline to the training document.</span></span> <span data-ttu-id="3e3ac-149">Cole o trecho a seguir em uma célula vazia e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-149">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="3e3ac-150">Verifique o documento de treinamento para o ponto de verificação de seu progresso com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-150">Verify the training document to checkpoint your progress with the application.</span></span> <span data-ttu-id="3e3ac-151">Cole o trecho a seguir em uma célula vazia e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-151">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="3e3ac-152">Isso deve fornecer um resultado semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="3e3ac-152">This should give the output similar to the following:</span></span>
   
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

    <span data-ttu-id="3e3ac-153">Volte e verifique se a saída em relação ao arquivo CSV bruto.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-153">Go back and verify the output against the raw CSV file.</span></span> <span data-ttu-id="3e3ac-154">Por exemplo, a primeira linha do arquivo CSV tem esses dados:</span><span class="sxs-lookup"><span data-stu-id="3e3ac-154">For example, the first row the CSV file has this data:</span></span>

    <span data-ttu-id="3e3ac-155">![Exemplo de instantâneo dos dados de saída para aprendizado de máquina do Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Exemplo de instantâneo dos dados de saída para aprendizado de máquina do Spark")</span><span class="sxs-lookup"><span data-stu-id="3e3ac-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="3e3ac-156">Observe como a temperatura real é menor que a temperatura de destino sugerindo que o prédio está frio.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-156">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span></span> <span data-ttu-id="3e3ac-157">Portanto, no resultado do treinamento, o valor para o **rótulo** na primeira linha é **0,0**, o que significa que o prédio não está quente.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-157">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span></span>

1. <span data-ttu-id="3e3ac-158">Prepare um conjunto de dados para executar o modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-158">Prepare a data set to run the trained model against.</span></span> <span data-ttu-id="3e3ac-159">Para fazer isso, passamos uma ID de sistema e a idade do sistema (denotado como **SystemInfo** no resultado de treinamento), e o modelo deve prever se o prédio com essa ID de sistema e idade de sistema seria mais quente (indicado por 1,0) ou mais frio (indicado pelo 0,0).</span><span class="sxs-lookup"><span data-stu-id="3e3ac-159">To do so, we would pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model would predict whether the building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="3e3ac-160">Cole o trecho a seguir em uma célula vazia e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-160">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="3e3ac-161">Por fim, faça as previsões nos dados de teste.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-161">Finally, make predictions on the test data.</span></span> <span data-ttu-id="3e3ac-162">Cole o trecho a seguir em uma célula vazia e pressione **SHIFT+ENTER**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-162">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="3e3ac-163">Você deverá ver um resultado semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="3e3ac-163">You should see an output similar to the following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="3e3ac-164">Na primeira linha na previsão, você pode ver que para um sistema HVAC com ID 20 e sistema de 25 anos, o prédio estará quente (**previsão = 1,0**).</span><span class="sxs-lookup"><span data-stu-id="3e3ac-164">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="3e3ac-165">O primeiro valor de DenseVector (0,49999) corresponde à previsão 0,0 e o segundo valor (0,5001) corresponde à previsão 1,0.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-165">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span></span> <span data-ttu-id="3e3ac-166">Na saída, mesmo que o segundo valor seja apenas um pouco mais alto, o modelo mostra **previsão = 1,0**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-166">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="3e3ac-167">Depois de concluir a execução do aplicativo, você deve encerrar o notebook para liberar os recursos.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-167">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="3e3ac-168">Para isso, no menu **Arquivo** do bloco de anotações, clique em **Fechar e Interromper**.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-168">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="3e3ac-169">Isso desligará e fechará o bloco de anotações.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-169">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="3e3ac-170"><a name="anaconda"></a>Use a biblioteca Anaconda scikit-learn para aprendizado de máquina do Spark</span><span class="sxs-lookup"><span data-stu-id="3e3ac-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="3e3ac-171">Os clusters Apache Spark no HDInsight incluem bibliotecas Anaconda.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="3e3ac-172">Isso também inclui a biblioteca **scikit-learn** para aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-172">This also includes the **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="3e3ac-173">A biblioteca também inclui vários conjuntos de dados que você pode usar para criar aplicativos de exemplo diretamente de um bloco de anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="3e3ac-173">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="3e3ac-174">Para obter exemplos sobre como usar a biblioteca scikit-learn, confira [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span><span class="sxs-lookup"><span data-stu-id="3e3ac-174">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="3e3ac-175"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="3e3ac-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="3e3ac-176">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e3ac-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="3e3ac-177">Cenários</span><span class="sxs-lookup"><span data-stu-id="3e3ac-177">Scenarios</span></span>
* [<span data-ttu-id="3e3ac-178">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="3e3ac-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* <span data-ttu-id="3e3ac-179">
            [Spark com Machine Learning: usar o Spark no HDInsight para prever resultados da inspeção de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)</span><span class="sxs-lookup"><span data-stu-id="3e3ac-179">[Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results](hdinsight-apache-spark-machine-learning-mllib-ipython.md)</span></span>
* [<span data-ttu-id="3e3ac-180">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="3e3ac-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="3e3ac-181">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e3ac-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="3e3ac-182">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="3e3ac-182">Create and run applications</span></span>
* [<span data-ttu-id="3e3ac-183">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="3e3ac-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3e3ac-184">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="3e3ac-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="3e3ac-185">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="3e3ac-185">Tools and extensions</span></span>
* [<span data-ttu-id="3e3ac-186">Usar o plug-in de Ferramentas do HDInsight para IntelliJ IDEA para criar e enviar aplicativos Spark Scala</span><span class="sxs-lookup"><span data-stu-id="3e3ac-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="3e3ac-187">Usar o plug-in de Ferramentas do HDInsight para depurar aplicativos Spark remotamente</span><span class="sxs-lookup"><span data-stu-id="3e3ac-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="3e3ac-188">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e3ac-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="3e3ac-189">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e3ac-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="3e3ac-190">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="3e3ac-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="3e3ac-191">Instalar o Jupyter em seu computador e conectar-se a um cluster Spark do HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e3ac-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="3e3ac-192">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="3e3ac-192">Manage resources</span></span>
* [<span data-ttu-id="3e3ac-193">Gerenciar os recursos de cluster do Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e3ac-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="3e3ac-194">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="3e3ac-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
