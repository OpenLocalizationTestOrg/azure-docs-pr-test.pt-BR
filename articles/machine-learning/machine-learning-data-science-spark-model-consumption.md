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
# <a name="operationalize-spark-built-machine-learning-models"></a>Operacionalizar modelos de aprendizado de máquina criados no Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Este tópico mostra como toooperationalize um modelo de aprendizado de máquina salva (ML) usando Python no HDInsight Spark clusters. Descreve como tooload modelos de aprendizado que foram criados usando Spark MLlib e armazenados no armazenamento de Blob do Azure (WASB) do computador e tooscore com conjuntos de dados que foram armazenados em WASB também. Mostra dados de entrada do processo como toopre hello, recursos de transformação usando Olá funções de indexação e a codificação no Kit de ferramentas do hello MLlib e como toocreate um objeto de dados de rotulado ponto que pode ser usado como entrada para pontuação com modelos de saudação ML. modelos de saudação usados para pontuação incluem Regressão Linear, Regressão logística, modelos de floresta aleatório e modelos de árvore de aumento de gradiente.

## <a name="spark-clusters-and-jupyter-notebooks"></a>Clusters do Spark e notebooks Jupyter
Etapas de instalação e Olá código toooperationalize um modelo ML são fornecidos neste passo a passo para usar um cluster HDInsight Spark 1.6, bem como um cluster Spark 2.0. código de saudação para esses procedimentos também são fornecidos em blocos de anotações do Jupyter.

### <a name="notebook-for-spark-16"></a>Notebook para Spark 1.6
Olá [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) notebook Jupyter mostra como toooperationalize um modelo de salvo usando Python no HDInsight clusters. 

### <a name="notebook-for-spark-20"></a>Notebook para Spark 2.0
anotações do Jupyter Olá toomodify para toouse 1.6 Spark com um cluster HDInsight Spark 2.0, substitua o arquivo de código Python Olá com [esse arquivo](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py). Esse código mostra como os modelos de saudação tooconsume criados no Spark 2.0.


## <a name="prerequisites"></a>Pré-requisitos

1. Você precisa de uma conta do Azure e um Spark 1.6 (ou 2.0 Spark) cluster HDInsight toocomplete este passo a passo. Consulte Olá [visão geral de ciência de dados usando o Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md) para obter instruções sobre como toosatisfy esses requisitos. Esse tópico também contém uma descrição da saudação dados NYC 2013 táxi usados aqui e instruções sobre como tooexecute código de um bloco de anotações do Jupyter no cluster do Spark hello. 
2. Você também deve criar hello modelos de aprendizado de máquina toobe aqui classificado trabalhando Olá [exploração de dados e modelagem com Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tópico para cluster Olá Spark 1.6 ou notebooks Olá Spark 2.0. 
3. blocos de anotações Olá Spark 2.0 usam um conjunto de dados adicional para tarefa de classificação hello, Olá conhecido aérea no horário partida conjunto de dados de 2011 e 2012. Uma descrição da saudação toothem de anotações e links são fornecidos no hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para o repositório do GitHub Olá que os contém. Além disso, Olá código aqui e em blocos de anotações Olá vinculado é genérico e deve funcionar em qualquer cluster do Spark. Se você não estiver usando o HDInsight Spark, as etapas de configuração e gerenciamento de cluster Olá podem ser ligeiramente diferentes da que é mostrado aqui. 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Programa de instalação: Olá, bibliotecas e locais de armazenamento predefinição contexto Spark
Spark é capaz de tooan tooread e gravação Blob de armazenamento do Azure (WASB). Para qualquer um dos seus dados existentes armazenados podem ser processadas usando Spark e Olá resultados armazenados em WASB.

toosave modelos ou os arquivos em WASB, o caminho Olá precisa toobe especificado corretamente. Olá padrão contêiner anexado toohello Spark cluster pode ser referenciado usando um caminho começando com: *"wasb / /"*. Olá, exemplo de código a seguir especifica o local de saudação de Olá toobe de dados de leitura e Olá caminho para a saída do modelo Olá modelo armazenamento diretório toowhich Olá é salvo. 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Definir caminhos de diretório para locais de armazenamento no WASB
Os modelos são salvos em: "wasb:///user/remoteuser/NYCTaxi/Models". Se esse caminho não estiver definido corretamente, os modelos não serão carregados para pontuação.

Olá resultados classificados tem sido salvo em: "wasb: / / / usuário/remoteuser/NYCTaxi/ScoredResults". Se Olá caminho toofolder estiver incorreta, resultados não são salvos na pasta.   

> [!NOTE]
> locais de caminho do arquivo Hello podem ser copiados e colados em espaços reservados de saudação nesse código da saída de saudação da última célula Olá Olá **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.   
> 
> 

Aqui está a caminhos de diretório Olá código tooset: 

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

**SAÍDA:**

datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)

### <a name="import-libraries"></a>Importar bibliotecas
Definir contexto spark e importar bibliotecas necessárias com hello código a seguir

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


