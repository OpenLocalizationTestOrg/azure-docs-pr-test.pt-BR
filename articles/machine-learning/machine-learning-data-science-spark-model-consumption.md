---
title: "aaaOperationalize criado Spark aprendizado de máquina modelos | Microsoft Docs"
description: "Como tooload e pontuação aprender os modelos armazenados no armazenamento de Blob de Azure (WASB) com Python."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="53f04-103">Operacionalizar modelos de aprendizado de máquina criados no Spark</span><span class="sxs-lookup"><span data-stu-id="53f04-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="53f04-104">Este tópico mostra como toooperationalize um modelo de aprendizado de máquina salva (ML) usando Python no HDInsight Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="53f04-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="53f04-105">Descreve como tooload modelos de aprendizado que foram criados usando Spark MLlib e armazenados no armazenamento de Blob do Azure (WASB) do computador e tooscore com conjuntos de dados que foram armazenados em WASB também.</span><span class="sxs-lookup"><span data-stu-id="53f04-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="53f04-106">Mostra dados de entrada do processo como toopre hello, recursos de transformação usando Olá funções de indexação e a codificação no Kit de ferramentas do hello MLlib e como toocreate um objeto de dados de rotulado ponto que pode ser usado como entrada para pontuação com modelos de saudação ML.</span><span class="sxs-lookup"><span data-stu-id="53f04-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="53f04-107">modelos de saudação usados para pontuação incluem Regressão Linear, Regressão logística, modelos de floresta aleatório e modelos de árvore de aumento de gradiente.</span><span class="sxs-lookup"><span data-stu-id="53f04-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="53f04-108">Clusters do Spark e notebooks Jupyter</span><span class="sxs-lookup"><span data-stu-id="53f04-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="53f04-109">Etapas de instalação e Olá código toooperationalize um modelo ML são fornecidos neste passo a passo para usar um cluster HDInsight Spark 1.6, bem como um cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="53f04-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="53f04-110">código de saudação para esses procedimentos também são fornecidos em blocos de anotações do Jupyter.</span><span class="sxs-lookup"><span data-stu-id="53f04-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="53f04-111">Notebook para Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="53f04-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="53f04-112">Olá [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) notebook Jupyter mostra como toooperationalize um modelo de salvo usando Python no HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="53f04-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="53f04-113">Notebook para Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="53f04-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="53f04-114">anotações do Jupyter Olá toomodify para toouse 1.6 Spark com um cluster HDInsight Spark 2.0, substitua o arquivo de código Python Olá com [esse arquivo](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="53f04-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="53f04-115">Esse código mostra como os modelos de saudação tooconsume criados no Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="53f04-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="53f04-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="53f04-116">Prerequisites</span></span>

