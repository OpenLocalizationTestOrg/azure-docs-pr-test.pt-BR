---
title: "aaaAdvanced a exploração de dados e modelagem com Spark | Microsoft Docs"
description: "Use a exploração de dados do HDInsight Spark toodo e treinar modelos de classificação e regressão binários usando a otimização de validação cruzada e hyperparameter."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a>Modelagem e exploração de dados avançados com o Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Este passo a passo usa HDInsight Spark toodo exploração e treinar binária e classificação de dados usando a validação cruzada de modelos de regressão e otimização de hyperparameter em uma amostra de saudação NYC táxi viagem e passagens de conjunto de dados de 2013. Lhe orienta pelas etapas de saudação do hello [processo de ciência de dados](http://aka.ms/datascienceprocess), cluster de ponta a ponta, usando um HDInsight Spark para processamento e modelos de dados e Olá Olá toostore de blobs do Azure. processo de saudação explora e visualiza os dados transferidos de um Blob de armazenamento do Azure e, em seguida, prepara Olá dados toobuild modelos de previsão. Python foi usado toocode Olá solução e tooshow Olá relevantes gráficos. Esses modelos são compilados usando classificação binária do toodo Olá Spark MLlib Kit de ferramentas e tarefas de modelagem de regressão. 

* Olá **classificação binária** tarefa é toopredict ou não uma dica é pago para viagem hello. 
* Olá **regressão** tarefa é toopredict Olá Olá dica com base em outros recursos de dica. 

etapas de modelagem Olá também contêm código que mostra como tootrain, avaliar e salvar cada tipo de modelo. Olá tópico aborda algumas das Olá mesmo Terra como Olá [exploração de dados e modelagem com Spark](machine-learning-data-science-spark-data-exploration-modeling.md) tópico. Mas ele é mais "Avançado" que também utiliza a validação cruzada com hyperparameter varredura tootrain modelos de classificação e regressão de maneira ideal precisos. 

**Validação cruzada (VC)** é uma técnica que avalia como um modelo treinado em um conjunto conhecido de dados generaliza toopredicting Olá recursos de conjuntos de dados no qual ele não foi treinado.  Uma implementação comum usada aqui é toodivide um conjunto de dados em K dobras e, em seguida, treinar o modelo de saudação de forma round robin em apenas uma das partições de saudação. capacidade de saudação do hello modelo tooprediction com precisão quando testados no conjunto de dados independentes no modelo dobra não usado tootrain Olá Olá será avaliada.

**Otimização de Hyperparameter** Olá problema de escolher um conjunto de hiperparâmetros para um algoritmo de aprendizado, geralmente com a meta de saudação de otimizar uma medida de desempenho do algoritmo Olá em um conjunto de dados independente. **Hiperparâmetros** são valores que devem ser especificados fora do procedimento de treinamento de modelo de saudação. Suposições sobre esses valores podem afetar a flexibilidade de saudação e precisão dos modelos de saudação. Árvores de decisão têm hiperparâmetros, por exemplo, como Olá desejado profundidade e número de folhas na árvore de saudação. As SVMs (Máquinas de Vetor de Suporte) exigem a configuração de um termo de penalidade de classificação incorreta. 

Uma otimização de hyperparameter de tooperform forma comum usada aqui é uma pesquisa de grade, ou um **varredura de parâmetro**. Isso consiste em executar uma pesquisa detalhada por meio de valores de saudação um subconjunto especificado de espaço de hyperparameter Olá para um algoritmo de aprendizado. Validação cruzada pode fornecer um toosort de métrica de desempenho os resultados ideais de Olá produzido pelo algoritmo de pesquisa de grade hello. VC usado com ajuda a varredura de hyperparameter problemas de limite como sobreajuste um tootraining de dados de modelo para que o modelo hello mantém Olá capacidade tooapply toohello conjunto geral de dados do qual Olá dados de treinamento foi extraídos.

os modelos de saudação que usamos incluem gradientes árvores aumentadas, florestas aleatórias e regressão logística e linear:

* [Regressão linear com SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) é um modelo de regressão linear que usa um método descendente gradiente Estocástico (SGD) e para a otimização e recurso de dimensionamento quantidades de dica de saudação toopredict pago. 
* [Regressão logística com LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou regressão "logit", é um modelo de regressão que pode ser usado quando a variável dependente de saudação é categórica toodo a classificação de dados. LBFGS é um algoritmo de otimização de quase-Newton que aproxima o algoritmo Broyden – Fletcher – Goldfarb – Shanno (BFGS) de saudação usando uma quantidade limitada de memória do computador e que é amplamente usada no aprendizado de máquina.
* [Florestas aleatórias](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) são conjuntos de árvores de decisão.  Elas combinam muitas decisões árvores tooreduce Olá risco de superajuste. Florestas aleatórias são usadas para classificação e regressão e podem lidar com recursos categóricos e configuração de classificação multiclasse toohello podem ser estendidas. Eles não exigem recurso escala e são capazes de toocapture não linearidades e interações de recurso. Florestas aleatórias são um dos modelos de classificação e regressão de aprendizado de máquina mais bem-sucedida de saudação.
* [GBTs (árvores com aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão. Árvores de decisão de treinar GBTs iterativamente toominimize uma função de perda. GBTs são usados para classificação e regressão pode lidar com recursos categóricos, não requerem o dimensionamento de recurso e são capazes de toocapture não linearidades e interações de recursos. Elas também podem ser usadas em uma configuração de classificação multiclasse.

Varredura de exemplos do uso de VC e Hyperparameter de modelagem são mostradas para problema de classificação binária hello. Os exemplos mais simples (sem varredura de parâmetro) são apresentados no tópico principal de Olá para tarefas de regressão. Mas, no Apêndice hello, validação usando net Elástico para regressão linear e VC com o uso de varredura de parâmetro de regressão de floresta aleatório também é apresentada. Olá **elástica net** é um método de regressão regularizada para ajuste de regressão linear que modelos linearmente combina as métricas de L1 e L2 hello como penalidades de saudação [Laço](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) e [Montanhas](https://en.wikipedia.org/wiki/Tikhonov_regularization) métodos.   

> [!NOTE]
> Embora o Kit de ferramentas do hello Spark MLlib toowork projetado em grandes conjuntos de dados, um exemplo relativamente pequeno (aproximadamente 30 Mb usando 170 mil linhas, cerca de 0,1% de saudação original NYC dataset) é usado aqui para sua conveniência. Exercício Olá fornecido aqui é executado com eficiência (em cerca de 10 minutos) em um cluster de HDInsight com 2 nós de trabalho. Olá mesmo código, com pequenas modificações, pode ser usado tooprocess-conjuntos de dados maiores, com as modificações apropriadas para o cache de dados na memória e alterar o tamanho do cluster hello.
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a>Instalação: blocos de notas e clusters do Spark
As etapas de configuração e o código são fornecidos neste passo a passo para usar um HDInsight Spark 1.6. Porém, notebooks Jupyter são fornecidos tanto para o HDInsight Spark 1.6 quanto para os clusters Spark 2.0. Uma descrição da saudação toothem de anotações e links são fornecidos no hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para o repositório do GitHub Olá que os contém. Além disso, Olá código aqui e em blocos de anotações Olá vinculado é genérico e deve funcionar em qualquer cluster do Spark. Se você não estiver usando o HDInsight Spark, as etapas de configuração e gerenciamento de cluster Olá podem ser ligeiramente diferentes da que é mostrado aqui. Para sua conveniência, aqui estão Olá links toohello Jupyter blocos de anotações para Spark 1.6 e 2.0 toobe executar no kernel do pyspark de saudação do servidor de Jupyter Notebook de saudação:

### <a name="spark-16-notebooks"></a>Blocos de notas Spark 1.6

[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): inclui tópicos no blocos de notas nº. 1 e o desenvolvimento de modelos usando validação cruzada e ajuste de hiperparâmetro.

### <a name="spark-20-notebooks"></a>Blocos de notas Spark 2.0

[Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este arquivo fornece informações sobre como a exploração de dados tooperform, modelagem e pontuação no Spark 2.0 clusters.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Programa de instalação: Olá, bibliotecas e locais de armazenamento predefinição contexto Spark
Spark é capaz de tooAzure tooread e gravar o Blob de armazenamento (também conhecido como WASB). Para qualquer um dos seus dados existentes armazenados podem ser processadas usando Spark e Olá resultados armazenados em WASB.

toosave modelos ou os arquivos em WASB, o caminho Olá precisa toobe especificado corretamente. Olá padrão contêiner anexado toohello Spark cluster pode ser referenciado usando um caminho começando com: "wasb: / / /". Outros locais são referenciados por "wasb://".

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Definir caminhos de diretório para locais de armazenamento no WASB
Olá, exemplo de código a seguir especifica o local de saudação de Olá toobe de dados de leitura e Olá caminho para a saída do modelo Olá modelo armazenamento diretório toowhich Olá é salvo:

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

**SAÍDA**

datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)

### <a name="import-libraries"></a>Importar bibliotecas
Importe bibliotecas necessárias com hello código a seguir:

    # LOAD PYSPARK LIBRARIES
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
kernels PySpark de saudação que são fornecidos com blocos de anotações do Jupyter tem um contexto de predefinição. Portanto não é necessário tooset Olá Spark ou Hive contextos explicitamente antes de começar a trabalhar com o aplicativo hello que você está desenvolvendo. Esses contextos estão disponíveis para você por padrão. Esses contextos são:

* sc - para o Spark 
* sqlContext - para o Hive

Olá PySpark kernel fornece algumas predefinidas "magics", que são comandos especiais que podem ser chamados com % %. Há dois comandos que são usados nesses exemplos de código.

* **% % local** Especifica que o código de saudação em linhas subsequentes é toobe executado localmente. O código deve ser um código Python válido.
* **% % -o do sql <variable name>**  executa uma consulta de Hive em Olá sqlContext. Se Olá -o parâmetro for passado, resultado de saudação de consulta de saudação é mantido no Olá % % contexto Python local como um DataFrame Pandas.

Para obter mais informações sobre kernels Olá para blocos de anotações do Jupyter e hello predefinidas "magics" que eles fornecem, consulte [clusters Kernels disponíveis para blocos de anotações do Jupyter com Linux do HDInsight Spark no HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="data-ingestion-from-public-blob"></a>Ingestão de dados do blob público:
Olá, primeira etapa no processo de ciência de dados Olá é tooingest Olá dados toobe analisado de fontes de onde ele reside em seu ambiente de modelagem e exploração de dados. Esse ambiente é o Spark neste passo a passo. Esta seção contém Olá código toocomplete uma série de tarefas:

* Olá toobe de exemplo de dados modelado de ingestão
* ler no conjunto de dados entrada hello (armazenado como um arquivo. tsv)
* formato e dados saudação normal
* criar e armazenar objetos em cache (RDDs ou quadros de dados) na memória
* registrá-lo como uma tabela temporária no contexto do SQL.

Este é o código de saudação para ingestão de dados.

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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SAÍDA**

Tempo gasto tooexecute acima célula: 276.62 segundos

## <a name="data-exploration--visualization"></a>Visualização e exploração de dados
Quando dados saudação foi colocados no Spark, hello próxima etapa no processo de ciência de dados Olá é toogain de compreensão mais profunda dos dados Olá por meio de exploração e visualização. Nesta seção, podemos examinar dados de táxi hello usando consultas SQL e recursos em potencial e variáveis de destino de saudação de plotagem para inspeção visual. Especificamente, podemos plotar frequência Olá passageiro de contagens de em viagens táxi, a frequência de saudação de quantidades de ponta e como dicas variam de acordo com o tipo e a quantidade de pagamento.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Plotar um histograma de frequências de contagem de passageiro no exemplo hello de viagens táxi
Esse código e trechos de código subsequentes usam exemplo do SQL tooquery magic hello e os dados de saudação do tooplot magic local.

* **Magic SQL (`%%sql`)** hello HDInsight PySpark kernel dá suporte a fácil embutido HiveQL consultas em relação a saudação sqlContext. saudação (-o VARIABLE_NAME) argumento persiste saída Olá de consulta do SQL hello como um DataFrame Pandas no servidor do Jupyter hello. Isso significa que ele está disponível no modo local hello.
* Olá  **`%%local` mágico** é usado toorun código localmente no servidor de Jupyter hello, que é Olá um nó principal do cluster do HDInsight hello. Normalmente, você usa `%%local` magic após Olá `%%sql -o` magic é usado toorun uma consulta. parâmetro -o de Hello persistir Olá saída de hello SQL consulta localmente. Em seguida, Olá `%%local` gatilhos magic Olá próximo conjunto de toorun de trechos de código localmente em relação a saída de hello de consultas SQL Olá persistiu localmente. saída de Hello é visualizada automaticamente depois de executar código hello.

Essa consulta recupera viagens Olá por contagem de passageiro. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


Esse código cria um quadro de dados local de saída da consulta hello e plota dados saudação. Olá `%%local` mágico cria um local-quadro de dados, `sqlResults`, que pode ser usado para plotar com matplotlib. 

> [!NOTE]
> Essas palavras mágicas do PySpark são usadas várias vezes neste passo a passo. Se a quantidade de saudação de dados for grande, você deve exemplo toocreate um quadro de dados que pode caber na memória local.
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Aqui está viagens de Olá Olá código tooplot por passageiro contagens

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**SAÍDA**

![Frequência de corridas por contagem de passageiros](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

Você pode selecionar entre vários tipos diferentes de visualizações (tabela, pizza, linha, área ou barra) usando Olá **tipo** botões de menu no bloco de anotações de saudação. gráfico de barras Olá é mostrado aqui.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Plote um histograma de valores de gorjetas e como o valor das gorjetas varia pelas tarifas e contagens de passageiros.
Usar um banco de dados consulta toosample do SQL.

    # SQL SQUERY
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


Esta célula código usa Olá consulta toocreate três gráficos Olá de dados do SQL.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


**SAÍDA:** 

![Distribuição de valores de gorjetas](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Valor de gorjeta por contagem de passageiros](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Valor de gorjeta por valor de tarifa](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Engenharia de recursos, transformação e preparação de dados para a modelagem
Esta seção descreve e fornece código Olá para procedimentos usados tooprepare dados para uso em modelagem ML. Ele mostra como as tarefas de saudação toodo a seguir:

* Criar um novo recurso por meio do particionamento de horários em compartimentos de tempo de tráfego
* Indexar e fazer a codificação one-hot dos recursos categóricos
* Criar objetos de ponto rotulado para entrada em funções de ML
* Cria uma amostragem aleatória de subgrupos de dados hello e dividi-lo em treinamento e conjuntos de teste
* Dimensionamento de recursos
* Armazenar objetos em cache na memória

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a>Criar um novo recurso por meio do particionamento de horários de tráfego em compartimentos
Esse código mostra como toocreate um novo recurso por meio do particionamento tráfego vezes em compartimentos e como toocache Olá resultante quadro de dados na memória. Cache leva tempo de execução tooimproved onde resiliente distribuídas conjuntos de dados (RDDs) e quadros de dados são usados repetidamente. Portanto, armazenamos em cache RDDs e quadros de dados em vários estágios no passo a passo.

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

**SAÍDA**

126050

### <a name="index-and-one-hot-encode-categorical-features"></a>Indexar e fazer a codificação one-hot dos recursos categóricos
Esta seção mostra como tooindex ou codificar recursos categóricos para entrada em Olá funções da modelagem. Olá modelagem e prever a funções de MLlib exigem que os recursos com dados categóricos de entrada ser indexados ou codificados toouse anterior. 

Dependendo do modelo de hello, você precisa tooindex ou codificá-los de maneiras diferentes. Por exemplo, modelos de regressão Linear e logística exigem hot uma codificação, onde, por exemplo, um recurso com três categorias pode ser expandido em três colunas de recurso, com cada contendo 0 ou 1 dependendo da categoria de saudação de uma observação. Fornece MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo hot uma codificação de função. Este codificador mapeia uma coluna da coluna de tooa de índices de rótulo de vetores de binários, no máximo um único um valor. Essa codificação permite que os algoritmos que esperam recursos com valores numéricos, como a regressão logística, recursos de toocategorical toobe aplicado.

Aqui está o hello tooindex de código e codificar recursos categóricos:

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

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


**SAÍDA**

Tempo gasto tooexecute acima célula: segundos 3.14

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Criar objetos de ponto rotulado para entrada em funções de ML
Esta seção contém o código que mostra como o tipo de dados de texto categóricos tooindex como um rótulo de ponto de dados e como tooencode-lo. Isso prepara toobe usado tootrain e teste MLlib Regressão logística e outros modelos de classificação. Objetos de ponto rotulados são RDDs (Conjuntos de Dados Resilientes Distribuídos) formatados de uma maneira que é necessária como dados de entrada pela maioria dos algoritmos de ML no MLlib. Um [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) é um vetor local, denso ou esparso, associado a um rótulo/resposta.

Aqui está o hello tooindex de código e codificar os recursos de texto para classificação binária.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


Aqui está o código de saudação tooencode e o índice de recursos categóricos texto para análise de regressão linear.

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>Cria uma amostragem aleatória de subgrupos de dados hello e dividi-lo em treinamento e conjuntos de teste
Esse código cria uma amostragem aleatória de dados de saudação (25% é usado aqui). Embora não seja necessário para este exemplo devido toohello tamanho do conjunto de dados hello, demonstraremos como de exemplo dados Olá aqui. Você sabe como toouse-lo para seus próprios problemas se necessário. Quando as amostras são grandes, isso pode economizar um tempo significativo durante o treinamento de modelos. Em seguida, dividiremos exemplo hello em uma parte de treinamento (75% aqui) e um teste toouse de parte (25% aqui) de classificação e modelagem de regressão.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

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

**SAÍDA**

Tempo gasto tooexecute acima célula: 0.31 segundos

### <a name="feature-scaling"></a>Dimensionamento de recursos
Dimensionamento de recurso, também conhecido como normalização de dados assegura que os recursos com valores amplamente distribuídos são não fornecido excessiva pesar na função objetivo hello. código para o recurso de dimensionamento Hello usa Olá [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) variação de toounit tooscale Olá recursos. Ele é fornecido pela MLlib para uso na regressão linear com SGD (Stochastic Gradient Descent). O SGD é um algoritmo popular de treinamento de uma grande variedade de outros modelos de aprendizado de máquina, como regressões regularizadas ou SVM (máquinas de vetor de suporte).   

> [!TIP]
> Encontramos Olá LinearRegressionWithSGD algoritmo toobe toofeature confidencial dimensionamento.   
> 
> 

Aqui está a variáveis de tooscale Olá código para uso com o algoritmo SGD linear Olá regularizada.

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

**SAÍDA**

Tempo gasto tooexecute acima célula: 11.67 segundos

### <a name="cache-objects-in-memory"></a>Armazenar objetos em cache na memória
tempo Olá para treinamento e teste de algoritmos ML pode ser reduzido ao armazenar em cache o quadro de dados de entrada hello objetos usados para classificação, regressão e recursos de escala.

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

**SAÍDA** 

Tempo gasto tooexecute acima célula: 0,13 segundos

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Prever se uma gorjeta é paga ou não com modelos de classificação binária
Esta seção mostra como usar três modelos para tarefa de classificação binária Olá de prever se uma dica é pago por uma viagem táxi ou não. modelos de saudação apresentados são:

* Regressão logística 
* Floresta aleatória
* Árvores de Ampliação de Gradiente

Cada seção de código de compilação de modelo é dividida em etapas: 

1. **Modelar os dados de treinamento** com um conjunto de parâmetros
2. **Modelar a avaliação** em um conjunto de dados de teste com métricas
3. **Salvar modelo** no blob para consumo futuro

Vamos mostrar como toodo validação cruzada (VC) com o parâmetro de varredura de duas maneiras:

1. Usando **genérico** código personalizado que pode ser aplicado tooany algoritmo no parâmetro MLlib e tooany define em um algoritmo. 
2. Usando Olá **pySpark função do pipeline de CrossValidator**. Observe que o CrossValidator tem algumas limitações para o Spark 1.5.0: 
   
   * Os modelos de pipeline não podem ser salvos/persistidos para consumo futuro.
   * Não pode ser usado para todos os parâmetros em um modelo.
   * Não pode ser usado para todos os algoritmos MLlib.

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a>Genérico cruzado validação e limpeza hyperparameter usado com o algoritmo de regressão logística Olá para classificação binária
código de saudação nesta seção mostra como tootrain, avaliar e salvar um modelo de regressão logística com [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi o conjunto de dados de processamento e passagens. modelo de saudação é treinado usando cruzada limpeza hyperparameter implementado com código personalizado que pode ser aplicado tooany de saudação MLlib algoritmos de aprendizado e validação (CV).   

> [!NOTE]
> execução de saudação desse código personalizado do VC pode levar vários minutos.
> 
> 

**Treinar o modelo de regressão logística hello usando VC e limpeza de hyperparameter**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SAÍDA**

Coeficientes: [0,0082065285375, -0,0223675576104, -0,0183812028036, -3,48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]

Interceptação: -0,0111216486893

Tempo gasto tooexecute acima célula: 14.43 segundos

**Avaliar o modelo de classificação binária Olá com métricas padrão**

código Olá nesta seção mostra como tooevaluate uma regressão logística de modelo em um teste-conjunto de dados, incluindo um gráfico de saudação curva ROC.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

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

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SAÍDA**

Área sob PR = 0,985336538462

Área sob ROC = 0,983383274312

Estatísticas de resumo

Precisão = 0,984174341679

Cancelamento = 0,984174341679

Pontuação F1 = 0,984174341679

Tempo gasto tooexecute acima célula: 2,67 segundos

**Plote curva ROC hello.**

Olá *predictionAndLabelsDF* é registrado como uma tabela, *tmp_results*, na célula de saudação anterior. *tmp_results* pode ser usado toodo consultas e resultados de saída em Olá sqlResults-quadro de dados para plotar. Aqui está o código de saudação.

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Aqui está o previsões de toomake código hello e Olá plotagem ROC curva.

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
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


**SAÍDA**

![Curva ROC de regressão logística de abordagem genérica](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

**Persistir o modelo em um blob para consumo futuro**

código Olá nesta seção mostra como modelo de regressão logística de saudação toosave para consumo.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


**SAÍDA**

Tempo gasto tooexecute acima célula: 34.57 segundos

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a>Usar a função de pipeline CrossValidator da MLlib com o modelo de regressão logística (Regressão elástica)
código de saudação nesta seção mostra como tootrain, avaliar e salvar um modelo de regressão logística com [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi o conjunto de dados de processamento e passagens. modelo de saudação é treinado usando validação cruzada (VC) e limpeza hyperparameter implementados com hello MLlib CrossValidator função de pipeline para VC com varredura de parâmetro.   

> [!NOTE]
> execução de saudação do código MLlib VC pode levar vários minutos.
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**SAÍDA**

Tempo gasto tooexecute acima célula: 107.98 segundos

**Plote curva ROC hello.**

Olá *predictionAndLabelsDF* é registrado como uma tabela, *tmp_results*, na célula de saudação anterior. *tmp_results* pode ser usado toodo consultas e resultados de saída em Olá sqlResults-quadro de dados para plotar. Aqui está o código de saudação.

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

Aqui está a curva ROC Olá código tooplot hello.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
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


**SAÍDA**

![Curva ROC de regressão logística usando CrossValidator da MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a>Classificação de floresta aleatória
código Olá nesta seção mostra como tootrain, avaliar e salvar uma regressão de floresta aleatório que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi viagem e passagens conjunto de dados.

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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


**SAÍDA**

Área sob ROC = 0,985336538462

Tempo gasto tooexecute acima célula: 26.72 segundos

### <a name="gradient-boosting-trees-classification"></a>Classificação de árvores de ampliação de gradiente
código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de árvores de ampliação gradiente que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi viagem e passagens conjunto de dados.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
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

**SAÍDA**

Área sob ROC = 0,985336538462

Tempo gasto tooexecute acima célula: 28.13 segundos

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a>Prever valores de gorjetas com modelos de regressão (não usando CV)
Esta seção mostra como usar três modelos para tarefa de regressão Olá: prever Olá dica quantidade pagada para uma viagem de táxi com base em outros recursos de dica. modelos de saudação apresentados são:

* Regressão linear regularizada
* Floresta aleatória
* Árvores de Ampliação de Gradiente

Esses modelos foram descritos na introdução de saudação. Cada seção de código de compilação de modelo é dividida em etapas: 

1. **Modelar os dados de treinamento** com um conjunto de parâmetros
2. **Modelar a avaliação** em um conjunto de dados de teste com métricas
3. **Salvar modelo** no blob para consumo futuro   

> Observação do AZURE: As validação cruzada não é usada com três modelos de regressão Olá nesta seção, pois isso foi mostrado em detalhes para modelos de regressão logística hello. Um exemplo que mostra como toouse VC com Elástico Net para regressão linear é fornecida no hello Apêndice deste tópico.
> 
> Observação do AZURE: Em nossa experiência, pode haver problemas com convergência de LinearRegressionWithSGD modelos e parâmetros necessário toobe alterado/otimizado cuidadosamente para obter um modelo válido. O dimensionamento de variáveis ajuda significativamente com a convergência. Elástico regressão net, mostrado Olá apêndice toothis tópico, também pode ser usado em vez de LinearRegressionWithSGD.
> 
> 

### <a name="linear-regression-with-sgd"></a>Regressão linear com SGD
Olá código nesta seção mostra como toouse dimensionado recursos tootrain uma regressão linear usa descendente do gradiente estocástico (SGD) para a otimização, e como tooscore, avaliar e Salvar modelo Olá no armazenamento de Blob do Azure (WASB).

> [!TIP]
> Em nossa experiência, pode haver problemas com convergência de saudação de LinearRegressionWithSGD modelos e parâmetros necessário toobe alterado/otimizado cuidadosamente para obter um modelo válido. O dimensionamento de variáveis ajuda significativamente com a convergência.
> 
> 

    # LINEAR REGRESSION WITH SGD 

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

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**SAÍDA**

Coeficientes: [0,0141707753435, -0,0252930927087, -0,0231442517137, 0,247070902996, 0,312544147152, 0,360296120645, 0,0122079566092, -0,00456498588241, -0,0898228505177, 0,0714046248793, 0,102171263868, 0,100022455632, -0,00289545676449, -0,00791124681938, 0,54396316518, -0,536293513569, 0,0119076553369, -0,0173039244582, 0,0119632796147, 0,00146764882502]

Interceptação: 0,854507624459

RMSE = 1,23485131376

R-sqr = 0,597963951127

Tempo gasto tooexecute acima célula: 38.62 segundos

### <a name="random-forest-regression"></a>Regressão de Floresta Aleatória
código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de floresta aleatório que prevê a quantidade de dica de saudação dados de viagem táxi NYC.   

> [!NOTE]
> A validação cruzada com o parâmetro de varredura usando código personalizado é fornecida no Apêndice hello.
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

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

**SAÍDA**

RMSE = 0,931981967875

R-sqr = 0,733445485802

Tempo gasto tooexecute acima célula: 25.98 segundos

### <a name="gradient-boosting-trees-regression"></a>Regressão de árvores de ampliação de gradiente
código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de árvores de ampliação gradiente que prevê a quantidade de dica de saudação dados de viagem táxi NYC.

**Treinar e avaliar**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SAÍDA**

RMSE = 0,928172197114

R-sqr = 0,732680354389

Tempo gasto tooexecute acima célula: 20.9 segundos

**Plotar**

*tmp_results* é registrado como uma tabela Hive na célula anterior hello. Resultados da tabela de saudação são saída Olá *sqlResults* quadro de dados para plotar. Aqui está o código de saudação

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Aqui está a dados Olá código tooplot hello usando Olá Jupyter server.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a>Apêndice: Tarefas de regressão adicionais usando a validação cruzada com limpezas de parâmetro
Este apêndice contém mostrando código como toodo VC usando net Elástico para regressão linear e como toodo VC com parâmetro de varredura usando código personalizado para regressão de floresta aleatório.

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a>Validação cruzada usando a rede elástica para a regressão linear
código Olá nesta seção mostra como toodo cruzada validação usando elástica net para regressão linear e como tooevaluate Olá modelo com base em dados de teste.

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SAÍDA**

Tempo gasto tooexecute acima célula: 161.21 segundos

**Avaliar com a métrica R-SQR**

*tmp_results* é registrado como uma tabela Hive na célula anterior hello. Resultados da tabela de saudação são saída Olá *sqlResults* quadro de dados para plotar. Aqui está o código de saudação

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


Aqui está a saudação código toocalculate sqr R.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


**SAÍDA**

R-sqr = 0,619184907088

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a>Validação cruzada com limpeza de parâmetro usando o código personalizado para a regressão de floresta aleatória
código Olá nesta seção mostra como toodo validação cruzada com varredura de parâmetro usando código personalizado para regressão de floresta aleatório e como tooevaluate Olá modelo com base em dados de teste.

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**SAÍDA**

RMSE = 0,906972198262

R-sqr = 0,740751197012

Tempo gasto tooexecute acima célula: 69.17 segundos

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a>Limpar objetos da memória e imprimir os locais de modelo
Use `unpersist()` toodelete objetos armazenados em cache na memória.

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

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


**SAÍDA**

PythonRDD[122] em RDD em PythonRDD.scala:43

* * Impressão caminho toomodel arquivos toobe usado no bloco de anotações de consumo de saudação. * * tooconsume e pontuação um independente de-conjunto de dados, você precisa toocopy e cole esses nomes de arquivo hello "Bloco de anotações de consumo".

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**SAÍDA**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"

## <a name="whats-next"></a>O que vem a seguir?
Agora que você criou modelos de classificação e regressão com hello Spark MlLib, você está pronto toolearn como tooscore e avaliar esses modelos.

**Consumo de modelo:** toolearn como tooscore e avaliar modelos de classificação e regressão de saudação criados neste tópico, consulte [pontuação e avaliar modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md).