### <a name="preset-spark-context-and-pyspark-magics"></a>Contexto predefinido do Spark e palavras mágicas do PySpark
kernels PySpark de saudação que são fornecidos com blocos de anotações do Jupyter tem um contexto de predefinição. Portanto não é necessário tooset Olá Spark ou Hive contextos explicitamente antes de começar a trabalhar com o aplicativo hello que você está desenvolvendo. Eles estão disponíveis para você por padrão. Esses contextos são:

* sc - para o Spark 
* sqlContext - para o Hive

Olá PySpark kernel fornece algumas predefinidas "magics", que são comandos especiais que podem ser chamados com % %. Há dois comandos que são usados nesses exemplos de código.

* **% % local** especificado que o código de saudação em linhas subsequentes é executado localmente. O código deve ser um código Python válido.
* **%%sql -o <variable name>** 
* Executa uma consulta de Hive em Olá sqlContext. Se Olá -o parâmetro for passado, resultado de saudação de consulta de saudação é mantido no Olá % % contexto Python local como um dataframe Pandas.

Para obter mais informações sobre kernels Olá para blocos de anotações do Jupyter e hello predefinidas "magics" que eles fornecem, consulte [clusters Kernels disponíveis para blocos de anotações do Jupyter com Linux do HDInsight Spark no HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a>Ingerir dados e criar um quadro de dados limpo
Esta seção contém código Olá para uma série de tarefas necessária tooingest Olá dados toobe classificado. Dados de saudação do formato de leitura em um exemplo de 0,1% unidas Olá táxi viagem e passagens do arquivo de (armazenado como um arquivo. tsv) e, em seguida, cria um quadro de dados limpo.

Olá táxi viagem e passagens arquivos foram adicionados com base no procedimento Olá fornecido no: [Olá o processo de ciência de dados de equipe em ação: usar clusters de HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) tópico.

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 46.37 segundos

## <a name="prepare-data-for-scoring-in-spark"></a>Preparar dados para pontuação no Spark
Esta seção mostra como tooindex, codificar e dimensionar recursos categóricos tooprepare-los para usam em algoritmos de aprendizado supervisionado de MLlib para classificação e regressão.

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a>Transformação de recurso: indexe e codifique recursos categóricos para entrada em modelos de pontuação
Esta seção mostra como tooindex dados categóricos usando um `StringIndexer` e codificar os recursos com `OneHotEncoder` de entrada em modelos de saudação.

Olá [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) codifica uma coluna de cadeia de caracteres da coluna de tooa de rótulos de índices de rótulo. índices de saudação são ordenados por frequências de rótulo. 

Olá [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) mapeia uma coluna da coluna de tooa de índices de rótulo de vetores de binários, no máximo um único um valor. Essa codificação permite que os algoritmos que esperam contínuos recursos importantes, como a regressão logística, recursos de toocategorical toobe aplicado.

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 5,37 segundos

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a>Crie objetos RDD com matrizes de recurso para entrada em modelos
Esta seção contém o código que mostra como tooindex categórica e dados de texto como um RDD objeto hot um codificação-lo para que ele pode ser usado tootrain e teste MLlib Regressão logística e modelos de árvore. Olá dados indexados são armazenados em [resiliente distribuídas Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objetos. Esses são a abstração básica Olá no Spark. Um objeto RDD representa uma coleção imutável e particionada de elementos que pode ser operada em paralelo com o Spark.

Ele também contém o código que mostra como os dados de tooscale com hello `StandardScalar` fornecido por MLlib para uso na regressão linear com Estocástico gradiente descendente (SGD), um algoritmo popular de treinamento de uma ampla variedade de modelos de aprendizado de máquina. Olá [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) é usado tooscale Olá recursos toounit variância. Dimensionamento de recurso, também conhecido como normalização de dados assegura que os recursos com valores amplamente distribuídos são não fornecido excessiva pesar na função objetivo hello. 

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 11.72 segundos

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a>Pontuação com hello modelo de regressão logística e salvar a saída tooblob
código Olá nesta seção mostra como tooload um modelo de regressão logística que foi salvo no Azure armazenamento de blob e usá-lo toopredict ou não uma dica é pago em uma viagem de táxi, pontuação-lo com as métricas de classificação padrão e, em seguida, salvar e plotar Olá resultados tooblob armazenamento. Olá resultados classificado são armazenados em objetos RDD. 

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 19.22 segundos

## <a name="score-a-linear-regression-model"></a>Classificar um modelo de regressão linear
Usamos [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain um modelo de regressão linear usando descendente do gradiente Estocástico (SGD) para otimização toopredict Olá total dica paga. 

código Olá nesta seção mostra como tooload um modelo de regressão Linear do armazenamento de BLOBs do Azure, classificação usando variáveis em escala e em seguida, salve o blob de backup toohello resultados hello.

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


**SAÍDA:**

Tempo gasto tooexecute acima célula: 16.63 segundos

## <a name="score-classification-and-regression-random-forest-models"></a>Pontue modelos de florestas aleatórias de classificação e regressão
código Olá nesta seção mostra como Olá tooload salvos classificação e modelos de floresta aleatório regressão salva no armazenamento de BLOBs do Azure, pontuação seu desempenho com classificação padrão e as medidas de regressão e salve Olá resultados tooblob back armazenamento.

[Florestas aleatórias](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) são conjuntos de árvores de decisão.  Elas combinam muitas decisões árvores tooreduce Olá risco de superajuste. Florestas aleatórias podem lidar com recursos categóricos, estender a configuração de classificação multiclasse toohello, não exigem dimensionamento de recurso e são capazes de toocapture não linearidades e interações de recursos. Florestas aleatórias são um dos modelos de classificação e regressão de aprendizado de máquina mais bem-sucedida de saudação.

[spark.mllib](http://spark.apache.org/mllib/) dá suporte a florestas aleatórias na classificação binária, multiclasse e regressão, usando recursos contínuos e categóricos. 

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 31.07 segundos

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a>Pontue modelos de árvore de aumento gradiente de classificação e regressão
código Olá nesta seção mostra como classificação tooload regressão gradiente modelos de árvore de aumento do armazenamento de BLOBs do Azure, pontuação seu desempenho com classificação padrão e as medidas de regressão e salve Olá resultados tooblob back armazenamento. 

**spark.mllib** dá suporte a GBTs para classificação binária e de regressão usando recursos contínuos e categóricos. 

[GBTs (árvores de aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão. Árvores de decisão de treinar GBTs iterativamente toominimize uma função de perda. GBTs pode lidar com recursos categóricos, não requerem o dimensionamento de recurso e são capazes de toocapture não linearidades e interações de recursos. Elas também podem ser usadas em uma configuração de classificação multiclasse.

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 14.6 segundos

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a>Limpe objetos da memória e imprima a localização de arquivos pontuados
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


**SAÍDA:**

logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt

linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949

randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt

randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt

BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt

BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt

## <a name="consume-spark-models-through-a-web-interface"></a>Consumir modelos do Spark por meio de uma interface Web
Spark fornece um mecanismo tooremotely trabalhos de lote de envio ou consultas interativas por meio de uma pausa de interface com um componente chamado Livy. O Livy está habilitado por padrão no cluster Spark no HDInsight. Para saber mais sobre o Livy, confira: [Enviar trabalhos em Spark remotamente usando o Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md). 

Você pode usar Livy tooremotely enviar um trabalho que o lote pontuações de um arquivo que é armazenado em um blob do Azure e, em seguida, grava o blob de tooanother resultados hello. toodo isso, carregue o script de Python de saudação do  
[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob de cluster do Spark hello. Você pode usar uma ferramenta como **Microsoft Azure Storage Explorer** ou **AzCopy** blob de cluster toocopy Olá script toohello. Em nosso caso é carregado script hello muito***wasb:///example/python/ConsumeGBNYCReg.py***.   

> [!NOTE]
> Olá chaves de acesso que você precisa podem ser encontrados no portal de Olá Olá conta de armazenamento associada Olá Spark cluster. 
> 
> 

Uma vez carregado toothis local, esse script é executado no cluster do Spark Olá em um contexto distribuído. Carrega o modelo hello e executa previsões em arquivos de entrada com base no modelo de saudação.  

Você pode chamar esse script remotamente fazendo uma simples solicitação HTTPS/REST no Livy.  Aqui está uma ondulação comando tooconstruct Olá HTTP solicitação tooinvoke Olá script Python remotamente. Substitua os valores apropriados para seu cluster Spark Olá CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME.

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

Você pode usar qualquer linguagem no trabalho de Spark de Olá Olá sistema remoto tooinvoke por meio de Livy fazendo uma chamada simple de HTTPS com a autenticação básica.   

> [!NOTE]
> Seria conveniente toouse biblioteca de solicitações de Python de Olá ao fazer essa chamada HTTP, mas ela não está instalada por padrão em funções do Azure. Portanto, em vez disso, são usadas bibliotecas HTTP mais antigas.   
> 
> 

Este é o código de Python de saudação para chamada hello HTTP:

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


Você também pode adicionar esse código Python muito[funções do Azure](https://azure.microsoft.com/documentation/services/functions/) tootrigger um envio de trabalho Spark pontuações de um blob com base em vários eventos como um timer, criação ou atualização de um blob. 

Se você preferir uma experiência de cliente gratuito de código, use Olá [os aplicativos lógicos do Azure](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke Olá Spark pontuação em lote ao definir uma ação HTTP Olá **lógica aplicativos Designer** e seus parâmetros de configuração. 

* No Portal do Azure, crie um novo aplicativo lógico selecionando **+Novo** -> **Web + Móvel** -> **Aplicativo Lógico**. 
* toobring backup Olá **lógica aplicativos Designer**, insira nome de saudação do hello lógica de aplicativo e o plano de serviço de aplicativo.
* Selecione uma ação HTTP e insira parâmetros de saudação mostrados na figura a seguir de saudação:

![Designer de Aplicativos Lógicos](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a>O que vem a seguir?
**Validação cruzada e limpeza de hiperparâmetro**: confira [Modelagem e exploração de dados avançados com o Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) para saber como os modelos podem ser treinados usando a validação cruzada e a limpeza de hiperparâmetro.

