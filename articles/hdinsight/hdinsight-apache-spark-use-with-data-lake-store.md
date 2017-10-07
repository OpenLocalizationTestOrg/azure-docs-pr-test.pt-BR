---
title: "aaaUse dados de tooanalyze Apache Spark no repositório Azure Data Lake | Microsoft Docs"
description: "Executar trabalhos do Spark tooanalyze dados armazenados no repositório Azure Data Lake"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a>Usar dados de tooanalyze de cluster do HDInsight Spark no repositório Data Lake

Neste tutorial, você pode usar anotações do Jupyter disponível com clusters de HDInsight Spark toorun um trabalho que lê dados de uma conta do repositório Data Lake.

## <a name="prerequisites"></a>Pré-requisitos

* Conta do Azure Data Lake Store. Siga as instruções de saudação em [Introdução ao repositório Azure Data Lake usando hello Azure Portal](../data-lake-store/data-lake-store-get-started-portal.md).

* Cluster Spark HDInsight do Azure com o Data Lake Store como armazenamento. Siga as instruções de saudação em [criar um cluster HDInsight com repositório Data Lake usando o Portal do Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    
## <a name="prepare-hello-data"></a>Preparar dados Olá

> [!NOTE]
> Não é necessário tooperform esta etapa se você tiver criado o cluster do HDInsight Olá com repositório Data Lake como armazenamento padrão. processos de criação de cluster Olá adiciona alguns dados de exemplo na conta do repositório Data Lake Olá que você especificar durante a criação de cluster hello. Ignorar a seção toohello [cluster Use HDInsight Spark com repositório Data Lake](#use-an-hdinsight-spark-cluster-with-data-lake-store).
>
>

Se você criou um cluster HDInsight com repositório Data Lake como armazenamento adicional e Blob de armazenamento do Azure como armazenamento padrão, você deve primeiro copiar sobre alguns dados de exemplo toohello conta do repositório Data Lake. Você pode usar dados de exemplo de saudação do hello que blob de armazenamento do Azure associado com o cluster do HDInsight hello. Você pode usar o hello [ADLCopy ferramenta](http://aka.ms/downloadadlcopy) toodo para. Baixe e instale a ferramenta de saudação do link de saudação.

1. Abra um prompt de comando e navegue diretório toohello onde AdlCopy é instalado, normalmente `%HOMEPATH%\Documents\adlcopy`.

2. Execute Olá toocopy de comando a seguir um blob específico de saudação fonte contêiner tooa repositório Data Lake:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Saudação de cópia **HVAC.csv** do arquivo de dados de exemplo no **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello conta do repositório Azure Data Lake. trecho de código Olá deve parecer com:

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > Certifique-se de Olá arquivo e nomes de caminho estão em letra maiuscula hello.
   >
   >
3. Será tooenter solicitada credenciais Olá Olá assinatura do Azure sob a qual você tem a sua conta do repositório Data Lake. Você verá uma saída semelhante toohello a seguir:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    arquivo de dados da saudação (**HVAC.csv**) serão copiados em uma pasta **/hvac** em Olá conta do repositório Data Lake.

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a>Usar um cluster Spark HDInsight com o Data Lake Store

1. De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial). Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.

2. Na folha de cluster do Spark hello, clique em **Links rápidos**e, em seguida, Olá **painel Cluster** folha, clique em **Jupyter Notebook**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.

   > [!NOTE]
   > Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Crie um novo bloco de anotações. Clique em **Novo** e em **PySpark**.

    ![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Criar um novo bloco de anotações do Jupyter")

4. Como você criou um bloco de anotações com o hello PySpark kernel, não é necessário toocreate qualquer contextos explicitamente. contextos de Spark e Hive Olá serão automaticamente criados para você quando você executar a primeira célula de código hello. Você pode começar importando tipos de saudação necessários para este cenário. toodo assim, cole Olá seguindo o trecho de código em uma célula e pressione **SHIFT + ENTER**.

        from pyspark.sql.types import *

    Toda vez que você executa um trabalho em Jupyter, o título de janela de navegador da web mostrará uma **(ocupada)** status junto com o título do bloco de anotações de saudação. Você também verá um toohello próximo do círculo sólido **PySpark** texto no canto superior direito de saudação. Após o trabalho hello, isso alterará o círculo vazio tooa.

     ![Status de um trabalho de bloco de anotações Jupyter](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Status de um trabalho de bloco de anotações Jupyter")

5. Carregar dados de amostra em uma tabela temporária usando Olá **HVAC.csv** arquivo copiado toohello conta de repositório Data Lake. Você pode acessar dados de saudação na conta do repositório Data Lake hello usando saudação padrão de URL a seguir.

    * Se você tiver o repositório Data Lake como armazenamento padrão, HVAC.csv será toohello semelhante de caminho Olá URL a seguir:

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        Ou, você também pode usar um formato abreviado como seguinte hello:

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * Se você tiver o repositório Data Lake como armazenamento adicional, HVAC.csv será no hello local onde você copiou, tais como:

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     Em uma célula vazia, Olá cole o exemplo de código a seguir, substitua **MYDATALAKESTORE** com seu nome de conta do repositório Data Lake e pressione **SHIFT + ENTER**. Este exemplo de código registra dados saudação em uma tabela temporária chamada **hvac**.

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. Como você está usando um kernel PySpark, agora você pode diretamente executar uma consulta SQL na tabela temporária Olá **hvac** que você acabou de criar usando Olá `%%sql` mágica. Para obter mais informações sobre Olá `%%sql` magic, bem como outros magics disponíveis com o kernel do PySpark hello, consulte [Kernels disponíveis em blocos de anotações do Jupyter com clusters HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. Depois que o trabalho de saudação é concluído com êxito, Olá após a saída tabular é exibido por padrão.

      ![Saída do resultado de consulta de tabela](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Saída do resultado de consulta de tabela")

     Você também pode ver os resultados de saudação em outras visualizações também. Por exemplo, um gráfico de área para Olá a mesma saída seria semelhante a seguinte hello.

     ![Gráfico de área de resultado da consulta](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Gráfico de área de resultado da consulta")

8. Depois de terminar de executar o aplicativo hello, você deverá recursos de saudação do desligamento Olá notebook toorelease. toodo caso de Olá **arquivo** menu notebook hello, clique em **fechar e interromper**. Esta desligará e notebook Olá fechar.


## <a name="next-steps"></a>Próximas etapas

* [Crie um toorun de aplicativo autônomo Scala Apache Spark cluster](hdinsight-apache-spark-create-standalone-application.md)
* [Usar ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos de Spark toocreate IntelliJ para o cluster HDInsight Spark Linux](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Use as ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark para HDInsight Spark Linux cluster](hdinsight-apache-spark-eclipse-tool-plugin.md)