1. <span data-ttu-id="53f04-117">Você precisa de uma conta do Azure e um Spark 1.6 (ou 2.0 Spark) cluster HDInsight toocomplete este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="53f04-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="53f04-118">Consulte Olá [visão geral de ciência de dados usando o Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md) para obter instruções sobre como toosatisfy esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="53f04-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="53f04-119">Esse tópico também contém uma descrição da saudação dados NYC 2013 táxi usados aqui e instruções sobre como tooexecute código de um bloco de anotações do Jupyter no cluster do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="53f04-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="53f04-120">Você também deve criar hello modelos de aprendizado de máquina toobe aqui classificado trabalhando Olá [exploração de dados e modelagem com Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tópico para cluster Olá Spark 1.6 ou notebooks Olá Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="53f04-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="53f04-121">blocos de anotações Olá Spark 2.0 usam um conjunto de dados adicional para tarefa de classificação hello, Olá conhecido aérea no horário partida conjunto de dados de 2011 e 2012.</span><span class="sxs-lookup"><span data-stu-id="53f04-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="53f04-122">Uma descrição da saudação toothem de anotações e links são fornecidos no hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para o repositório do GitHub Olá que os contém.</span><span class="sxs-lookup"><span data-stu-id="53f04-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="53f04-123">Além disso, Olá código aqui e em blocos de anotações Olá vinculado é genérico e deve funcionar em qualquer cluster do Spark.</span><span class="sxs-lookup"><span data-stu-id="53f04-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="53f04-124">Se você não estiver usando o HDInsight Spark, as etapas de configuração e gerenciamento de cluster Olá podem ser ligeiramente diferentes da que é mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="53f04-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="53f04-125">Programa de instalação: Olá, bibliotecas e locais de armazenamento predefinição contexto Spark</span><span class="sxs-lookup"><span data-stu-id="53f04-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="53f04-126">Spark é capaz de tooan tooread e gravação Blob de armazenamento do Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="53f04-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="53f04-127">Para qualquer um dos seus dados existentes armazenados podem ser processadas usando Spark e Olá resultados armazenados em WASB.</span><span class="sxs-lookup"><span data-stu-id="53f04-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="53f04-128">toosave modelos ou os arquivos em WASB, o caminho Olá precisa toobe especificado corretamente.</span><span class="sxs-lookup"><span data-stu-id="53f04-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="53f04-129">Olá padrão contêiner anexado toohello Spark cluster pode ser referenciado usando um caminho começando com: *"wasb / /"*.</span><span class="sxs-lookup"><span data-stu-id="53f04-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="53f04-130">Olá, exemplo de código a seguir especifica o local de saudação de Olá toobe de dados de leitura e Olá caminho para a saída do modelo Olá modelo armazenamento diretório toowhich Olá é salvo.</span><span class="sxs-lookup"><span data-stu-id="53f04-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="53f04-131">Definir caminhos de diretório para locais de armazenamento no WASB</span><span class="sxs-lookup"><span data-stu-id="53f04-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="53f04-132">Os modelos são salvos em: "wasb:///user/remoteuser/NYCTaxi/Models".</span><span class="sxs-lookup"><span data-stu-id="53f04-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="53f04-133">Se esse caminho não estiver definido corretamente, os modelos não serão carregados para pontuação.</span><span class="sxs-lookup"><span data-stu-id="53f04-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="53f04-134">Olá resultados classificados tem sido salvo em: "wasb: / / / usuário/remoteuser/NYCTaxi/ScoredResults".</span><span class="sxs-lookup"><span data-stu-id="53f04-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="53f04-135">Se Olá caminho toofolder estiver incorreta, resultados não são salvos na pasta.</span><span class="sxs-lookup"><span data-stu-id="53f04-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="53f04-136">locais de caminho do arquivo Hello podem ser copiados e colados em espaços reservados de saudação nesse código da saída de saudação da última célula Olá Olá **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span><span class="sxs-lookup"><span data-stu-id="53f04-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="53f04-137">Aqui está a caminhos de diretório Olá código tooset:</span><span class="sxs-lookup"><span data-stu-id="53f04-137">Here is hello code tooset directory paths:</span></span> 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="53f04-138">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="53f04-138">**OUTPUT:**</span></span>

<span data-ttu-id="53f04-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="53f04-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="53f04-140">Importar bibliotecas</span><span class="sxs-lookup"><span data-stu-id="53f04-140">Import libraries</span></span>
<span data-ttu-id="53f04-141">Definir contexto spark e importar bibliotecas necessárias com hello código a seguir</span><span class="sxs-lookup"><span data-stu-id="53f04-141">Set spark context and import necessary libraries with hello following code</span></span>

    #IMPORT LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="53f04-142">Contexto predefinido do Spark e palavras mágicas do PySpark</span><span class="sxs-lookup"><span data-stu-id="53f04-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="53f04-143">kernels PySpark de saudação que são fornecidos com blocos de anotações do Jupyter tem um contexto de predefinição.</span><span class="sxs-lookup"><span data-stu-id="53f04-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="53f04-144">Portanto não é necessário tooset Olá Spark ou Hive contextos explicitamente antes de começar a trabalhar com o aplicativo hello que você está desenvolvendo.</span><span class="sxs-lookup"><span data-stu-id="53f04-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="53f04-145">Eles estão disponíveis para você por padrão.</span><span class="sxs-lookup"><span data-stu-id="53f04-145">These are available for you by default.</span></span> <span data-ttu-id="53f04-146">Esses contextos são:</span><span class="sxs-lookup"><span data-stu-id="53f04-146">These contexts are:</span></span>

