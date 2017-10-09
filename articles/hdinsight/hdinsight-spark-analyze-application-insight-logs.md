---
title: aaaAnalyze Application Insight registra em log com Spark - HDInsight do Azure | Microsoft Docs
description: "Saiba como tooexport Application Insight registra tooblob armazenamento e, em seguida, analise os logs de saudação com Spark no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>Analisar logs de telemetria do Application Insights com Spark no HDInsight

Saiba como toouse despertar em HDInsight tooanalyze dados de telemetria do Application Insight.

[Visual Studio Application Insights](../application-insights/app-insights-overview.md) é um serviço de análise que monitora seus aplicativos Web. Dados de telemetria gerados pelo Application Insights podem ser exportado tooAzure armazenamento. Quando dados saudação estiverem no armazenamento do Azure, HDInsight pode ser usado tooanalyze-lo.

## <a name="prerequisites"></a>Pré-requisitos

* Um aplicativo que é configurado toouse Application Insights.

* Familiaridade com a criação de um cluster HDInsight baseado em Linux. Para saber mais, veja [Criar o Spark no HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

  > [!IMPORTANT]
  > etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Um navegador da Web.

Olá recursos a seguir foram usados no desenvolvimento e teste neste documento:

* Dados de telemetria do Application Insights foi gerados usando um [aplicativo web Node.js configurado toouse Application Insights](../application-insights/app-insights-nodejs.md).

* Um Spark baseados em Linux em versão 3.5 do cluster HDInsight foi usado tooanalyze Olá dados.

## <a name="architecture-and-planning"></a>Arquitetura e planejamento

Olá diagrama a seguir ilustra a arquitetura de serviço Olá deste exemplo:

![Diagrama mostrando dados que fluem do armazenamento de tooblob Application Insights, em seguida, sendo processadas pelo Spark no HDInsight](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Armazenamento do Azure

Application Insights pode ser configurado toocontinuously exportar telemetria informações tooblobs. HDInsight, em seguida, pode ler os dados armazenados em blobs de saudação. No entanto, há alguns requisitos que devem ser seguidos:

* **Local**: se hello conta de armazenamento e HDInsight estão em locais diferentes, isso pode aumentar a latência. Ele também aumenta o custo, como encargos de saída são aplicada toodata movendo entre regiões.

    > [!WARNING]
    > Não há suporte para o uso de uma Conta de armazenamento em um local diferente do HDInsight.

* **Tipo de Blob**: o HDInsight dá suporte apenas aos blobs de bloco. Application Insights padrões toousing blobs de bloco, portanto deve funcionar por padrão com o HDInsight.

Para obter informações sobre como adicionar armazenamento adicional tooan existente cluster HDInsight, consulte Olá [adicionar mais contas de armazenamento](hdinsight-hadoop-add-storage.md) documento.

### <a name="data-schema"></a>Esquema de dados

Application Insights fornece [exportar modelo de dados](../application-insights/app-insights-export-data-model.md) informações de formato de dados de telemetria hello exportada tooblobs. Olá etapas neste documento usam Spark SQL toowork com dados de saudação. Spark SQL pode gerar automaticamente um esquema para a estrutura JSON de saudação registrado pelo Application Insights.

## <a name="export-telemetry-data"></a>Exportar dados de telemetria

Siga as etapas de saudação em [configurar a exportação contínua](../application-insights/app-insights-export-telemetry.md) tooconfigure sua tooan de informações de telemetria do Application Insights tooexport armazenamento do Azure blob.

## <a name="configure-hdinsight-tooaccess-hello-data"></a>Configurar dados de saudação do HDInsight tooaccess

Se você estiver criando um cluster HDInsight, adicione a conta de armazenamento de Olá durante a criação do cluster.

Olá tooadd cluster existente do tooan da conta de armazenamento do Azure, use as informações de Olá Olá [adicionar outras contas de armazenamento](hdinsight-hadoop-add-storage.md) documento.

## <a name="analyze-hello-data-pyspark"></a>Analisar dados saudação: PySpark

1. De saudação [portal do Azure](https://portal.azure.com), selecione o Spark no cluster HDInsight. De saudação **Links rápidos** seção, selecione **painéis do Cluster**e, em seguida, selecione **Jupyter Notebook** da folha de Cluster Dashboard__ hello.

    ![painéis do cluster Olá](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. No hello canto superior direito da página de Jupyter hello, selecione **novo**e, em seguida, **PySpark**. Uma nova guia do navegador que contém um Bloco de Notas Jupyter com base em Python é aberta.

3. No primeiro campo de saudação (chamado um **célula**) na página de hello, digite Olá texto a seguir:

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    Esse código define a estrutura de diretórios de saudação do Spark toorecursively acesso para dados de entrada hello. Telemetria do Application Insights está conectado tooa directory estrutura semelhante toohello `/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Use **SHIFT + ENTER** toorun código de saudação. Em Olá lado esquerdo da célula hello, um '\*' aparece entre Olá colchetes tooindicate que código Olá nesta célula está sendo executado. Depois que ele for concluído, hello '\*' altera tooa número e a saída semelhante toohello texto a seguir é exibida abaixo de célula hello:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. É criada uma nova célula abaixo Olá um primeiro. Digite hello depois do texto na célula de novo hello. Substituir `CONTAINER` e `STORAGEACCOUNT` com o nome de conta de armazenamento do Azure hello e o nome do contêiner de blob que contém dados do Application Insights.

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Use **SHIFT + ENTER** tooexecute esta célula. Você verá um toohello semelhante resultado texto a seguir:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    caminho de wasb Olá retornado é o local de saudação do hello dados de telemetria do Application Insights. Saudação de alteração `hdfs dfs -ls` Olá célula toouse Olá wasb caminho retornado de linha e, em seguida, usar **SHIFT + ENTER** toorun célula de saudação novamente. Neste momento, os resultados de saudação devem exibir diretórios Olá que contêm dados de telemetria.

   > [!NOTE]
   > Olá para restante Olá Olá as etapas nesta seção, `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` diretório foi usado. A estrutura de diretório pode ser diferente.

6. Na célula de Avançar hello, insira Olá código a seguir: substituir `WASB_PATH` com caminho de saudação da etapa anterior hello.

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    Esse código cria um dataframe de arquivos JSON hello exportados pelo processo de exportação contínua hello. Use **SHIFT + ENTER** toorun esta célula.
7. Na próxima célula de Olá, digite e execute Olá esquema Olá tooview Spark criado para os arquivos JSON Olá a seguir:

   ```python
   jsonData.printSchema()
   ```

    saudação de esquema para cada tipo de telemetria é diferente. Olá, exemplo a seguir é esquema Olá que é gerada para solicitações da web (dados armazenados em Olá `Requests` subdiretório):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. Use Olá após tooregister Olá dataframe como uma tabela temporária e executar uma consulta em relação aos dados hello:

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    Essa consulta retorna informações de cidade Olá para registros de 20 principais Olá onde context.location.city não é nulo.

   > [!NOTE]
   > estrutura de contexto Hello está presente em toda a telemetria registrada pelo Application Insights. elemento de cidade Olá não pode ser preenchido em seus logs. Use Olá esquema tooidentify outros elementos que você pode consultar que podem conter dados para seus logs.

    Esta consulta retorna informações toohello semelhante texto a seguir:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>Analisar dados saudação: Scala

1. De saudação [portal do Azure](https://portal.azure.com), selecione o Spark no cluster HDInsight. De saudação **Links rápidos** seção, selecione **painéis do Cluster**e, em seguida, selecione **Jupyter Notebook** da folha de Cluster Dashboard__ hello.

    ![painéis do cluster Olá](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. No hello canto superior direito da página de Jupyter hello, selecione **novo**e, em seguida, **Scala**. Uma nova guia do navegador contendo um Bloco de anotações do Jupyter com base em Scala é exibida.
3. No primeiro campo de saudação (chamado um **célula**) na página de hello, digite Olá texto a seguir:

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    Esse código define a estrutura de diretórios de saudação do Spark toorecursively acesso para dados de entrada hello. Dados de telemetria do Application Insights conectado tooa estrutura de diretórios semelhante muito`/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Use **SHIFT + ENTER** toorun código de saudação. Em Olá lado esquerdo da célula hello, um '\*' aparece entre Olá colchetes tooindicate que código Olá nesta célula está sendo executado. Depois que ele for concluído, hello '\*' altera tooa número e a saída semelhante toohello texto a seguir é exibida abaixo de célula hello:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. É criada uma nova célula abaixo Olá um primeiro. Digite hello depois do texto na célula de novo hello. Substituir `CONTAINER` e `STORAGEACCOUNT` com o nome de conta de armazenamento do Azure hello e o nome do contêiner de blob que contém informações de aplicativo registra em log.

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Use **SHIFT + ENTER** tooexecute esta célula. Você verá um toohello semelhante resultado texto a seguir:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    caminho de wasb Olá retornado é o local de saudação do hello dados de telemetria do Application Insights. Saudação de alteração `hdfs dfs -ls` Olá célula toouse Olá wasb caminho retornado de linha e, em seguida, usar **SHIFT + ENTER** toorun célula de saudação novamente. Neste momento, os resultados de saudação devem exibir diretórios Olá que contêm dados de telemetria.

   > [!NOTE]
   > Olá para restante Olá Olá as etapas nesta seção, `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` diretório foi usado. Este diretório pode não existir, a menos que os dados de telemetria sejam para um aplicativo Web.

6. Na célula de Avançar hello, insira Olá código a seguir: substituir `WASB\_PATH` com caminho de saudação da etapa anterior hello.

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    Esse código cria um dataframe de arquivos JSON hello exportados pelo processo de exportação contínua hello. Use **SHIFT + ENTER** toorun esta célula.

7. Na próxima célula de Olá, digite e execute Olá esquema Olá tooview Spark criado para os arquivos JSON Olá a seguir:

   ```scala
   jsonData.printSchema
   ```

    saudação de esquema para cada tipo de telemetria é diferente. Olá, exemplo a seguir é esquema Olá que é gerada para solicitações da web (dados armazenados em Olá `Requests` subdiretório):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. Use Olá após tooregister Olá dataframe como uma tabela temporária e executar uma consulta em relação aos dados hello:

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    Essa consulta retorna informações de cidade Olá para registros de 20 principais Olá onde context.location.city não é nulo.

   > [!NOTE]
   > estrutura de contexto Hello está presente em toda a telemetria registrada pelo Application Insights. elemento de cidade Olá não pode ser preenchido em seus logs. Use Olá esquema tooidentify outros elementos que você pode consultar que podem conter dados para seus logs.
   >
   >

    Esta consulta retorna informações toohello semelhante texto a seguir:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>Próximas etapas

Para obter mais exemplos de como usar toowork Spark com dados e serviços no Azure, consulte Olá documentos a seguir:

* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

Para obter informações sobre como criar e executar Spark aplicativos, consulte Olá documentos a seguir:

* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)
