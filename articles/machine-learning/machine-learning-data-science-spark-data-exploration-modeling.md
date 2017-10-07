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
# <a name="data-exploration-and-modeling-with-spark"></a>Modelagem e exploração de dados com Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Este passo a passo usa a exploração de dados do HDInsight Spark toodo e classificação binária e regressão tarefas de modelagem em uma amostra de saudação NYC táxi viagem e passagens de conjunto de dados de 2013.  Lhe orienta pelas etapas de saudação do hello [processo de ciência de dados](http://aka.ms/datascienceprocess), cluster de ponta a ponta, usando um HDInsight Spark para processamento e modelos de dados e Olá Olá toostore de blobs do Azure. processo de saudação explora e visualiza os dados transferidos de um Blob de armazenamento do Azure e, em seguida, prepara Olá dados toobuild modelos de previsão. Esses modelos são compilados usando classificação binária do toodo Olá Spark MLlib Kit de ferramentas e tarefas de modelagem de regressão.

* Olá **classificação binária** tarefa é toopredict ou não uma dica é pago para viagem hello. 
* Olá **regressão** tarefa é toopredict Olá Olá dica com base em outros recursos de dica. 

os modelos de saudação que usamos incluem gradientes árvores aumentadas, florestas aleatórias e regressão logística e linear:

