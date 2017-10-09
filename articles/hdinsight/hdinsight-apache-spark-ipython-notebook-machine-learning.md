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
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>Criar aplicativos de aprendizado de máquina do Apache Spark no Azure HDInsight

Saiba como toobuild um aplicativo de aprendizado de máquina do Apache Spark usando um Spark cluster HDInsight. Este artigo mostra como toouse Olá anotações do Jupyter com hello cluster toobuild e testar esse aplicativo. aplicativo Hello usa dados de HVAC.csv do exemplo hello estão disponíveis em todos os clusters por padrão.

**Pré-requisitos:**

Você deve ter o seguinte hello:

* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="data"></a>Entender o conjunto de dados Olá
Antes de começar criando um aplicativo hello, vamos entenda a estrutura de saudação de dados Olá para que criamos aplicativo hello e tipo de saudação de análise que faremos nos dados de saudação. 

Neste artigo, podemos usar o exemplo hello **HVAC.csv** arquivo de dados que está disponível no hello conta de armazenamento do Azure que você associou com cluster do HDInsight hello. Na conta de armazenamento hello, arquivo hello está no **\HdiSamples\HdiSamples\SensorSampleData\hvac**. Baixe e abra Olá CSV arquivo tooget um instantâneo dos dados de saudação.  

![Exemplo de instantâneo dos dados usados para aprendizado de máquina do Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Exemplo de instantâneo dos dados usados para aprendizado de máquina do Spark")

dados saudação mostram a temperatura do destino hello e temperatura real de saudação do prédio com sistemas de ar Condicionado instalados. Vamos supor que Olá **sistema** coluna representa a ID de sistema hello e hello **SystemAge** coluna representa o número de saudação de sistema HVAC Olá foi em vigor na construção de saudação de anos.

Usamos este toopredict de dados se um edifício serão mais quentes ou colder com base em temperatura de destino hello, recebe uma ID de sistema e a idade do sistema.

## <a name="app"></a>Escrever um aplicativo de aprendizado de máquina do Spark usando o MLlib Spark
Neste aplicativo, usamos um pipeline de Spark ML tooperform uma classificação de documento. No pipeline de saudação é dividir o documento de saudação em palavras, converter palavras Olá em um vetor de recurso numérico e, por fim, criar um modelo de previsão usando rótulos e vetores de recursos de saudação. Execute Olá aplicativo de hello toocreate as etapas a seguir.

1. De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial). Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.   
2. Na folha de cluster do Spark hello, clique em **painel Cluster**e, em seguida, clique em **Jupyter Notebook**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.
   
   > [!NOTE]
   > Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. Crie um novo bloco de anotações. Clique em **Novo** e em **PySpark**.
   
    ![Criar um exemplo de bloco de anotações do Jupyter para aprendizado de máquina do Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Criar um exemplo de bloco de anotações do Jupyter para aprendizado de máquina Spark")
4. Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb. Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.
   
    ![Fornecer um exemplo de nome de bloco de anotações do Jupyter para aprendizado de máquina Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Fornecer um exemplo de nome de bloco de anotações do Jupyter para aprendizado de máquina Spark")
5. Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente. contextos de Spark e Hive Olá serão automaticamente criados para você quando você executar a primeira célula de código hello. Você pode começar importando tipos Olá que são necessários para este cenário. Cole Olá seguindo o trecho de código em uma célula vazia e, em seguida, pressione **SHIFT + ENTER**. 
   
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
6. Você agora deve carregar dados de saudação (hvac.csv), analisá-lo e usá-lo tootrain modelo de saudação. Para isso, você define uma função que verifica se a temperatura real Olá da criação de saudação do é maior do que a temperatura do destino de saudação. Se a temperatura real Olá for maior, a construção de saudação é ativa, indicado pelo valor Olá **1.0**. Se a temperatura real Olá é menor, construção Olá fria, é indicado pelo valor de saudação **0,0**. 
   
    Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.

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


1. Configurar o pipeline de aprendizado de máquina do Spark Olá que consiste em três estágios: lr, hashingTF e tokenizer. Para obter mais informações sobre o que é um pipeline e como ele funciona, confira <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Pipeline de aprendizado de máquina Spark</a>.
   
    Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. Ajustar o documento de treinamento de toohello Olá pipeline. Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.
   
        model = pipeline.fit(training)
3. Verifique se Olá treinamento documento toocheckpoint seu progresso com o aplicativo hello. Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.
   
        training.show()
   
    Isso deve dar a seguir Olá saída semelhante toohello:
   
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

    Voltar e verifique se a saída de hello no arquivo CSV bruto de saudação. Por exemplo, arquivo CSV para Olá primeira linha hello tem esses dados:

    ![Exemplo de instantâneo dos dados de saída para aprendizado de máquina do Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Exemplo de instantâneo dos dados de saída para aprendizado de máquina do Spark")

    Observe como a temperatura real Olá é menor do que a temperatura do destino Olá sugerindo construção hello está frio. Portanto, na saída de treinamento hello, Olá valor para **rótulo** Olá primeira linha é **0,0**, que significa construção Olá não está ativa.

1. Prepare um conjunto de dados toorun Olá treinado em. toodo assim, passar em uma ID de sistema e a idade do sistema (denotado como **SystemInfo** na saída de treinamento Olá), e Olá modelo seria prever se Olá compilando com idade de ID e do sistema que sistema poderiam ser mais quentes (indicado por 1.0) ou mais ( indicado pela 0.0).
   
   Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. Por fim, fazer previsões sobre os dados de teste de saudação. Saudação de colar o trecho de código em uma célula vazia e pressione a seguir **SHIFT + ENTER**.
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. Você verá uma saída semelhante toohello a seguir:
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   A primeira linha na previsão Olá Olá, você pode ver que para um sistema HVAC com ID 20 e o sistema de 25 anos, construção hello serão mais acessada (**previsão = 1.0**). primeiro valor Olá para DenseVector (0.49999) corresponde toohello previsão 0,0 e valor de segundo hello (0.5001) corresponde a previsão toohello 1.0. Na saída de hello, embora Olá segundo valor só é ligeiramente maior, Olá modelo mostra **previsão = 1.0**.
4. Depois de terminar de executar o aplicativo hello, você deverá recursos de saudação do desligamento Olá notebook toorelease. toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**. Esta desligará e notebook Olá fechar.

## <a name="anaconda"></a>Use a biblioteca Anaconda scikit-learn para aprendizado de máquina do Spark
Os clusters Apache Spark no HDInsight incluem bibliotecas Anaconda. Isso também inclui Olá **scikit-Saiba** biblioteca para o aprendizado de máquina. biblioteca de saudação também inclui vários conjuntos de dados que você pode usar os aplicativos de exemplo toobuild diretamente de um bloco de anotações do Jupyter. Para exemplos sobre como usar o hello scikit-Saiba biblioteca, consulte [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).

## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar maiores Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
