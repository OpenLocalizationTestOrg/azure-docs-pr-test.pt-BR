---
title: pacotes de Maven personalizados aaaUse com Jupyter no Spark do Azure | Microsoft Docs
description: "Instruções passo a passo sobre como os clusters de anotações do Jupyter tooconfigure disponíveis com o HDInsight Spark pacotes personalizados de Maven toouse."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Usar pacotes externos com blocos de anotações Jupyter em clusters Apache Spark no HDInsight
> [!div class="op_single_selector"]
> * [Usando a mágica da célula](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Usando a ação de script](hdinsight-apache-spark-python-package-installation.md)
>
>

Saiba como tooconfigure um bloco de anotações do Jupyter no cluster do Apache Spark no HDInsight toouse externo, contribuído pela comunidade **maven** pacotes que não são incluídas de caixa Olá cluster. 

Você pode pesquisar Olá [Repositório Maven](http://search.maven.org/) para a lista completa de saudação dos pacotes que estão disponíveis. Você também pode obter uma lista de pacotes disponíveis de outras fontes. Por exemplo, uma lista completa dos pacotes enviados pela comunidade está disponível em [Pacotes do Spark](http://spark-packages.org/).

Neste artigo, você aprenderá como Olá toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacote com anotações do Jupyter hello.



## <a name="prerequisites"></a>Pré-requisitos
Você deve ter o seguinte hello:

* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Usar pacotes externos com blocos de notas Jupyter
1. De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial). Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.   
2. Na folha de cluster do Spark hello, clique em **Links rápidos**e, em seguida, Olá **painel Cluster** folha, clique em **Jupyter Notebook**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.

    > [!NOTE]
    > Você também poderá atingir Olá anotações do Jupyter para o cluster por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Crie um novo bloco de anotações. Clique em **Novo** e em **Spark**.
   
    ![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Criar um novo bloco de anotações do Jupyter")

4. Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb. Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.
   
    ![Forneça um nome para o bloco de anotações de saudação](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "forneça um nome para o bloco de anotações de saudação")

5. Você usará Olá `%%configure` tooconfigure magic Olá notebook toouse um pacote externo. Em blocos de anotações que usam pacotes externos, certifique-se de chamar hello `%%configure` magic na primeira célula de código hello. Isso garante que kernel Olá pacote de saudação toouse configurado antes do início da sessão de saudação.

    >[!IMPORTANT] 
    >Se você esquecer tooconfigure kernel de saudação na primeira célula do hello, você pode usar o hello `%%configure` com hello `-f` parâmetro, mas que irá reiniciar a sessão de saudação e andamento todos serão perdido.

    | Versão do HDInsight | Command |
    |-------------------|---------|
    |Para HDInsight 3.3 e HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | Para HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. trecho de saudação acima espera Olá maven coordenadas para o pacote de saudação externo no repositório Central Maven. Neste trecho, `com.databricks:spark-csv_2.10:1.4.0` é coordenada maven Olá **spark csv** pacote. Aqui está como você constrói Olá coordenadas de um pacote.
   
    a. Localize o pacote de saudação em Olá Repositório Maven. Para este tutorial, usamos [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Do repositório de saudação reunir os valores hello para **GroupId**, **ArtifactId**, e **versão**. Verifique se você coletar os valores hello correspondem seu cluster. Nesse caso, estamos usando um pacote de Spark 1.4.0 e Scala 2.10, mas talvez seja necessário tooselect diferentes versões de versão apropriada Olá Scala ou Spark no cluster. Você pode descobrir Olá Scala versão no cluster executando `scala.util.Properties.versionString` no kernel do Spark Jupyter hello ou em envio Spark. Você pode descobrir Olá Spark versão no cluster executando `sc.version` em blocos de anotações do Jupyter.
   
    ![Usar pacotes externos com blocos de anotações do Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Usar pacotes externos com blocos de anotações do Jupyter")
   
    c. Concatenar valores hello três, separados por dois-pontos (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Execute a célula de código Olá com hello `%%configure` mágica. Isso configurará Olá subjacente Livy sessão toouse Olá pacote fornecido. Nas células de subsequentes Olá no bloco de anotações Olá, agora você pode usar o pacote de saudação, conforme mostrado abaixo.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. Você pode executar trechos Olá, como mostrado abaixo, tooview hello dados de dataframe de saudação você criou na etapa anterior Olá.
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões

* [Usar pacotes Python externos com notebooks Jupyter em clusters do Apache Spark no HDInsight Linux](hdinsight-apache-spark-python-package-installation.md)
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

