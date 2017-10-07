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
# <a name="data-science-using-scala-and-spark-on-azure"></a>Ciência de Dados usando o Scala e o Spark no Azure
Este artigo mostra como toouse Scala para tarefas de aprendizado de máquina supervisionado com hello MLlib escalonável Spark e Spark ML pacotes em um cluster Spark no HDInsight. Orienta você pelas tarefas de saudação que constituem Olá [processo de ciência de dados](http://aka.ms/datascienceprocess): inclusão de dados e exploração, visualização, engenharia de recurso, modelagem e consumo de modelo. modelos Olá artigo Olá incluem Regressão logística e linear, florestas aleatórias e árvores ampliadas gradiente (GBTs), além de tootwo comum supervisionado tarefas de aprendizado de máquina:

* Problema de regressão: previsão do valor de dica de saudação ($) para uma viagem de táxi
* Classificação binária: previsão da gorjeta ou não (1/0) para uma corrida de táxi

processo de modelagem de saudação requer treinamento e avaliação em um conjunto de dados de teste e métricas de precisão relevantes. Neste artigo, você pode aprender como toostore esses modelos no armazenamento de BLOBs do Azure e como tooscore e avaliar o desempenho previsível. Este artigo também aborda hello mais avançados tópicos de como toooptimize modelos usando validação cruzada e parâmetro hyper limpeza. dados de saudação usados são um exemplo hello 2013 NYC táxi viagem e passagens do conjunto de dados disponível no GitHub.

[Scala](http://www.scala-lang.org/), um idioma com base na máquina virtual Java com hello, integra conceitos de linguagem funcional e orientada a objeto. É uma linguagem escalonável toodistributed adequado de processamento na nuvem Olá, e é executado no Azure Spark clusters.

[Spark](http://spark.apache.org/) é tooboost Olá desempenho de aplicativos de análise de dados grandes do processamento de uma estrutura de processamento paralelo de código-fonte aberto que dá suporte na memória. mecanismo de processamento do Spark Olá é construído para velocidade, facilidade de uso e análise sofisticada. As funcionalidades de computação distribuídas na memória do Spark fazem dele uma boa escolha para algoritmos iterativos em cálculos de gráfico e aprendizado de máquina. Olá [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) pacote fornece um conjunto uniforme de APIs de alto nível criado com base em dados quadros que podem ajudá-lo a criar e ajustar prática pipelines de aprendizado de máquina. [MLlib](http://spark.apache.org/mllib/) é a biblioteca de aprendizado de máquina escalonável do Spark, que oferece recursos de modelagem ambiente distribuído toothis.

[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) é Olá hospedado no Azure oferta do código-fonte aberto Spark. Também inclui suporte para blocos de anotações do Jupyter Scala no cluster do Spark Olá, e pode executar tootransform Spark SQL de consultas interativas, filtrar e visualizar os dados armazenados no armazenamento de BLOBs do Azure. Olá Scala trechos de código neste artigo que fornecem soluções hello e mostram gráficos relevantes Olá dados de saudação toovisualize executar em blocos de anotações do Jupyter instalados nos clusters do Spark hello. etapas de modelagem Olá nestes tópicos tiver o código que mostra a você como tootrain, avaliar, salvar e consumir cada tipo de modelo.

etapas de instalação Hello e o código neste artigo são para o Azure HDInsight 3.4 Spark 1.6. No entanto, Olá código neste artigo e Olá [Scala de anotações do Jupyter](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) são genéricos e deve funcionar em qualquer cluster Spark. Olá instalação de cluster e etapas de gerenciamento podem ser ligeiramente diferentes da que é mostrado neste artigo, se você não estiver usando o HDInsight Spark.

> [!NOTE]
> Para um tópico que mostra como as tarefas de toocomplete de Python em vez de Scala toouse para um processo de ciência de dados de ponta a ponta, consulte [ciência de dados usando o Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
* Você precisa ter uma assinatura do Azure. Se ainda não tiver uma, [obtenha uma avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Você precisa de uma saudação de toocomplete de cluster Azure HDInsight 3.4 Spark 1.6 procedimentos a seguir. toocreate um cluster, consulte as instruções de saudação em [Introdução: criar o Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Definir tipo de cluster hello e versão em Olá **Selecionar tipo de Cluster** menu.

![Configuração de tipo de cluster do HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

Para obter uma descrição de dados de viagem táxi Olá NYC e instruções sobre como tooexecute código de um bloco de anotações do Jupyter no cluster do Spark hello, consulte a seções relevantes Olá [visão geral de ciência de dados usando o Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md).  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Execute o código de Scala de um bloco de anotações do Jupyter no cluster do Spark Olá
Você pode iniciar um bloco de anotações do Jupyter de saudação portal do Azure. Localizar o cluster do Spark Olá em seu painel e clique tooenter página de gerenciamento de saudação para seu cluster. Em seguida, clique em **painéis do Cluster**e, em seguida, clique em **Jupyter Notebook** tooopen notebook de saudação associada Olá Spark cluster.

![Painel do cluster e notebooks Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

Você também pode acessar blocos de anotações do Jupyter em https://&lt;clustername&gt;.azurehdinsight.net/jupyter. Substituir *clustername* com nome de saudação do cluster. Senha de saudação é necessária para o administrador conta tooaccess Olá Jupyter blocos de anotações.

![Vá tooJupyter notebooks usando o nome do cluster Olá](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

Selecione **Scala** toosee um diretório com alguns exemplos de blocos de anotações predefinidos Olá que use PySpark API. Olá exploração de modelagem e pontuação usando notebook Scala.ipynb que contém exemplos de código Olá para este conjunto de tópicos do Spark está disponível em [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).

Você pode carregar notebook Olá diretamente do GitHub toohello servidor de Jupyter Notebook em seu cluster Spark. Na home page Jupyter, clique em Olá **carregar** botão. No Explorador de arquivos Olá, cole Olá GitHub (conteúdo bruto) URL do bloco de anotações do hello Scala e, em seguida, clique em **abrir**. o bloco de anotações do Hello Scala estará disponível em Olá URL a seguir:

[Exploration-Modeling-and-Scoring-using-Scala.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a>Configuração: contextos predefinidos de Spark e Hive, palavras mágicas Spark e bibliotecas Spark
### <a name="preset-spark-and-hive-contexts"></a>Contextos predefinidos de Spark e Hive
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


kernels do Spark Olá que são fornecidos com blocos de anotações do Jupyter tem contextos predefinidos. Você não precisa tooexplicitly conjunto Olá Spark ou Hive contextos antes de começar a trabalhar com o aplicativo hello que você está desenvolvendo. Olá contextos predefinidos são:

* `sc` para SparkContext
* `sqlContext` para HiveContext

### <a name="spark-magics"></a>Palavras mágicas do Spark
Olá kernel Spark fornece algumas predefinidas "magics", que são comandos especiais que podem ser chamados com `%%`. Dois desses comandos são usados em Olá exemplos de código a seguir.

* `%%local`Especifica que código Olá nas linhas subsequentes será executado localmente. código de saudação deve ser código Scala válido.
* `%%sql -o <variable name>` executa uma consulta do Hive no `sqlContext`. Se hello `-o` parâmetro for passado, o resultado de saudação de consulta de saudação é mantido no hello `%%local` Scala contexto como um quadro de dados Spark.

Para obter mais informações sobre kernels Olá para blocos de anotações do Jupyter e seus predefinido "magics" que você chamar com `%%` (por exemplo, `%%local`), consulte [Kernels disponíveis para blocos de anotações do Jupyter com HDInsight Spark Linux clusters em HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

### <a name="import-libraries"></a>Importar bibliotecas
Importar Olá Spark, MLlib e outras bibliotecas que você precisará usando Olá código a seguir.

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


## <a name="data-ingestion"></a>Ingestão de dados
primeira etapa Olá Olá processo de ciência de dados é dados de saudação tooingest que você deseja tooanalyze. Colocar dados saudação de fontes externas ou sistemas onde ele reside em seu ambiente de modelagem e exploração de dados. Neste artigo, você ingestão de dados de saudação são um exemplo de 0,1% que se unidas Olá táxi viagem e passagens do arquivo de (armazenado como um arquivo. tsv). ambiente de modelagem e exploração de dados Olá é Spark. Esta seção contém Olá Olá de toocomplete código série de tarefas a seguir:

1. Definir os caminhos de diretório para o armazenamento de dados e de modelos.
2. Ler no conjunto de dados entrada hello (armazenado como um arquivo. tsv).
3. Defina um esquema para dados hello e limpar hello.
4. Criar um quadro de dados limpo e armazená-lo em cache na memória.
5. Registre dados saudação como uma tabela temporária no SQLContext.
6. Consultar a tabela de saudação e importar resultados de saudação para um quadro de dados.

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a>Definir caminhos de diretório para locais de armazenamento no armazenamento de Blobs do Azure
Spark pode ler e gravar tooAzure armazenamento de Blob. Você pode usar Spark tooprocess qualquer um dos seus dados existentes e armazenar os resultados de saudação novamente no armazenamento de Blob.

modelos de toosave ou arquivos no armazenamento de Blob, você precisará tooproperly especificar caminho hello. Contêiner de padrão de saudação de referência anexado cluster do Spark toohello usando um caminho que começa com `wasb:///`. Faça referência a outros locais usando `wasb://`.

Hello exemplo de código a seguir especifica local Olá Olá toobe de dados de entrada de leitura e Olá caminho tooBlob armazenamento de cluster do Spark toohello anexado qual modelo Olá será salvo.

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a>Importar dados, criar um RDD e definir um quadro de dados de acordo com o esquema de toohello
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


**Saída:**

Célula de saudação do tempo toorun: 8 segundos.

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a>Consultar a tabela de saudação e importar resultados de um quadro de dados
Em seguida, a tabela de saudação de consulta de passagens, passageiro e dados de dica; Filtrar dados corrompidos e distantes; e imprima várias linhas.

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

**Saída:**

| fare_amount | passenger_count | tip_amount | tipped |
| --- | --- | --- | --- |
|        13,5 |1.0 |2,9 |1.0 |
|        16,0 |2,0 |3.4 |1.0 |
|        10,5 |2,0 |1.0 |1.0 |

## <a name="data-exploration-and-visualization"></a>Visualização e exploração de dados
Depois de você colocar dados saudação em Spark, Olá próxima etapa no hello processo de ciência de dados é toogain uma compreensão mais profunda dos dados Olá por meio de exploração e visualização. Nesta seção, você pode examinar dados táxi de saudação por meio de consultas do SQL. Em seguida, importar Olá resultados em um tooplot de quadro de dados Olá recursos potenciais para inspeção visual e variáveis de destino usando o recurso de visualização automática de saudação do Jupyter.

### <a name="use-local-and-sql-magic-tooplot-data"></a>Usar o local e dados do SQL tooplot magic
Por padrão, a saída de hello qualquer trecho de código que você executa em um bloco de anotações do Jupyter está disponível no contexto de saudação da sessão de saudação que é mantido em nós de trabalho hello. Se você quiser toosave nós de trabalho de toohello uma viagem para cada cálculo, e se todos os hello dados necessários para a computação está disponível localmente no nó do servidor Olá Jupyter (que é o nó principal Olá), você pode usar o hello `%%local` magic toorun código de saudação trecho de código no servidor do Jupyter hello.

* **Palavra mágica do SQL** (`%%sql`). Olá kernel HDInsight Spark dá suporte a consultas estilo embutido fácil SQLContext. saudação (`-o VARIABLE_NAME`) argumento persiste saída Olá de consulta do SQL hello como um quadro de dados no servidor do Jupyter Olá Pandas. Isso significa que ele estarão disponível no modo local hello.
* `%%local` **palavra mágica**. Olá `%%local` magic executa código Olá localmente no servidor do Jupyter hello, que é o nó principal de saudação do cluster do HDInsight hello. Normalmente, você usa `%%local` magic em conjunto com hello `%%sql` magic com hello `-o` parâmetro. Olá `-o` parâmetro persistir Olá saída de hello SQL consulta localmente e, em seguida, `%%local` magic acionaria o próximo conjunto de saudação do toorun de trecho de código localmente contra a saída da saudação de consultas SQL Olá persistido localmente.

### <a name="query-hello-data-by-using-sql"></a>Consultar dados saudação usando SQL
Essa consulta recupera viagens de táxi Olá pela quantidade de passagens, contagem de passageiro e quantidade de dica.

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

Em Olá código a seguir, Olá `%%local` magic cria um quadro de dados local, sqlResults. Você pode usar sqlResults tooplot usando matplotlib.

> [!TIP]
> A palavra mágica local é usada várias vezes neste artigo. Se seu conjunto de dados for grande, por favor, exemplo toocreate um quadro de dados que pode caber na memória local.
> 
> 

### <a name="plot-hello-data"></a>Plotar dados Olá
Você pode plotar usando código Python após o quadro de dados Olá no contexto local como um quadro de dados Pandas.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 kernel do Spark Olá automaticamente visualiza saída Olá de consultas SQL (HiveQL) depois de executar código hello. Você pode escolher entre vários tipos de visualizações:

* Tabela
* Pizza
* Linha
* Área
* Barra

Aqui está a dados de Olá Olá código tooplot:

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


**Saída:**

![Histograma do valor da gorjeta](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Valor de gorjeta por contagem de passageiros](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Valor de gorjeta por valor de tarifa](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a>Criar recursos, transformar recursos e depois preparar os dados para entrada em funções de modelagem
Para funções de modelagem baseado na árvore do Spark ML e MLlib, você tem destino tooprepare e recursos usando uma variedade de técnicas, como agrupamento, indexação, ativa uma codificação e vetorização. Aqui estão Olá toofollow de procedimentos nesta seção:

1. Criar um novo recurso **reunindo** horários em blocos de tempo de tráfego.
2. Aplicar **hot uma codificação e indexação** toocategorical recursos.
3. **Exemplo e dividir o conjunto de dados de Olá** em frações de treinamento e teste.
4. **Especificar os recursos e a variável de treinamento**e depois criar RDDs (conjuntos de dados distribuídos e resilientes) de ponto de sinalização de entrada para treinamentos de codificação indexada e one-hot, ou quadros de dados.
5. Automaticamente **categorizar e vectorize recursos e destinos** toouse como entradas para modelos de aprendizado de máquina.

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Criar um novo recurso reunindo horários em blocos de tempo de tráfego
Este código mostra como os buckets de toocreate um novo recurso guardando horas em vez de tráfego e como toocache Olá resultante quadro de dados na memória. Onde os quadros de dados e RDDs forem usados repetidamente, cache leva tooimproved tempos de execução. Da mesma forma, você vai cache quadros de dados e RDDs em vários estágios de saudação procedimentos a seguir.

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


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a>Indexação e codificação one-hot de recursos categóricos
Olá modelagem e prever a funções de MLlib exigem recursos com entrada de dados categóricos toobe indexado ou codificado toouse anterior. Esta seção mostra como tooindex ou codificar recursos categóricos para entrada em Olá funções da modelagem.

Você precisa tooindex ou codifica seus modelos de maneiras diferentes, dependendo do modelo de saudação. Por exemplo, modelos de regressão logística e lineares exigem codificação one-hot. Por exemplo, um recurso com três categorias pode ser expandido em três colunas de recurso. Cada coluna contém 0 ou 1, dependendo da categoria de saudação de uma observação. MLlib fornece Olá [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) função hot uma codificação. Este codificador mapeia uma coluna da coluna de tooa de índices de rótulo dos vetores de binários no máximo um único um valor. Com essa codificação, os algoritmos que esperam recursos com valores numéricos, como a regressão logística, podem ser aplicada toocategorical recursos.

Aqui você transformar exemplos de tooshow apenas quatro variáveis, que são cadeias de caracteres. Também é possível indexar outras variáveis, como dia da semana, representadas por valores numéricos, como variáveis categóricas.

Para indexação, use `StringIndexer()` e para codificação one-hot, use as funções `OneHotEncoder()` da MLlib. Aqui está o hello tooindex de código e codificar recursos categóricos:

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


**Saída:**

Célula de saudação do tempo toorun: 4 segundos.

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a>Exemplo e dividir Olá conjunto de dados em frações de treinamento e teste
Esse código cria uma amostragem aleatória de dados de saudação (25%, neste exemplo). Embora a amostragem não é necessária para este exemplo devido tamanho toohello saudação do conjunto de dados, o artigo de saudação mostra como você pode criar amostra para que você saiba como toouse-lo para seus próprios problemas quando necessário. Quando as amostras são grandes, isso pode economizar um tempo significativo durante o treinamento de modelos. Em seguida, dividir o exemplo hello em uma parte de treinamento (75%, neste exemplo) e um teste parte toouse (25%, neste exemplo) de classificação e modelagem de regressão.

Adicione uma linha de tooeach de número aleatório (entre 0 e 1) (em uma coluna de "rand") que pode ser usado tooselect validação cruzada dobras durante o treinamento.

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


**Saída:**

Célula de saudação do tempo toorun: 2 segundos.

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a>Especificar os recursos e a variável de treinamento, bem como criar treinamentos de codificação indexada e one-hot e entrada de testes denominada RDDs pontuais ou quadros de dados
Esta seção contém código que mostra como tooindex categórica e dados de texto como um rótulo do ponto de tipo de dados, codificação-lo, você pode usar outros modelos de classificação e de teste e tootrain MLlib de regressão logística. Objetos de ponto rotulados são RDDs formatados de uma maneira para que sejam exigidos como dados de entrada pela maioria dos algoritmos de aprendizado de máquina na MLlib. Um [ponto rotulado](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) é um vetor local, denso ou esparso, associado a um rótulo/resposta.

Nesse código, você pode especificar variável (dependente) de destino hello e modelos de tootrain Olá recursos toouse. Depois, você cria treinamentos de codificação indexada e one-hot e RDDs de ponto de entrada de teste ou quadros de dados.

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


**Saída:**

Célula de saudação do tempo toorun: 4 segundos.

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a>Categorizar automaticamente e vectorize toouse de recursos e destinos como entradas para modelos de aprendizado de máquina
Use Spark ML toocategorize toouse de destino e os recursos do hello em funções de modelagem baseado na árvore. código de saudação conclui duas tarefas:

* Cria um destino binário para classificação, atribuindo um valor de 0 ou 1 ponto de dados de tooeach entre 0 e 1 usando um valor de limite de 0,5.
* Categoriza automaticamente os recursos. Se o número de saudação de valores numéricos distintos para qualquer recurso for menor que 32, esse recurso é categorizado.

Este é o código de saudação para essas duas tarefas.

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



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a>Modelo de classificação binária: prevê se uma gorjeta será paga ou não
Nesta seção, você deve criar três tipos de toopredict de modelos de classificação binária ou não uma dica deve ser pago:

* Um **modelo de regressão logística** usando Olá Spark ML `LogisticRegression()` função
* Um **modelo de classificação de floresta aleatório** usando Olá Spark ML `RandomForestClassifier()` função
* Um **modelo de classificação de árvore de ampliação gradiente** usando Olá MLlib `GradientBoostedTrees()` função

### <a name="create-a-logistic-regression-model"></a>Criar um modelo de regressão logística
Em seguida, crie um modelo de regressão logística usando Olá Spark ML `LogisticRegression()` função. Criar modelo Olá compilar o código em uma série de etapas:

1. **Treinar modelo de saudação** dados com um conjunto de parâmetros.
2. **Avaliar modelo Olá** em um conjunto de dados de teste com métricas.
3. **Salvar modelo Olá** no armazenamento de Blob para consumo futuro.
4. **Modelo de saudação de pontuação** em relação aos dados de teste.
5. **Plotar resultados Olá** com receptor operacional curvas característica (ROC).

Este é o código de saudação para estes procedimentos:

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

Carregar, pontuação e salvar os resultados de saudação.

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


**Saída:**

ROC nos dados de teste = 0,9827381497557599

Use o Python no local Pandas dados quadros tooplot Olá ROC em curva.

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


**Saída:**

![Curva ROC de gorjeta ou não](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a>Criar um modelo de classificação de floresta aleatória
Em seguida, crie um modelo de classificação aleatória de floresta usando Olá Spark ML `RandomForestClassifier()` de função e, em seguida, avaliar o modelo de saudação nos dados de teste.

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


**Saída:**

ROC nos dados de teste = 0,9847103571552683

### <a name="create-a-gbt-classification-model"></a>Criar um modelo de classificação GBT
Em seguida, crie um modelo de classificação GBT por meio do MLlib `GradientBoostedTrees()` de função e, em seguida, avaliar o modelo de saudação nos dados de teste.

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


**Saída:**

Área sob a curva ROC = 0,9846895479241554

## <a name="regression-model-predict-tip-amount"></a>Modelo de regressão: prever o valor da gorjeta
Nesta seção, você deve criar dois tipos de valor de dica regressão modelos toopredict hello:

* Um **modelo de regressão linear regularizada** usando Olá Spark ML `LinearRegression()` função. Você salvar o modelo de saudação e avaliar modelo Olá em dados de teste.
* Um **Impulsionamento de gradiente modelo de regressão de árvore** usando Olá Spark ML `GBTRegressor()` função.

### <a name="create-a-regularized-linear-regression-model"></a>Criar um modelo de regressão linear regularizada
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


**Saída:**

Célula de saudação do tempo toorun: 13 segundos.

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


**Saída:**

R-sqr nos dados de teste = 0,5960320470835743

Em seguida, consulta Olá resultados de teste como um quadro de dados e usar toovisualize AutoVizWidget e matplotlib-lo.

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

código de saudação cria um quadro de dados local saudação do resultado da consulta e plota dados saudação. Olá `%%local` mágico cria um quadro de dados local, `sqlResults`, que você pode usar tooplot com matplotlib.

> [!NOTE]
> Essa palavra mágica do Spark será usada várias vezes neste artigo. Se a quantidade de saudação de dados for grande, você deve exemplo toocreate um quadro de dados que pode caber na memória local.
> 
> 

Crie plotagens usando matplotlib do Python.

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

**Saída:**

![Valor da gorjeta: real vs. previsto](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a>Criar um modelo de regressão GBT
Criar um modelo de regressão GBT usando Olá Spark ML `GBTRegressor()` de função e, em seguida, avaliar o modelo de saudação nos dados de teste.

[GBTs (árvores com aumento gradiente)](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) são conjuntos de árvores de decisão. Árvores de decisão de treinar GBTs iterativamente toominimize uma função de perda. Você pode usar GBTs para regressão e classificação. Elas podem manipular recursos categóricos, não exigem o dimensionamento de recursos e são capazes de capturar não linearidades e interações de recursos. Use-as também em uma configuração de classificação multiclasse.

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


**Saída:**

R-sqr do teste é: 0,7655383534596654

## <a name="advanced-modeling-utilities-for-optimization"></a>Utilitários de modelagem avançada para otimização
Nesta seção, use utilitários de aprendizado de máquina que os desenvolvedores usam frequentemente para otimização do modelo. Especificamente, você pode otimizar os modelos de AM de três maneiras diferentes usando a limpeza de parâmetro e a validação cruzada:

* Dividir dados saudação em conjuntos de treinamento e validação, otimizar modelo hello usando a limpeza de parâmetro hyper em um conjunto de treinamento e avaliar em um conjunto de validação (regressão linear)
* Otimizar o modelo hello usando a validação cruzada e hyper-varredura de parâmetro por meio CrossValidator função do Spark ML (classificação binária)
* Otimizar modelo hello usando código personalizado de validação cruzada e limpeza de parâmetro toouse qualquer conjunto de função e o parâmetro (regressão linear) de aprendizado de máquina

**Validação cruzada** é uma técnica que avalia como um modelo treinado em um conjunto conhecido de dados será generalizar toopredict Olá recursos de conjuntos de dados no qual ele não foi treinado. Olá geral ideia essa técnica é que um modelo é treinado em um conjunto de dados de dados conhecidos e, em seguida, hello precisão de suas previsões é testado em relação a um conjunto de dados independente. Uma implementação comum é toodivide um conjunto de dados em *k*-dobra e, em seguida, treinar o modelo de saudação de forma round robin em apenas uma das partições de saudação.

**Otimização de Hyper-parâmetro** Olá problema de escolher um conjunto de hyper-parâmetros para um algoritmo de aprendizado, geralmente com a meta de saudação de otimizar uma medida de desempenho do algoritmo Olá em um conjunto de dados independente. Um parâmetro hyper-é um valor que você deve especificar fora Olá procedimento de treinamento de modelo. Suposições sobre valores de parâmetro hyper podem afetar flexibilidade hello e a precisão do modelo de saudação. Árvores de decisão têm hyper-parâmetros, por exemplo, como Olá desejado profundidade e número de folhas na árvore de saudação. Configure de um termo de penalidade de classificação incorreta para uma SVM (máquina de vetor de suporte).

Uma otimização de hyper-parâmetro de tooperform de maneira comum é toouse uma pesquisa de grade, também chamado de um **varredura de parâmetro**. Em uma pesquisa de grade, uma pesquisa detalhada é executada por meio de valores de saudação de um subconjunto especificado de espaço de parâmetro hyper Olá para um algoritmo de aprendizado. Validação cruzada pode fornecer um toosort de métrica de desempenho os resultados ideais de Olá produzido pelo algoritmo de pesquisa de grade hello. Se você usar a limpeza de hyper-parâmetro de validação cruzada, você pode ajudar a problemas de limite como sobreajuste um tootraining de dados de modelo. Dessa forma, o modelo Olá retém Olá capacidade tooapply toohello conjunto geral de dados do qual Olá dados de treinamento foi extraídos.

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a>Otimizar um modelo de regressão linear com a limpeza de hiperparâmetro
Em seguida, dividir os dados em conjuntos de treinamento e validação, use hyper-varredura de parâmetro em um treinamento defina toooptimize Olá modelo e avaliar em um conjunto de validação (regressão linear).

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


**Saída:**

R-sqr do teste é: 0,6226484708501209

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a>Otimizar o modelo de classificação binária hello usando a limpeza de validação cruzada e parâmetro hyper
Esta seção mostra como toooptimize uma classificação binária de modelo usando a validação cruzada e parâmetro hyper limpeza. Isso usa Olá Spark ML `CrossValidator` função.

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


**Saída:**

Célula de saudação do tempo toorun: 33 segundos.

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a>Otimizar o modelo de regressão linear hello usando código personalizado de validação cruzada e limpeza de parâmetro
Em seguida, otimizar modelo hello usando código personalizado e identificar os melhores parâmetros de modelo Olá usando o critério de saudação de precisão mais alta. Em seguida, crie o modelo final hello, avaliar modelo Olá em dados de teste e Salvar modelo Olá no armazenamento de Blob. Por fim, carregar modelo hello, classificar dados de teste e avaliar a precisão.

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


**Saída:**

Célula de saudação do tempo toorun: 61 segundos.

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a>Consumir automaticamente modelos da aprendizado de máquina compilados no Spark com o Scala
Para obter uma visão geral dos tópicos que orientam você pelas tarefas de saudação que compõem o processo de ciência de dados Olá no Azure, consulte [processo de ciência de dados de equipe](http://aka.ms/datascienceprocess).

[Explicações passo a passo do processo de ciência de dados da equipe](data-science-process-walkthroughs.md) descreve outras orientações de ponta a ponta que demonstram etapas Olá Olá processo de ciência de dados de equipe para cenários específicos. Olá explicações passo a passo também ilustra como toocombine de nuvem e ferramentas no local e serviços em um fluxo de trabalho ou pipeline toocreate um aplicativo inteligente.

[Pontuação de modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md) mostra como toouse Scala código tooautomatically carregar e pontuação novos conjuntos de dados com modelos de aprendizado de máquina interna do Spark e salva no armazenamento de BLOBs do Azure. Você pode siga instruções Olá fornecidas e simplesmente substitua Olá código Python Scala código neste artigo para consumo automatizado.