* [Regressão linear com SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) é um modelo de regressão linear que usa um método descendente gradiente Estocástico (SGD) e para a otimização e recurso de dimensionamento quantidades de dica de saudação toopredict pago. 
* [Regressão logística com LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) ou regressão "logit", é um modelo de regressão que pode ser usado quando a variável dependente de saudação é categórica toodo a classificação de dados. LBFGS é um algoritmo de otimização de quase-Newton que aproxima o algoritmo Broyden – Fletcher – Goldfarb – Shanno (BFGS) de saudação usando uma quantidade limitada de memória do computador e que é amplamente usada no aprendizado de máquina.
* [Florestas aleatórias](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) são conjuntos de árvores de decisão.  Elas combinam muitas decisões árvores tooreduce Olá risco de superajuste. Florestas aleatórias são usadas para classificação e regressão e podem lidar com recursos categóricos e configuração de classificação multiclasse toohello podem ser estendidas. Eles não exigem recurso escala e são capazes de toocapture não linearidades e interações de recurso. Florestas aleatórias são um dos modelos de classificação e regressão de aprendizado de máquina mais bem-sucedida de saudação.
* [GBTs (árvores com aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão. Árvores de decisão de treinar GBTs iterativamente toominimize uma função de perda. GBTs são usados para classificação e regressão pode lidar com recursos categóricos, não requerem o dimensionamento de recurso e são capazes de toocapture não linearidades e interações de recursos. Elas também podem ser usadas em uma configuração de classificação multiclasse.

etapas de modelagem Olá também contêm código que mostra como tootrain, avaliar e salvar cada tipo de modelo. Python foi usado toocode Olá solução e tooshow Olá relevantes gráficos.   

> [!NOTE]
> Embora o Kit de ferramentas do hello Spark MLlib toowork projetado em grandes conjuntos de dados, um exemplo relativamente pequeno (aproximadamente 30 Mb usando 170 mil linhas, cerca de 0,1% de saudação original NYC dataset) é usado aqui para sua conveniência. Exercício Olá fornecido aqui é executado com eficiência (em cerca de 10 minutos) em um cluster de HDInsight com 2 nós de trabalho. Olá mesmo código, com pequenas modificações, pode ser usado tooprocess-conjuntos de dados maiores, com as modificações apropriadas para o cache de dados na memória e alterar o tamanho do cluster hello.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Você precisa de uma conta do Azure e um Spark 1.6 (ou 2.0 Spark) cluster HDInsight toocomplete este passo a passo. Consulte Olá [visão geral de ciência de dados usando o Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md) para obter instruções sobre como toosatisfy esses requisitos. Esse tópico também contém uma descrição da saudação dados NYC 2013 táxi usados aqui e instruções sobre como tooexecute código de um bloco de anotações do Jupyter no cluster do Spark hello. 

## <a name="spark-clusters-and-notebooks"></a>Blocos de notas e clusters do Spark
As etapas de configuração e o código são fornecidos neste passo a passo para usar um HDInsight Spark 1.6. Porém, notebooks Jupyter são fornecidos tanto para o HDInsight Spark 1.6 quanto para os clusters Spark 2.0. Uma descrição da saudação toothem de anotações e links são fornecidos no hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para o repositório do GitHub Olá que os contém. Além disso, Olá código aqui e em blocos de anotações Olá vinculado é genérico e deve funcionar em qualquer cluster do Spark. Se você não estiver usando o HDInsight Spark, as etapas de configuração e gerenciamento de cluster Olá podem ser ligeiramente diferentes da que é mostrado aqui. Para sua conveniência, aqui estão os links de saudação blocos de anotações do Jupyter toohello para Spark 1.6 (toobe executar no kernel do pySpark de saudação do servidor de Jupyter Notebook de saudação) e o Spark 2.0 (toobe executar no kernel do pySpark3 de saudação do servidor de Jupyter Notebook de saudação):

### <a name="spark-16-notebooks"></a>Blocos de notas Spark 1.6

[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fornece informações sobre como tooperform de exploração de dados, modelagem e pontuação com vários algoritmos diferentes.

### <a name="spark-20-notebooks"></a>Blocos de notas Spark 2.0
tarefas de classificação e regressão de saudação que são implementadas usando um cluster Spark 2.0 são blocos de anotações separado e bloco de anotações de classificação Olá usa um conjunto de dados diferente:

- [Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este arquivo fornece informações sobre como tooperform a exploração de dados, modelagem e pontuação no Spark 2.0 clusters usando Olá trip NYC táxi e passagens-conjunto de dados descrito [aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Este bloco de anotações pode ser um bom ponto de partida para explorar rapidamente código Olá que fornecemos para Spark 2.0. Para um bloco de anotações mais detalhado analisa Olá dados NYC táxi, consulte o próximo bloco de anotações de saudação nesta lista. Consulte as notas de saudação seguinte lista que comparam esses blocos de anotações. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): esse arquivo mostra como tooperform dados disputa (operações Spark SQL e dataframe), a exploração, modelagem e pontuação usando Olá trip NYC táxi e passagens conjunto de dados descrito [ aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): esse arquivo mostra como tooperform dados disputa (operações Spark SQL e dataframe), a exploração, modelagem e pontuação usando Olá conhecida saída em tempo de aérea conjunto de dados de 2011 e 2012. Podemos integrada Olá aérea dataset com hello a toomodeling de anteriores de dados (por exemplo, windspeed, temperatura, altitude etc.) do aeroporto clima, para que esses recursos de tempo podem ser incluídos no modelo de saudação.

<!-- -->

> [!NOTE]
> Olá aérea dataset foi adicionado toohello 2.0 Spark notebooks toobetter ilustram o uso de saudação de algoritmos de classificação. Consulte Olá links para obter informações sobre o conjunto de dados de saída em tempo de passagens áreas e conjunto de dados de tempo a seguir:

>- Dados de partidas no horário em aeroportos: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Dados de clima aeroporto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
Olá Spark 2.0 blocos de anotações Olá táxi NYC e conjuntos de dados de atraso de voo de aérea podem levar 10 minutos ou mais toorun (dependendo do tamanho de saudação do cluster HDI). primeiro notebook no hello acima da lista Hello mostra muitos aspectos de exploração de dados hello, visualização e ML do modelo de treinamento em um bloco de anotações que utiliza menos toorun de tempo com convertidos NYC conjunto de dados, no qual Olá táxi e passagens arquivos tem sido previamente Unidos: [ Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) este bloco de anotações leva uma quantidade menor tempo toofinish (2-3 minutos) e pode ser um bom ponto de partida para explorar rapidamente código Olá temos fornecido para Spark 2.0. 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
descrições de saudação abaixo são relacionada toousing Spark 1.6. Para versões do Spark 2.0, use anotações Olá descritos e no link acima. 

<!-- -->

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
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a>Importar bibliotecas
A instalação também requer a importação das bibliotecas necessárias. Definir contexto spark e importar bibliotecas necessárias com hello código a seguir:

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


### <a name="preset-spark-context-and-pyspark-magics"></a>Contexto predefinido do Spark e palavras mágicas do PySpark
kernels PySpark de saudação que são fornecidos com blocos de anotações do Jupyter tem um contexto de predefinição. Portanto não é necessário tooset Olá Spark ou Hive contextos explicitamente antes de começar a trabalhar com o aplicativo hello que você está desenvolvendo. Esses contextos estão disponíveis para você por padrão. Esses contextos são:

* sc - para o Spark 
* sqlContext - para o Hive

Olá PySpark kernel fornece algumas predefinidas "magics", que são comandos especiais que podem ser chamados com % %. Há dois comandos que são usados nesses exemplos de código.

* **% % local** Especifica que o código de saudação em linhas subsequentes é toobe executado localmente. O código deve ser um código Python válido.
* **% % -o do sql <variable name>**  executa uma consulta de Hive em Olá sqlContext. Se Olá -o parâmetro for passado, resultado de saudação de consulta de saudação é mantido no Olá % % contexto Python local como um DataFrame Pandas.

Para obter mais informações sobre kernels Olá para blocos de anotações do Jupyter e hello predefinidas "magics" que eles fornecem, consulte [clusters Kernels disponíveis para blocos de anotações do Jupyter com Linux do HDInsight Spark no HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="data-ingestion-from-public-blob"></a>Ingestão de dados de blob público
Olá primeira etapa no processo de ciência de dados Olá é tooingest Olá dados toobe analisado de fontes de onde é reside em seu ambiente de modelagem e exploração de dados. ambiente de saudação é Spark neste passo a passo. Esta seção contém Olá código toocomplete uma série de tarefas:

* Olá toobe de exemplo de dados modelado de ingestão
* ler no conjunto de dados entrada hello (armazenado como um arquivo. tsv)
* formato e dados saudação normal
* criar e armazenar objetos em cache (RDDs ou quadros de dados) na memória
* registrá-lo como uma tabela temporária no contexto do SQL.

Este é o código de saudação para ingestão de dados.

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 51.72 segundos

## <a name="data-exploration--visualization"></a>Visualização e exploração de dados
Quando dados saudação foi colocados no Spark, hello próxima etapa no processo de ciência de dados Olá é toogain de compreensão mais profunda dos dados Olá por meio de exploração e visualização. Nesta seção, podemos examinar dados de táxi hello usando consultas SQL e recursos em potencial e variáveis de destino de saudação de plotagem para inspeção visual. Especificamente, podemos plotar frequência Olá passageiro de contagens de em viagens táxi, a frequência de saudação de quantidades de ponta e como dicas variam de acordo com o tipo e a quantidade de pagamento.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Plotar um histograma de frequências de contagem de passageiro no exemplo hello de viagens táxi
Esse código e trechos de código subsequentes usam exemplo do SQL tooquery magic hello e os dados de saudação do tooplot magic local.

* **Magic SQL (`%%sql`)** hello HDInsight PySpark kernel dá suporte a fácil embutido HiveQL consultas em relação a saudação sqlContext. saudação (-o VARIABLE_NAME) argumento persiste saída Olá de consulta do SQL hello como um DataFrame Pandas no servidor do Jupyter hello. Isso significa que ele está disponível no modo local hello.
* Olá  **`%%local` mágico** é usado toorun código localmente no servidor de Jupyter hello, que é Olá um nó principal do cluster do HDInsight hello. Normalmente, você usa `%%local` magic em conjunto com hello `%%sql` magic com o parâmetro -o. parâmetro -o de Hello persistir Olá saída de hello SQL consulta localmente e, em seguida, % % magic local irá disparar o próximo conjunto de saudação do toorun de trecho de código localmente contra a saída da saudação de consultas SQL Olá persistido localmente

saída de Hello é visualizada automaticamente depois de executar código hello.

Essa consulta recupera viagens Olá por contagem de passageiro. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

Esse código cria um quadro de dados local de saída da consulta hello e plota dados saudação. Olá `%%local` mágico cria um local-quadro de dados, `sqlResults`, que pode ser usado para plotar com matplotlib. 

> [!NOTE]
> Essas palavras mágicas do PySpark são usadas várias vezes neste passo a passo. Se a quantidade de saudação de dados for grande, você deve exemplo toocreate um quadro de dados que pode caber na memória local.
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Aqui está viagens de Olá Olá código tooplot por passageiro contagens

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

**SAÍDA:**

![Frequência de corridas por contagem de passageiros](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

Você pode selecionar entre vários tipos diferentes de visualizações (tabela, pizza, linha, área ou barra) usando Olá **tipo** botões de menu no bloco de anotações de saudação. gráfico de barras Olá é mostrado aqui.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Plote um histograma de valores de gorjetas e como o valor das gorjetas varia pelas tarifas e contagens de passageiros.
Use um banco de dados consulta toosample do SQL.

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


Esta célula código usa Olá consulta toocreate três gráficos Olá de dados do SQL.

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


**SAÍDA:** 

![Distribuição de valores de gorjetas](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Valor de gorjeta por contagem de passageiros](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Valor de gorjeta por valor de tarifa](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Engenharia de recursos, transformação e preparação de dados para a modelagem
Esta seção descreve e fornece código Olá para procedimentos usados tooprepare dados para uso em modelagem ML. Ele mostra como as tarefas de saudação toodo a seguir:

* Criar um novo recurso reunindo horários em blocos de tempo de tráfego
* Indexar e codificar recursos categóricos
* Criar objetos de ponto rotulado para entrada em funções de ML
* Cria uma amostragem aleatória de subgrupos de dados hello e dividi-lo em treinamento e conjuntos de teste
* Dimensionamento de recursos
* Armazenar objetos em cache na memória

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Criar um novo recurso reunindo horários em blocos de tempo de tráfego
Esse código mostra como toocreate um novo recurso guardando horas em vez de tráfego buckets e, em seguida, como toocache Olá resultante quadro de dados na memória. Onde resiliente distribuídas conjuntos de dados (RDDs) e quadros de dados são usados repetidamente, cache leva tooimproved tempos de execução. Da mesma forma, cache RDDs e quadros de dados em vários estágios Olá passo a passo. 

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

**SAÍDA:** 

126050

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a>Indexar e codificar recursos categóricos para entrada em funções de modelagem
Esta seção mostra como tooindex ou codificar recursos categóricos para entrada em Olá funções da modelagem. Olá modelagem e prever a funções de MLlib exigem recursos com entrada de dados categóricos toobe indexado ou codificado toouse anterior. Dependendo do modelo de hello, você precisa tooindex ou codificá-los de maneiras diferentes:  

* **Baseado na árvore de modelagem** requer toobe categorias codificada como valores numéricos (por exemplo, um recurso com três categorias pode ser codificado com 0, 1, 2). Isso é fornecido pela função [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) do MLlib. Essa função codifica uma coluna de cadeia de caracteres da coluna de tooa de rótulos de índices de rótulo que são ordenados por frequências de rótulo. Embora indexado com valores numéricos para entrada e manipulação de dados, os algoritmos com base em árvore Olá podem ser tootreat especificado-los adequadamente como categorias. 
* **Modelos de regressão Linear e logística** exigem hot uma codificação, onde, por exemplo, um recurso com três categorias pode ser expandido em três colunas de recurso, com cada contendo 0 ou 1 dependendo da categoria de saudação de uma observação. Fornece MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) toodo hot uma codificação de função. Este codificador mapeia uma coluna da coluna de tooa de índices de rótulo de vetores de binários, no máximo um único um valor. Essa codificação permite que os algoritmos que esperam recursos com valores numéricos, como a regressão logística, recursos de toocategorical toobe aplicado.

Aqui está o hello tooindex de código e codificar recursos categóricos:

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 1.28 segundos

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Criar objetos de ponto rotulado para entrada em funções de ML
Esta seção contém o código que mostra como tipo de dados de texto categóricos tooindex como um rótulo de ponto de dados e codificação-lo para que ele possa ser usado tootrain e teste MLlib Regressão logística e outros modelos de classificação. Objetos de ponto rotulados são RDDs (Conjuntos de Dados Resilientes Distribuídos) formatados de uma maneira que é necessária como dados de entrada pela maioria dos algoritmos de ML no MLlib. Um [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) é um vetor local, denso ou esparso, associado a um rótulo/resposta.  

Esta seção contém o código que mostra como dados de texto categóricos tooindex como um [rotulada ponto](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) tipo de dados e codificá-lo para que ele possa ser usado tootrain e teste MLlib Regressão logística e outros modelos de classificação. Objetos de ponto de rotulado são RDDs (Conjuntos de Dados Resilientes Distribuídos) que consistem em um rótulo (variável de destino/resposta) e um vetor de recurso. Esse formato é necessário como entrada para muitos algoritmos de ML no MLlib.

Aqui está o hello tooindex de código e codificar os recursos de texto para classificação binária.

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
Esse código cria uma amostragem aleatória de dados de saudação (25% é usado aqui). Embora não seja necessário para este exemplo devido toohello tamanho do conjunto de dados hello, demonstraremos como você pode criar amostra aqui para saber como toouse-lo para o seu próprio problema quando necessário. Quando as amostras são grandes, isso pode economizar um tempo significativo durante o treinamento de modelos. Em seguida, dividiremos exemplo hello em uma parte de treinamento (75% aqui) e um teste toouse de parte (25% aqui) de classificação e modelagem de regressão.

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 0.24 segundos

### <a name="feature-scaling"></a>Dimensionamento de recursos
Dimensionamento de recurso, também conhecido como normalização de dados assegura que os recursos com valores amplamente distribuídos são não fornecido excessiva pesar na função objetivo hello. código para o recurso de dimensionamento Hello usa Olá [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) variação de toounit tooscale Olá recursos. Ele é fornecido por MLlib para uso na regressão linear com SGD (Stochastic Gradient Descent), um algoritmo popular de treinamento de uma grande variedade de outros modelos de aprendizado de máquina, como regressões regularizadas ou SVM (máquinas de vetor de suporte).

> [!NOTE]
> Encontramos Olá LinearRegressionWithSGD algoritmo toobe toofeature confidencial dimensionamento.
> 
> 

Aqui está a variáveis de tooscale Olá código para uso com o algoritmo SGD linear Olá regularizada.

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

**SAÍDA:**

Tempo gasto tooexecute acima célula: 13.17 segundos

### <a name="cache-objects-in-memory"></a>Armazenar objetos em cache na memória
tempo Olá para treinamento e teste de algoritmos ML podem ser reduzidos pelo cache de objetos de quadro de dados de entrada hello usados para classificação, regressão, e recursos de escala.

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

**SAÍDA:** 

Tempo gasto tooexecute acima célula: 0,15 segundos

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Prever se uma gorjeta é paga ou não com modelos de classificação binária
Esta seção mostra como usar três modelos para tarefa de classificação binária Olá de prever se uma dica é pago por uma viagem táxi ou não. modelos de saudação apresentados são:

* Regressão logística regularizada 
* Modelo de floresta aleatória
* Árvores de Ampliação de Gradiente

Cada seção de código de compilação de modelo é dividida em etapas: 

1. **Modelar os dados de treinamento** com um conjunto de parâmetros
2. **Modelar a avaliação** em um conjunto de dados de teste com métricas
3. **Salvar modelo** no blob para consumo futuro

### <a name="classification-using-logistic-regression"></a>Classificação usando regressão logística
código de saudação nesta seção mostra como tootrain, avaliar e salvar um modelo de regressão logística com [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi o conjunto de dados de processamento e passagens.

**Treinar o modelo de regressão logística hello usando VC e limpeza de hyperparameter**

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


**SAÍDA:** 

Coeficientes: [0,0082065285375, -0,0223675576104, -0,0183812028036, -3,48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]

Interceptação: -0,0111216486893

Tempo gasto tooexecute acima célula: 14.43 segundos

**Avaliar o modelo de classificação binária Olá com métricas padrão**

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

**SAÍDA:** 

Área sob PR = 0,985297691373

Área sob ROC = 0,983714670256

Estatísticas de resumo

Precisão = 0,984304060189

Recuperação = 0,984304060189

Pontuação F1 = 0,984304060189

Tempo gasto tooexecute acima célula: 57.61 segundos

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


**SAÍDA:**

![curve.png de ROC de regressão logística](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a>Classificação de floresta aleatória
código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de floresta aleatório que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi viagem e passagens conjunto de dados.

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

**SAÍDA:**

Área sob ROC = 0,985297691373

Tempo gasto tooexecute acima célula: 31.09 segundos

### <a name="gradient-boosting-trees-classification"></a>Classificação de árvores de ampliação de gradiente
código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de árvores de ampliação gradiente que prevê se ou não uma dica é pago por uma viagem Olá NYC táxi viagem e passagens conjunto de dados.

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


**SAÍDA:**

Área sob ROC = 0,985297691373

Tempo gasto tooexecute acima célula: 19.76 segundos

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a>Prever valores de gorjetas para corridas de táxi com modelos de regressão
Esta seção mostra como usar três modelos para tarefa de regressão de saudação de prever a quantidade de saudação de dica Olá pagada para uma viagem de táxi com base em outros recursos de dica. modelos de saudação apresentados são:

* Regressão linear regularizada
* Floresta aleatória
* Árvores de Ampliação de Gradiente

Esses modelos foram descritos na introdução de saudação. Cada seção de código de compilação de modelo é dividida em etapas: 

1. **Modelar os dados de treinamento** com um conjunto de parâmetros
2. **Modelar a avaliação** em um conjunto de dados de teste com métricas
3. **Salvar modelo** no blob para consumo futuro

### <a name="linear-regression-with-sgd"></a>Regressão linear com SGD
Olá código nesta seção mostra como toouse dimensionado recursos tootrain uma regressão linear usa descendente do gradiente estocástico (SGD) para a otimização, e como tooscore, avaliar e Salvar modelo Olá no armazenamento de Blob do Azure (WASB).

> [!TIP]
> Em nossa experiência, pode haver problemas com convergência de saudação de LinearRegressionWithSGD modelos e parâmetros necessário toobe alterado/otimizado cuidadosamente para obter um modelo válido. O dimensionamento de variáveis ajuda significativamente com a convergência. 
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

**SAÍDA:**

Coeficientes: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]

Interceptação: 0,853872718283

RMSE = 1,24190115863

R-sqr = 0,608017146081

Tempo gasto tooexecute acima célula: 58.42 segundos

### <a name="random-forest-regression"></a>Regressão de Floresta Aleatória
código Olá nesta seção mostra como tootrain, avaliar e salvar uma regressão de floresta aleatório que prevê a quantidade de dica de saudação dados de viagem táxi NYC.

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

**SAÍDA:**

RMSE = 0,891209218139

R-sqr = 0,759661334921

Tempo gasto tooexecute acima célula: 49.21 segundos

### <a name="gradient-boosting-trees-regression"></a>Regressão de árvores de ampliação de gradiente
código Olá nesta seção mostra como tootrain, avaliar e salvar um modelo de árvores de ampliação gradiente que prevê a quantidade de dica de saudação dados de viagem táxi NYC.

**Treinar e avaliar**

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

**SAÍDA:**

RMSE = 0,908473148639

R-sqr = 0,753835096681

Tempo gasto tooexecute acima célula: 34.52 segundos

**Plotar**

*tmp_results* é registrado como uma tabela Hive na célula anterior hello. Resultados da tabela de saudação são saída Olá *sqlResults* quadro de dados para plotar. Aqui está o código de saudação

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

Aqui está a dados Olá código tooplot hello usando Olá Jupyter server.

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


**SAÍDA:**

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a>Limpar objetos da memória
Use `unpersist()` toodelete objetos armazenados em cache na memória.

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a>Locais de armazenamento de registro de modelos de saudação para consumo e pontuação
tooconsume e pontuação de um conjunto de dados independente descritas Olá [pontuação e avaliar modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md) tópico, você precisa toocopy e colar esses arquivos nomes que contêm modelos de saudação salvo criados aqui em hello Anotações do Jupyter de consumo. Aqui está a saudação código tooprint out toomodel arquivos Olá caminhos que você precisa existe.

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**SAÍDA**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"

## <a name="whats-next"></a>O que vem a seguir?
Agora que você criou modelos de classificação e regressão com hello Spark MlLib, você está pronto toolearn como tooscore e avaliar esses modelos. Olá avançados de exploração de dados e modelagem unidades notebook mais profundo em incluindo a validação cruzada, parâmetro hyper varredura e avaliação de modelo. 

**Consumo de modelo:** toolearn como tooscore e avaliar modelos de classificação e regressão de saudação criados neste tópico, consulte [pontuação e avaliar modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md).

**Validação cruzada e limpeza de hiperparâmetro**: confira [Modelagem e exploração de dados avançados com o Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) para saber como os modelos podem ser treinados usando a validação cruzada e a limpeza de hiperparâmetro

