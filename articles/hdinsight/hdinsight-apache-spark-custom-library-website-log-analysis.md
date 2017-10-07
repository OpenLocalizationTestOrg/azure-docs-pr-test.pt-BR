---
title: logs de site aaaAnalyze com bibliotecas de Python no Spark - Azure | Microsoft Docs
description: "Este bloco de anotações demonstra como tooanalyze dados de log usando uma biblioteca personalizada com Spark no HDInsight do Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a>Analisar logs do site usando uma biblioteca personalizada do Python com cluster Spark no HDInsight

Este bloco de anotações demonstra como tooanalyze dados de log usando uma biblioteca personalizada com Spark no HDInsight. podemos usar a biblioteca personalizada de saudação é uma biblioteca de Python chamada **iislogparser.py**.

> [!TIP]
> Este tutorial também está disponível como um notebook Jupyter em um cluster do Spark (Linux) que você pode criar no HDInsight. experiência de notebook Olá permite executar trechos de Python de saudação do bloco de anotações de saudação em si. tutorial de saudação tooperform de dentro de um bloco de anotações, criar um cluster Spark, inicie um bloco de anotações do Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), e, em seguida, execute notebook Olá **analisar logs com Spark usando um library.ipynb personalizado** em Olá  **PySpark** pasta.
>
>

**Pré-requisitos:**

Você deve ter o seguinte hello:

* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="save-raw-data-as-an-rdd"></a>Salvar dados brutos como RDD
Nesta seção, usamos Olá [Jupyter](https://jupyter.org) notebook associado a um cluster do Apache Spark no HDInsight toorun trabalhos que processam os dados brutos de exemplo e salvá-lo como uma tabela de Hive. dados de exemplo Hello são um arquivo. csv (hvac.csv) disponível em todos os clusters por padrão.

Depois que seus dados é salvo como uma tabela Hive, nós conectará toohello tabela de Hive usando ferramentas de BI como Power BI e Tableau na próxima seção, Olá.

1. De saudação [portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial). Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.   
2. Na folha de cluster do Spark hello, clique em **painel Cluster**e, em seguida, clique em **Jupyter Notebook**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.

   > [!NOTE]
   > Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Crie um novo bloco de anotações. Clique em **Novo** e em **PySpark**.

    ![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Criar um novo bloco de anotações do Jupyter")
4. Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb. Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.

    ![Forneça um nome para o bloco de anotações de saudação](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "forneça um nome para o bloco de anotações de saudação")
5. Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente. contextos de Spark e Hive Olá serão automaticamente criados para você quando você executar a primeira célula de código hello. Você pode começar importando tipos Olá que são necessários para este cenário. Cole Olá seguindo o trecho de código em uma célula vazia e, em seguida, pressione **SHIFT + ENTER**.

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. Crie um RDD usando dados de log de exemplo hello já disponíveis no cluster de saudação. Você pode acessar dados Olá na conta de armazenamento padrão de saudação associada Olá cluster em **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. Recupere um tooverify de conjunto de log de exemplo que Olá a etapa anterior foi concluída com êxito.

        logs.take(5)

    Você verá uma saída semelhante toohello a seguir:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a>Analise os dados de log usando uma biblioteca Python personalizada
1. Na saída de hello acima, primeiras linhas de alguns Olá incluem informações de cabeçalho hello e corresponde a cada linha restante esquema Olá descrita nesse cabeçalho. Analisar esses logs pode ser complicado. Então, usamos uma biblioteca personalizada do Python (**iislogparser.py**) que torna a análise desses logs muito mais fácil. Por padrão, essa biblioteca é incluída com o cluster do Spark no HDInsight em **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.

    No entanto, essa biblioteca não fica Olá `PYTHONPATH` para nós não pode usá-lo usando uma instrução de importação como `import iislogparser`. toouse nessa biblioteca, é necessário distribuir nós de trabalho tooall hello. Execute Olá trecho de código a seguir.

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. `iislogparser`Fornece uma função `parse_log_line` que retorna `None` se uma linha de log é uma linha de cabeçalho e retorna uma instância da saudação `LogLine` classe se ele encontrar uma linha de log. Olá Use `LogLine` classe tooextract Olá apenas linhas de log de saudação RDD:

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. Recupere algumas linhas de log extraídos tooverify que Olá etapa foi concluída com êxito.

       logLines.take(2)

   saída de Hello deve ser a seguir toohello semelhante:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. Olá `LogLine` classe, por sua vez, tem alguns métodos úteis, como `is_error()`, que retorna se uma entrada de log tem um código de erro. Use esse número de saudação de toocompute de erros nas linhas de log Olá extraído, em seguida, arquivo de log e todos os Olá erros tooa diferentes.

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   Você verá uma saída semelhante Olá seguinte:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. Você também pode usar **Matplotlib** tooconstruct uma visualização de dados de saudação. Por exemplo, se você quiser tooisolate causa de saudação de solicitações que são executados por um longo tempo, convém arquivos Olá toofind levar hello mais tooserve de tempo em média.
   trecho de saudação abaixo recupera Olá superior 25 recursos que levou a maioria dos tooserve de tempo uma solicitação.

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   Você verá uma saída semelhante Olá seguinte:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. Você também pode apresentar essas informações no formulário de saudação de plotagem. Como uma primeira toocreate etapa um gráfico, vamos primeiro criar uma tabela temporária **AverageTime**. saudação de grupos de tabela Olá registra por toosee tempo se houver qualquer picos de latência incomum em um determinado momento.

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. Você pode executar Olá tooget de consulta SQL a seguir todos os registros de saudação em Olá **AverageTime** tabela.

       %%sql -o averagetime
       SELECT * FROM AverageTime

   Olá `%%sql` mágico seguido `-o averagetime` garante que saída Olá de consulta de saudação é persistentes localmente no servidor de Jupyter de saudação (normalmente Olá nó principal do cluster Olá). saída de Hello é mantida como um [Pandas](http://pandas.pydata.org/) dataframe com hello especificado nome **averagetime**.

   Você verá uma saída semelhante Olá seguinte:

   ![Saída da consulta SQL](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Saída da consulta SQL")

   Para obter mais informações sobre Olá `%%sql` magic, consulte [suporte para parâmetros com Olá % % sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
7. Agora você pode usar Matplotlib, uma biblioteca usada tooconstruct visualização de dados, toocreate um gráfico. Porque plotagem Olá deve ser criada de saudação localmente persistente **averagetime** dataframe, o trecho de código Olá deve começar com hello `%%local` mágica. Isso garante que o código de Olá é executado localmente no servidor do Jupyter hello.

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   Você verá uma saída semelhante Olá seguinte:

   ![Saída de Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Saída de Matplotlib")
8. Depois de terminar de executar o aplicativo hello, você deverá recursos de saudação do desligamento Olá notebook toorelease. toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**. Esta desligará e notebook Olá fechar.

## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)

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