* <span data-ttu-id="53f04-147">sc - para o Spark</span><span class="sxs-lookup"><span data-stu-id="53f04-147">sc - for Spark</span></span> 
* <span data-ttu-id="53f04-148">sqlContext - para o Hive</span><span class="sxs-lookup"><span data-stu-id="53f04-148">sqlContext - for Hive</span></span>

<span data-ttu-id="53f04-149">Olá PySpark kernel fornece algumas predefinidas "magics", que são comandos especiais que podem ser chamados com % %.</span><span class="sxs-lookup"><span data-stu-id="53f04-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="53f04-150">Há dois comandos que são usados nesses exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="53f04-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="53f04-151">**% % local** especificado que o código de saudação em linhas subsequentes é executado localmente.</span><span class="sxs-lookup"><span data-stu-id="53f04-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="53f04-152">O código deve ser um código Python válido.</span><span class="sxs-lookup"><span data-stu-id="53f04-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="53f04-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="53f04-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="53f04-154">Executa uma consulta de Hive em Olá sqlContext.</span><span class="sxs-lookup"><span data-stu-id="53f04-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="53f04-155">Se Olá -o parâmetro for passado, resultado de saudação de consulta de saudação é mantido no Olá % % contexto Python local como um dataframe Pandas.</span><span class="sxs-lookup"><span data-stu-id="53f04-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="53f04-156">Para obter mais informações sobre kernels Olá para blocos de anotações do Jupyter e hello predefinidas "magics" que eles fornecem, consulte [clusters Kernels disponíveis para blocos de anotações do Jupyter com Linux do HDInsight Spark no HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="53f04-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="53f04-157">Ingerir dados e criar um quadro de dados limpo</span><span class="sxs-lookup"><span data-stu-id="53f04-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="53f04-158">Esta seção contém código Olá para uma série de tarefas necessária tooingest Olá dados toobe classificado.</span><span class="sxs-lookup"><span data-stu-id="53f04-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="53f04-159">Dados de saudação do formato de leitura em um exemplo de 0,1% unidas Olá táxi viagem e passagens do arquivo de (armazenado como um arquivo. tsv) e, em seguida, cria um quadro de dados limpo.</span><span class="sxs-lookup"><span data-stu-id="53f04-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="53f04-160">Olá táxi viagem e passagens arquivos foram adicionados com base no procedimento Olá fornecido no: [Olá o processo de ciência de dados de equipe em ação: usar clusters de HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="53f04-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_test_file.first()
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

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="53f04-161">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="53f04-161">**OUTPUT:**</span></span>

<span data-ttu-id="53f04-162">Tempo gasto tooexecute acima célula: 46.37 segundos</span><span class="sxs-lookup"><span data-stu-id="53f04-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="53f04-163">Preparar dados para pontuação no Spark</span><span class="sxs-lookup"><span data-stu-id="53f04-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="53f04-164">Esta seção mostra como tooindex, codificar e dimensionar recursos categóricos tooprepare-los para usam em algoritmos de aprendizado supervisionado de MLlib para classificação e regressão.</span><span class="sxs-lookup"><span data-stu-id="53f04-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="53f04-165">Transformação de recurso: indexe e codifique recursos categóricos para entrada em modelos de pontuação</span><span class="sxs-lookup"><span data-stu-id="53f04-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="53f04-166">Esta seção mostra como tooindex dados categóricos usando um `StringIndexer` e codificar os recursos com `OneHotEncoder` de entrada em modelos de saudação.</span><span class="sxs-lookup"><span data-stu-id="53f04-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="53f04-167">Olá [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) codifica uma coluna de cadeia de caracteres da coluna de tooa de rótulos de índices de rótulo.</span><span class="sxs-lookup"><span data-stu-id="53f04-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="53f04-168">índices de saudação são ordenados por frequências de rótulo.</span><span class="sxs-lookup"><span data-stu-id="53f04-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="53f04-169">Olá [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) mapeia uma coluna da coluna de tooa de índices de rótulo de vetores de binários, no máximo um único um valor.</span><span class="sxs-lookup"><span data-stu-id="53f04-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="53f04-170">Essa codificação permite que os algoritmos que esperam contínuos recursos importantes, como a regressão logística, recursos de toocategorical toobe aplicado.</span><span class="sxs-lookup"><span data-stu-id="53f04-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
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

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="53f04-171">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="53f04-171">**OUTPUT:**</span></span>

<span data-ttu-id="53f04-172">Tempo gasto tooexecute acima célula: 5,37 segundos</span><span class="sxs-lookup"><span data-stu-id="53f04-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="53f04-173">Crie objetos RDD com matrizes de recurso para entrada em modelos</span><span class="sxs-lookup"><span data-stu-id="53f04-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="53f04-174">Esta seção contém o código que mostra como tooindex categórica e dados de texto como um RDD objeto hot um codificação-lo para que ele pode ser usado tootrain e teste MLlib Regressão logística e modelos de árvore.</span><span class="sxs-lookup"><span data-stu-id="53f04-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="53f04-175">Olá dados indexados são armazenados em [resiliente distribuídas Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objetos.</span><span class="sxs-lookup"><span data-stu-id="53f04-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="53f04-176">Esses são a abstração básica Olá no Spark.</span><span class="sxs-lookup"><span data-stu-id="53f04-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="53f04-177">Um objeto RDD representa uma coleção imutável e particionada de elementos que pode ser operada em paralelo com o Spark.</span><span class="sxs-lookup"><span data-stu-id="53f04-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="53f04-178">Ele também contém o código que mostra como os dados de tooscale com hello `StandardScalar` fornecido por MLlib para uso na regressão linear com Estocástico gradiente descendente (SGD), um algoritmo popular de treinamento de uma ampla variedade de modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="53f04-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="53f04-179">Olá [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) é usado tooscale Olá recursos toounit variância.</span><span class="sxs-lookup"><span data-stu-id="53f04-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="53f04-180">Dimensionamento de recurso, também conhecido como normalização de dados assegura que os recursos com valores amplamente distribuídos são não fornecido excessiva pesar na função objetivo hello.</span><span class="sxs-lookup"><span data-stu-id="53f04-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="53f04-181">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="53f04-181">**OUTPUT:**</span></span>

<span data-ttu-id="53f04-182">Tempo gasto tooexecute acima célula: 11.72 segundos</span><span class="sxs-lookup"><span data-stu-id="53f04-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="53f04-183">Pontuação com hello modelo de regressão logística e salvar a saída tooblob</span><span class="sxs-lookup"><span data-stu-id="53f04-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="53f04-184">código Olá nesta seção mostra como tooload um modelo de regressão logística que foi salvo no Azure armazenamento de blob e usá-lo toopredict ou não uma dica é pago em uma viagem de táxi, pontuação-lo com as métricas de classificação padrão e, em seguida, salvar e plotar Olá resultados tooblob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="53f04-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="53f04-185">Olá resultados classificado são armazenados em objetos RDD.</span><span class="sxs-lookup"><span data-stu-id="53f04-185">hello scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="53f04-186">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="53f04-186">**OUTPUT:**</span></span>

<span data-ttu-id="53f04-187">Tempo gasto tooexecute acima célula: 19.22 segundos</span><span class="sxs-lookup"><span data-stu-id="53f04-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="53f04-188">Classificar um modelo de regressão linear</span><span class="sxs-lookup"><span data-stu-id="53f04-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="53f04-189">Usamos [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain um modelo de regressão linear usando descendente do gradiente Estocástico (SGD) para otimização toopredict Olá total dica paga.</span><span class="sxs-lookup"><span data-stu-id="53f04-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="53f04-190">código Olá nesta seção mostra como tooload um modelo de regressão Linear do armazenamento de BLOBs do Azure, classificação usando variáveis em escala e em seguida, salve o blob de backup toohello resultados hello.</span><span class="sxs-lookup"><span data-stu-id="53f04-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="53f04-191">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="53f04-191">**OUTPUT:**</span></span>

<span data-ttu-id="53f04-192">Tempo gasto tooexecute acima célula: 16.63 segundos</span><span class="sxs-lookup"><span data-stu-id="53f04-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="53f04-193">Pontue modelos de florestas aleatórias de classificação e regressão</span><span class="sxs-lookup"><span data-stu-id="53f04-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="53f04-194">código Olá nesta seção mostra como Olá tooload salvos classificação e modelos de floresta aleatório regressão salva no armazenamento de BLOBs do Azure, pontuação seu desempenho com classificação padrão e as medidas de regressão e salve Olá resultados tooblob back armazenamento.</span><span class="sxs-lookup"><span data-stu-id="53f04-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="53f04-195">[Florestas aleatórias](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="53f04-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="53f04-196">Elas combinam muitas decisões árvores tooreduce Olá risco de superajuste.</span><span class="sxs-lookup"><span data-stu-id="53f04-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="53f04-197">Florestas aleatórias podem lidar com recursos categóricos, estender a configuração de classificação multiclasse toohello, não exigem dimensionamento de recurso e são capazes de toocapture não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="53f04-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="53f04-198">Florestas aleatórias são um dos modelos de classificação e regressão de aprendizado de máquina mais bem-sucedida de saudação.</span><span class="sxs-lookup"><span data-stu-id="53f04-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="53f04-199">[spark.mllib](http://spark.apache.org/mllib/) dá suporte a florestas aleatórias na classificação binária, multiclasse e regressão, usando recursos contínuos e categóricos.</span><span class="sxs-lookup"><span data-stu-id="53f04-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="53f04-200">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="53f04-200">**OUTPUT:**</span></span>

<span data-ttu-id="53f04-201">Tempo gasto tooexecute acima célula: 31.07 segundos</span><span class="sxs-lookup"><span data-stu-id="53f04-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="53f04-202">Pontue modelos de árvore de aumento gradiente de classificação e regressão</span><span class="sxs-lookup"><span data-stu-id="53f04-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="53f04-203">código Olá nesta seção mostra como classificação tooload regressão gradiente modelos de árvore de aumento do armazenamento de BLOBs do Azure, pontuação seu desempenho com classificação padrão e as medidas de regressão e salve Olá resultados tooblob back armazenamento.</span><span class="sxs-lookup"><span data-stu-id="53f04-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="53f04-204">**spark.mllib** dá suporte a GBTs para classificação binária e de regressão usando recursos contínuos e categóricos.</span><span class="sxs-lookup"><span data-stu-id="53f04-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="53f04-205">[GBTs (árvores de aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão.</span><span class="sxs-lookup"><span data-stu-id="53f04-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="53f04-206">Árvores de decisão de treinar GBTs iterativamente toominimize uma função de perda.</span><span class="sxs-lookup"><span data-stu-id="53f04-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="53f04-207">GBTs pode lidar com recursos categóricos, não requerem o dimensionamento de recurso e são capazes de toocapture não linearidades e interações de recursos.</span><span class="sxs-lookup"><span data-stu-id="53f04-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="53f04-208">Elas também podem ser usadas em uma configuração de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="53f04-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="53f04-209">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="53f04-209">**OUTPUT:**</span></span>

<span data-ttu-id="53f04-210">Tempo gasto tooexecute acima célula: 14.6 segundos</span><span class="sxs-lookup"><span data-stu-id="53f04-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="53f04-211">Limpe objetos da memória e imprima a localização de arquivos pontuados</span><span class="sxs-lookup"><span data-stu-id="53f04-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="53f04-212">**SAÍDA:**</span><span class="sxs-lookup"><span data-stu-id="53f04-212">**OUTPUT:**</span></span>

<span data-ttu-id="53f04-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="53f04-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="53f04-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="53f04-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="53f04-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="53f04-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="53f04-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="53f04-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="53f04-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="53f04-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="53f04-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="53f04-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="53f04-219">Consumir modelos do Spark por meio de uma interface Web</span><span class="sxs-lookup"><span data-stu-id="53f04-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="53f04-220">Spark fornece um mecanismo tooremotely trabalhos de lote de envio ou consultas interativas por meio de uma pausa de interface com um componente chamado Livy.</span><span class="sxs-lookup"><span data-stu-id="53f04-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="53f04-221">O Livy está habilitado por padrão no cluster Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="53f04-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="53f04-222">Para saber mais sobre o Livy, confira: [Enviar trabalhos em Spark remotamente usando o Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="53f04-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="53f04-223">Você pode usar Livy tooremotely enviar um trabalho que o lote pontuações de um arquivo que é armazenado em um blob do Azure e, em seguida, grava o blob de tooanother resultados hello.</span><span class="sxs-lookup"><span data-stu-id="53f04-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="53f04-224">toodo isso, carregue o script de Python de saudação do</span><span class="sxs-lookup"><span data-stu-id="53f04-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="53f04-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob de cluster do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="53f04-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="53f04-226">Você pode usar uma ferramenta como **Microsoft Azure Storage Explorer** ou **AzCopy** blob de cluster toocopy Olá script toohello.</span><span class="sxs-lookup"><span data-stu-id="53f04-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="53f04-227">Em nosso caso é carregado script hello muito***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="53f04-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="53f04-228">Olá chaves de acesso que você precisa podem ser encontrados no portal de Olá Olá conta de armazenamento associada Olá Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="53f04-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="53f04-229">Uma vez carregado toothis local, esse script é executado no cluster do Spark Olá em um contexto distribuído.</span><span class="sxs-lookup"><span data-stu-id="53f04-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="53f04-230">Carrega o modelo hello e executa previsões em arquivos de entrada com base no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="53f04-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="53f04-231">Você pode chamar esse script remotamente fazendo uma simples solicitação HTTPS/REST no Livy.</span><span class="sxs-lookup"><span data-stu-id="53f04-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="53f04-232">Aqui está uma ondulação comando tooconstruct Olá HTTP solicitação tooinvoke Olá script Python remotamente.</span><span class="sxs-lookup"><span data-stu-id="53f04-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="53f04-233">Substitua os valores apropriados para seu cluster Spark Olá CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME.</span><span class="sxs-lookup"><span data-stu-id="53f04-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="53f04-234">Você pode usar qualquer linguagem no trabalho de Spark de Olá Olá sistema remoto tooinvoke por meio de Livy fazendo uma chamada simple de HTTPS com a autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="53f04-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="53f04-235">Seria conveniente toouse biblioteca de solicitações de Python de Olá ao fazer essa chamada HTTP, mas ela não está instalada por padrão em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="53f04-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="53f04-236">Portanto, em vez disso, são usadas bibliotecas HTTP mais antigas.</span><span class="sxs-lookup"><span data-stu-id="53f04-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="53f04-237">Este é o código de Python de saudação para chamada hello HTTP:</span><span class="sxs-lookup"><span data-stu-id="53f04-237">Here is hello Python code for hello HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="53f04-238">Você também pode adicionar esse código Python muito[funções do Azure](https://azure.microsoft.com/documentation/services/functions/) tootrigger um envio de trabalho Spark pontuações de um blob com base em vários eventos como um timer, criação ou atualização de um blob.</span><span class="sxs-lookup"><span data-stu-id="53f04-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="53f04-239">Se você preferir uma experiência de cliente gratuito de código, use Olá [os aplicativos lógicos do Azure](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke Olá Spark pontuação em lote ao definir uma ação HTTP Olá **lógica aplicativos Designer** e seus parâmetros de configuração.</span><span class="sxs-lookup"><span data-stu-id="53f04-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="53f04-240">No Portal do Azure, crie um novo aplicativo lógico selecionando **+Novo** -> **Web + Móvel** -> **Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="53f04-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="53f04-241">toobring backup Olá **lógica aplicativos Designer**, insira nome de saudação do hello lógica de aplicativo e o plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="53f04-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="53f04-242">Selecione uma ação HTTP e insira parâmetros de saudação mostrados na figura a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="53f04-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![Designer de Aplicativos Lógicos](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="53f04-244">O que vem a seguir?</span><span class="sxs-lookup"><span data-stu-id="53f04-244">What's next?</span></span>
<span data-ttu-id="53f04-245">**Validação cruzada e limpeza de hiperparâmetro**: confira [Modelagem e exploração de dados avançados com o Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) para saber como os modelos podem ser treinados usando a validação cruzada e a limpeza de hiperparâmetro.</span><span class="sxs-lookup"><span data-stu-id="53f04-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

