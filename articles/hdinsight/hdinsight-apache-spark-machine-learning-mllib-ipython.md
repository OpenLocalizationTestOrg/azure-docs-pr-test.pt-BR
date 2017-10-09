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
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>Use o Spark MLlib toobuild uma aplicativo de aprendizado de máquina e analisar um conjunto de dados

Saiba como toouse Spark **MLlib** toocreate um aplicativo toodo simples análise de previsão em um conjunto de dados aberto do aprendizado de máquina. Das bibliotecas aprendizado de máquina internas do Spark, este exemplo usa *classificação* por meio de regressão logística. 

> [!TIP]
> Este exemplo também está disponível como um notebook Jupyter em um cluster do Spark (Linux) que você pode criar no HDInsight. experiência de notebook Olá permite executar trechos de Python de saudação do bloco de anotações de saudação em si. tutorial de saudação do toofollow de dentro de um bloco de anotações, criar um Spark cluster e iniciar um bloco de anotações do Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`). Em seguida, execute o bloco de anotações de saudação **aprendizado de máquina do Spark - análise preditiva em dados de inspeção de alimentos com MLlib.ipynb** em Olá **Python** pasta.
>
>

MLlib é uma biblioteca Spark principal que fornece vários utilitários úteis para tarefas de aprendizado de máquina, incluindo utilitários adequados para:

* classificação
* Regressão
* Clustering
* Modelagem de tópico
* Decomposição de valor singular (SVD) e análise de componente principal (PCA)
* Teste de hipótese e cálculo de estatísticas de exemplo

## <a name="what-are-classification-and-logistic-regression"></a>O que são a classificação e regressão logística?
*Classificação*, uma tarefa de aprendizado de máquina popular é Olá o processo de classificação de dados de entrada em categorias. É Olá trabalho de um toofigure de algoritmo de classificação como tooassign "rótulos" tooinput dados que você fornecer. Por exemplo, você pode pensar em um algoritmo de aprendizado de máquina que aceita informações sobre ações como entrada e divide Olá estoque em duas categorias: ações que você deve vender e ações que você deve manter.

Regressão logística é um algoritmo Olá usado para classificação. A API de regressão logística do Spark é útil para *classificação binária*ou para classificação de dados de entrada em um dos dois grupos. Para obter mais informações sobre a regressão logística, consulte [Wikipédia](https://en.wikipedia.org/wiki/Logistic_regression).

Em resumo, o processo de saudação de regressão logística produz um *função logística* que pode ser usado toopredict Olá probabilidade que um vetor de entrada pertence a um grupo ou outros hello.  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>Exemplo de análise preditiva em dados de inspeção de alimentos
Neste exemplo, você usar a Spark tooperform alguma análise preditiva em dados de inspeção de alimentos (**Food_Inspections1.csv**) que foi adquirido por meio de saudação [portal de dados da cidade de Chicago](https://data.cityofchicago.org/). Este conjunto de dados contém informações sobre inspeções de estabelecimento de alimentos foram realizados em Chicago, incluindo informações sobre cada estabelecimento, violações de saudação encontrados (se houver) e Olá resultados de inspeção de saudação. arquivo de dados CSV Olá já está disponível na conta de armazenamento Olá associada Olá cluster em **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.

Nas etapas de saudação abaixo, desenvolver um modelo toosee que é necessário toopass ou falhar uma inspeção de alimentos.

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>Comece a criar um aplicativo de aprendizado de máquina MMLib do Spark
1. De saudação [portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial). Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.   
1. Na folha de cluster do Spark hello, clique em **painel Cluster**e, em seguida, clique em **Jupyter Notebook**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.

   > [!NOTE]
   > Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. Crie um notebook. Clique em **Novo** e em **PySpark**.

    ![Criar um bloco de anotações do Jupyter](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Criar um novo bloco de anotações do Jupyter")
1. Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb. Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.

    ![Forneça um nome para o bloco de anotações de saudação](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "forneça um nome para o bloco de anotações de saudação")
1. Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente. Olá Spark e Hive contextos são criados automaticamente para você quando você executar a primeira célula de código hello. Você pode começar a criar seu aplicativo de aprendizado importando tipos de saudação necessários para este cenário de máquina. toodo, portanto, coloque o cursor de saudação na célula hello e pressione **SHIFT + ENTER**.

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>Construir um dataframe de entrada
Podemos usar `sqlContext` tooperform transformações em dados estruturados. Olá primeira tarefa é dados de exemplo hello tooload ((**Food_Inspections1.csv**)) em um Spark SQL *dataframe*.

1. Como dados brutos hello estão em um formato CSV, é preciso toouse Olá Spark contexto toopull cada linha do arquivo de saudação na memória como texto não estruturado; em seguida, você use tooparse de biblioteca CSV do Python cada linha individualmente.

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. Agora temos arquivo CSV de saudação como um RDD.  esquema de Olá toounderstand de dados hello, recuperamos uma linha de saudação RDD.

        inspections.take(1)

    Você verá uma saída semelhante Olá seguinte:

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
1. Olá saída anterior nos dá uma ideia do esquema de saudação do arquivo de entrada hello. Ele inclui o nome de saudação do cada estabelecimento, o tipo de saudação do estabelecimento, endereço hello, dados de saudação do inspeções hello e localização Olá, entre outras coisas. Vamos selecionar algumas colunas que são úteis para nosso análise de previsão e agrupar resultados de saudação como um dataframe, quais nós e usam toocreate uma tabela temporária.

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. Agora temos um *dataframe*, `df` no qual podemos executar nossa análise. Também temos uma chamada de tabela temporária **CountResults**. Há quatro colunas de interesse em Olá dataframe: **id**, **nome**, **resultados**, e **violações**.

    Vamos uma pequena amostra dos dados hello:

        df.show(5)

    Você verá uma saída semelhante Olá seguinte:

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

## <a name="understand-hello-data"></a>Compreender os dados de saudação
1. Vamos começar tooget uma ideia do que contém o nosso conjunto de dados. Por exemplo, quais são os diferentes valores Olá Olá **resultados** coluna?

        df.select('results').distinct().show()

    Você verá uma saída semelhante Olá seguinte:

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
1. Uma visualização rápida pode nos ajudar a raciocinar sobre a distribuição de saudação desses resultados. Já temos dados saudação em uma tabela temporária **CountResults**. Você pode executar Olá Olá tabela tooget consulta SQL a seguir uma melhor compreensão de como os resultados de saudação são distribuídos.

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    Olá `%%sql` mágico seguido `-o countResultsdf` garante que saída Olá de consulta de saudação é persistentes localmente no servidor de Jupyter de saudação (normalmente Olá nó principal do cluster Olá). saída de Hello é mantida como um [Pandas](http://pandas.pydata.org/) dataframe com hello especificado nome **countResultsdf**.

    Você verá uma saída semelhante Olá seguinte:

    ![Saída da consulta SQL](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "Saída da consulta SQL")

    Para obter mais informações sobre Olá `%%sql` mágico e outros magics disponíveis com o kernel do PySpark hello, consulte [Kernels disponíveis em blocos de anotações do Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
1. Você também pode usar Matplotlib, uma biblioteca usada tooconstruct visualização de dados, toocreate um gráfico. Porque plotagem Olá deve ser criada de saudação localmente persistente **countResultsdf** dataframe, o trecho de código Olá deve começar com hello `%%local` mágica. Isso garante que o código de Olá é executado localmente no servidor do Jupyter hello.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Você verá uma saída semelhante Olá seguinte:

    ![Saída do aplicativo de aprendizado de máquina do Spark – gráfico de pizza com cinco conjuntos de resultados de inspeção distintos](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Saída do resultado de aprendizado de máquina de Spark")
1. Você pode ver que uma inspeção pode ter cinco resultados distintos:

   * Negócios não localizados
   * Reprovado
   * Aprovado
   * Aprovar c/ condições
   * Fora de negócio

     Vamos desenvolva um modelo que pode adivinhar o resultado de saudação de uma inspeção de alimentos, violações de saudação determinado. Como a regressão logística é um método de classificação binária, faz sentido toogroup nossos dados em duas categorias: **falha** e **passar**. Um "passar com condições de" ainda é uma passagem, portanto quando treinamos modelo hello, consideramos Olá dois resultados equivalente. Dados com hello outros resultados ("Business não localizada" ou "de negócios") não são úteis para removemos do nosso conjunto de treinamento. Isso deve ser okey porque essas duas categorias compõem uma porcentagem muito pequena de resultados Olá mesmo assim.
1. Vamos prosseguir e converter nosso dataframe existente (`df`) em um novo dataframe em que cada inspeção é representada como um par de violações de rótulo. No nosso caso, um rótulo de `0.0` representa uma falha, um rótulo de `1.0` representa um sucesso e um rótulo de `-1.0` representa alguns resultados diferentes desses dois. Vamos filtrar esses outros resultados ao calcular o novo quadro de dados hello.

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    toosee quais Olá rotulada dados parece, vamos recuperar uma linha.

        labeledData.take(1)

    Você verá uma saída semelhante Olá seguinte:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>Criar um modelo de regressão logística de dataframe de entrada hello
Nossa tarefa final é tooconvert Olá rotulada dados em um formato que pode ser analisado por regressão logística. algoritmo de regressão logística Olá tooa entrada deve ser um conjunto de *pares de vetor de recurso de rótulo*, onde hello "vetor de recurso" é um vetor de números que representam o ponto de entrada hello. Portanto, é preciso tooconvert a coluna de violações"hello", o que é semi-estruturados e contém muitos comentários na matriz de tooan texto livre de números reais que uma máquina facilmente compreensível.

Uma abordagem de aprendizado de máquina padrão para o idioma natural de processamento é tooassign cada palavra distinct "index" e, em seguida, passar uma algoritmo de aprendizagem, de modo que o valor de cada índice contém frequência relativa de saudação da palavra em texto de saudação de máquina do vetor toohello cadeia de caracteres.

MLlib fornece uma maneira fácil tooperform esta operação. Primeiro, "transformar" cada violações cadeia de caracteres tooget Olá palavras individuais em cada cadeia de caracteres. Em seguida, use um `HashingTF` tooconvert cada conjunto de tokens em um vetor de recurso que pode ser passado toohello tooconstruct de algoritmo de regressão logística de um modelo. Realizamos todas essas etapas em sequência, usando um "pipeline".

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>Avaliar modelo Olá em um conjunto de dados de teste separada
Podemos usar o modelo de saudação que criamos anteriormente muito*prever* quais Olá resultados da nova inspeções serão, com base em violações de saudação que foram observadas. Esse modelo no conjunto de dados de saudação é treinado **Food_Inspections1.csv**. Vamos usar um segundo conjunto de dados, **Food_Inspections2.csv**, muito*avaliar* Olá intensidade desse modelo em dados novos. Esse segundo conjunto de dados (**Food_Inspections2.csv**) já deve estar no contêiner de armazenamento padrão de Olá associada Olá cluster.

1. Olá, trecho a seguir cria um novo dataframe, **predictionsDf** que contém a previsão Olá gerado pelo modelo de saudação. trecho de saudação também cria uma tabela temporária chamada **previsões** com base em dataframe de saudação.

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    Você verá uma saída semelhante Olá seguinte:

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
1. Examinar uma das previsões de saudação. Execute este trecho de código:

        predictionsDf.take(1)

   Há uma previsão para a primeira entrada hello no conjunto de dados de teste de saudação.
1. Olá `model.transform()` método se aplica a saudação mesmo transformação tooany novos dados com hello mesmo esquema e chegar a uma previsão de como tooclassify Olá dados. Podemos fazer algumas estatísticas simples tooget uma noção da nossas previsões como precisas foram:

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    saída de Hello semelhante ao seguinte hello:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    Usando Regressão logística com Spark fornece um modelo preciso da relação de saudação entre descrições de violações em inglês e se um negócio deve passar ou falhar uma inspeção de alimentos.

## <a name="create-a-visual-representation-of-hello-prediction"></a>Criar uma representação visual de previsão Olá
Agora podemos construir um toohelp final visualização que nos argumentar sobre resultados de saudação desse teste.

1. Vamos começar por meio da extração previsões diferentes hello e resultados de Olá **previsões** tabela temporária criada anteriormente. consultas a seguir Hello separam saída hello como *true_positive*, *false_positive*, *true_negative*, e *false_negative*. Em consultas de saudação abaixo, podemos desativar visualização usando `-q` e também salvar a saída de hello (usando `-o`) como quadros de dados que podem ser usados com hello `%%local` mágica.

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. Por fim, use Olá seguindo o trecho de código toogenerate Olá plotagem usando **Matplotlib**.

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    Você deve ver Olá saída a seguir:

    ![Saída do aplicativo de aprendizado de máquina do Spark – percentuais de gráfico de pizza de inspeções em alimentos com falha.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Saída do resultado de aprendizado de máquina do Spark")

    Neste gráfico, um resultado "positivo" refere-se inspeção de alimentos toohello falhado, enquanto um resultado negativo refere-se tooa passado inspeção.

## <a name="shut-down-hello-notebook"></a>Fechar o bloco de anotações de saudação
Depois de terminar de executar o aplicativo hello, você deve desligar recursos de Olá Olá notebook toorelease. toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**. Isso é desligado e fecha Olá notebook.

## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* 
            [Spark com Machine Learning: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Streaming Spark: use o Spark no HDInsight para a criação de aplicativos streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)
