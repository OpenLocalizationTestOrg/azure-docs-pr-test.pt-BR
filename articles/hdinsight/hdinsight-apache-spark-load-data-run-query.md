---
title: aaaRun a consultas interativas em um cluster Spark no HDInsight | Microsoft Docs
description: "Início rápido do HDInsight Spark no como cluster de toocreate um Apache Spark no HDInsight."
keywords: "início rápido do spark,spark interativo,consulta interativa,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>Executar consultas interativas em um cluster HDInsight Spark

Neste artigo, você deve usar um Jupyter notebook toorun interativo Spark consultas SQL em relação a um cluster Spark. Anotações do Jupyter é um aplicativo baseado em navegador que estende Olá baseado em console interativo experiência toohello da Web. Para obter mais informações, consulte [de anotações do Jupyter Olá](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

Para este tutorial, você usar Olá **PySpark** kernel no toorun de notebook Jupyter de saudação uma consulta SQL Spark interativa. Blocos de anotações do Jupyter em de clusters HDInsight também dão suporte a dois outros kernels – **PySpark3** e **Spark**. Para obter mais informações sobre kernels hello e benefícios de saudação do uso de **PySpark**, consulte [clusters kernels de notebook Jupyter de uso com o Apache Spark no HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Pré-requisitos

* **Um cluster HDInsight Spark do Azure**. Para obter instruções, consulte [Criar um cluster do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>Criar um bloco de anotações do Jupyter consultas interativas toorun

consultas de toorun, usamos os dados de exemplo que está disponível no armazenamento de saudação associado cluster Olá por padrão. No entanto, você deve primeiro carregar esses dados no Spark como um dataframe. Uma vez que o dataframe hello, você pode executar consultas nele usando anotações do Jupyter hello. Nesta seção, você vê como:

* Registrar um conjunto de dados de exemplo como um dataframe do Spark.
* Execute consultas no dataframe de saudação.

1. Olá abrir [portal do Azure](https://portal.azure.com/). Se você optou por painel de toohello toopin Olá cluster, clique em Olá cluster lado a lado na folha de cluster Olá painel toolaunch hello.

    Se você não fixar Olá cluster toohello painel de controle, no painel esquerdo do hello, clique em **clusters HDInsight**e, em seguida, clique em cluster Olá que você criou.

3. Em **Links rápidos**, clique em **Painéis de cluster**e, em seguida, clique em **Anotações do Jupyter**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.

   ![Abra Jupyter notebook toorun Spark SQL consulta interativo](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "consulta toorun Spark SQL interativo notebook Jupyter aberto")

   > [!NOTE]
   > Você também pode acessar as anotações do Jupyter Olá para o cluster por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Crie um notebook. Clique em **Novo** e em **PySpark**.

   ![Criar uma consulta SQL Spark interativa Jupyter notebook toorun](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "criar uma consulta Jupyter notebook toorun interativa Spark SQL")

   Um novo bloco de anotações é criado e aberto com o nome hello Untitled(Untitled.pynb).

4. Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável, se desejar.

    ![Forneça um nome para Olá Jupter notebook toorun Spark consulta interativo de](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "forneça um nome para Olá Jupter notebook toorun Spark consulta interativa do")

5. Colar Olá seguinte código em uma célula vazia e, em seguida, pressione **SHIFT + ENTER** toorun código de saudação. código de saudação importa tipos de saudação requeridos para este cenário:

        from pyspark.sql.types import *

    Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente. Olá Spark e Hive contextos são criados automaticamente para você quando você executar a primeira célula de código hello.

    ![Status de consulta interativa SQL Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status de consulta interativa SQL Spark")

    Sempre que você executa uma consulta interativa em Jupyter, o título da janela navegador web mostra um **(ocupada)** status junto com o título do bloco de anotações de saudação. Você também verá um toohello próximo do círculo sólido **PySpark** texto no canto superior direito de saudação. Após o trabalho hello, ele altera o círculo vazio tooa.

6. Antes de carregar dados saudação em um cluster Spark, vamos examinar um instantâneo dele. Olá dados de exemplo usados neste tutorial estão disponíveis como um arquivo CSV em todos os clusters de HDInsight Spark no **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**. dados de saudação captura variações de temperatura de saudação do prédio. Aqui está Olá primeiras linhas de dados de saudação.

    ![Instantâneo de dados para consulta SQL interativa do Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "Instantâneo de dados para consulta SQL interativa do Spark")

6. Criar um dataframe e uma tabela temporária (**hvac**) executando Olá código a seguir. Para este tutorial, não criamos todas as colunas de saudação na tabela temporária hello como colunas de toohello comparados em dados brutos de CSV hello. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Depois de criar tabela hello, executar consulta interativa nos dados hello, use Olá código a seguir.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   Como você está usando um kernel PySpark, agora você pode diretamente executar uma consulta SQL interativa na tabela temporária Olá **hvac** que você criou usando Olá `%%sql` mágica. Para obter mais informações sobre Olá `%%sql` mágico e outros magics disponíveis com o kernel do PySpark hello, consulte [Kernels disponíveis em blocos de anotações do Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   Olá após a saída tabular é exibido por padrão.

     ![Tabela de saída do resultado da consulta interativa Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Tabela de saída do resultado da consulta interativa Spark")

    Você também pode ver os resultados de saudação em outras visualizações também. Por exemplo, um gráfico de área para Olá a mesma saída seria semelhante a seguinte hello.

    ![Gráfico de área de resultado de consulta interativa do Spark](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Gráfico de área de resultado de consulta interativa do Spark")

9. Desliga os recursos de cluster de saudação do hello notebook toorelease depois de terminar de executar o aplicativo hello. toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**.

## <a name="next-step"></a>Próxima etapa

Neste artigo, você aprendeu como toorun a consultas interativas no Spark usando anotações do Jupyter. Avançar toohello próximo artigo toosee como dados de saudação registrado no Spark podem ser removidos em uma ferramenta de análise de BI, como o Power BI e Tableau. 

> [!div class="nextstepaction"]
>[Spark BI usando ferramentas de visualização de dados com o Azure HDInsight](hdinsight-apache-spark-use-bi-tools.md)




