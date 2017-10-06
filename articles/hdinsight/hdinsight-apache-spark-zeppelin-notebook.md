---
title: "cluster de blocos de anotações do aaaUse Zeppelin com o Apache Spark no Azure HDInsight | Microsoft Docs"
description: "Instruções passo a passo sobre como clusters de blocos de anotações do toouse Zeppelin com o Apache Spark no HDInsight do Azure."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>Usar notebooks Zeppelin com cluster Apache Spark no Azure HDInsight

Clusters de HDInsight Spark incluem notebooks Zeppelin que você pode usar trabalhos do Spark toorun. Neste artigo, você aprenderá como toouse Olá notebook Zeppelin em um cluster HDInsight.

> [!NOTE]
> Os blocos de anotações Zeppelin estão disponíveis apenas para Spark 1.6.3 no HDInsight 3.5 e Spark 2.1.0 no HDInsight 3.6.
>

**Pré-requisitos:**

* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="launch-a-zeppelin-notebook"></a>Inicie um notebook Zeppelin
1. Na folha de cluster do Spark hello, clique em **painel Cluster**e, em seguida, clique em **Zeppelin Notebook**. Se solicitado, insira as credenciais de administrador de saudação para cluster hello.
   
   > [!NOTE]
   > Você também pode acessar Olá Zeppelin Notebook para seu cluster por Olá abrir URL a seguir em seu navegador. Substituir **CLUSTERNAME** com nome de saudação do cluster:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. Crie um novo bloco de anotações. No painel de cabeçalho hello, clique em **Notebook**e, em seguida, clique em **criar nova anotação**.
   
    ![Criar um novo notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "Criar um novo notebook Zeppelin")
   
    Insira um nome para o bloco de anotações hello e, em seguida, clique em **criar anotação**.
3. Além disso, certifique-se de cabeçalho do bloco de anotações de saudação mostrará um status conectado. Ele é indicado por um ponto verde no canto superior direito de saudação.
   
    ![Status do notebook Zeppelin](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Status do notebook Zeppelin")
4. Carregar dados de exemplo em uma tabela temporária. Quando você cria um cluster Spark no HDInsight, arquivo de dados de exemplo hello, **hvac.csv**, é copiado toohello associado a conta de armazenamento em **\HdiSamples\SensorSampleData\hvac**.
   
    No parágrafo vazio Olá que é criado por padrão no novo bloco de anotações de hello, cole Olá trecho de código a seguir.
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    Pressione **SHIFT + ENTER** ou clique em Olá **reproduzir** botão de trecho de código da saudação toorun Olá parágrafo. status Olá no canto direito de saudação do parágrafo Olá deve avançar de READY, pendente, tooFINISHED em execução. saída de Hello aparece na parte inferior de saudação do hello mesmo paragraph. captura de tela de saudação semelhante ao seguinte hello:
   
    ![Criar uma tabela temporária a partir de dados brutos](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "Criar uma tabela temporária a partir de dados brutos")
   
    Você também pode fornecer um parágrafo de tooeach do título. No canto superior direito da saudação, clique em Olá **configurações** ícone e clique **Mostrar título**.
5. Agora você pode executar instruções SQL Spark no hello **hvac** tabela. Colar Olá consulta em um novo parágrafo a seguir. consulta Olá recupera a ID de construção de hello e diferença de saudação entre destino hello e temperaturas reais para cada prédio em uma determinada data. Pressione **SHIFT+ENTER**.
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    Olá **% sql** instrução no início de saudação informa ao interpretador de Livy Scala Olá notebook toouse hello.
   
    Hello seguinte captura de tela mostra a saída de hello.
   
    ![Executar uma instrução SQL do Spark usando notebook Olá](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "executar uma instrução SQL Spark usando o bloco de anotações de saudação")
   
     Clique em Olá exibição Opções (destacado no retângulo) tooswitch entre diferentes representações de saudação mesma saída. Clique em **configurações** toochoose que consitutes Olá chave e valores na saída de hello. Olá captura de tela acima usa **buildingID** hello e média de saudação do **temp_diff** como valor de saudação.
6. Você também pode executar instruções SQL Spark usando variáveis na consulta de saudação. Olá Avançar mostra de trecho de código como toodefine uma variável, **Temp**, na consulta Olá com os valores possíveis Olá deseja tooquery com. Ao executar consulta Olá pela primeira vez, uma lista suspensa automaticamente é preenchida com valores de saudação especificado para a variável de saudação.
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    Cole esse trecho em um novo parágrafo e pressione **SHIFT+ENTER**. Hello seguinte captura de tela mostra a saída de hello.
   
    ![Executar uma instrução SQL do Spark usando notebook Olá](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "executar uma instrução SQL Spark usando o bloco de anotações de saudação")
   
    Para as consultas subsequentes, você pode selecionar um novo valor na lista suspensa hello e execute a consulta de saudação novamente. Clique em **configurações** toochoose que consitutes Olá chave e valores na saída de hello. Olá captura de tela acima usa **buildingID** como chave Olá Olá médio de **temp_diff** como valor de saudação e **targettemp** como grupo hello.
7. Reinicie Olá aplicativo hello do Livy interpretador tooexit. toodo isso, abra as configurações do interpretador clicando Olá registrado no nome de usuário do canto superior direito de saudação e, em seguida, clique em **interpretador**.
   
    ![Iniciar o intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Saída do Hive")
8. Role a tela de configurações do interpretador tooLivy e, em seguida, clique em **reiniciar**.
   
    ![Reiniciar Olá Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "reiniciar Olá Zeppelin intepreter")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>Como usar pacotes externos com notebook Olá?
Você pode configurar o bloco de anotações do hello Zeppelin no cluster do Apache Spark no HDInsight (Linux) toouse externo contribuído pela comunidade de pacotes que não são incluídos-a-prontos cluster hello. Você pode pesquisar Olá [Repositório Maven](http://search.maven.org/) para a lista completa de saudação dos pacotes que estão disponíveis. Você também pode obter uma lista de pacotes disponíveis de outras fontes. Por exemplo, uma lista completa dos pacotes enviados pela comunidade está disponível em [Pacotes do Spark](http://spark-packages.org/).

Neste artigo, você verá como Olá toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacote com anotações do Jupyter hello.

1. Abra as configurações do interpretador. Do canto superior direito de saudação, clique em Olá registrado no nome de usuário e, em seguida, clique em **interpretador**.
   
    ![Iniciar o intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Saída do Hive")
2. Role a tela de configurações do interpretador tooLivy e, em seguida, clique em **editar**.
   
    ![Alterar configurações do intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "Alterar configurações do intérprete")
3. Adicionar uma nova chave chamada **livy.spark.jars.packages** e defina seu valor no formato de saudação `group:id:version`. Portanto, se você deseja Olá toouse [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pacote, você deve definir a saudação valor da chave de saudação muito`com.databricks:spark-csv_2.10:1.4.0`.
   
    ![Alterar configurações do intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "Alterar configurações do intérprete")
   
    Clique em **salvar** e, em seguida, reinicie Olá interpretador Livy.
4. **Dica**: se você quiser toounderstand como tooarrive no valor de saudação da chave Olá inserido acima, aqui está como.
   
    a. Localize o pacote de saudação em Olá Repositório Maven. Para este tutorial, usamos [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Do repositório de saudação reunir os valores hello para **GroupId**, **ArtifactId**, e **versão**.
   
    ![Usar pacotes externos com blocos de anotações do Jupyter](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Usar pacotes externos com blocos de anotações do Jupyter")
   
    c. Concatenar valores hello três, separados por dois-pontos (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>Onde está Olá notebooks Zeppelin salvados?
blocos de anotações do Hello Zeppelin são salvos toohello headnodes de cluster. Portanto, se você excluir o cluster hello, notebooks Olá também serão excluídos. Se você quiser toopreserve seus blocos de anotações para uso posterior em outros clusters, você deve exportá-los depois de concluir a saudação de trabalhos em execução. tooexport um bloco de anotações, clique em Olá **exportar** ícone conforme mostrado na imagem de saudação abaixo.

![Baixar notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "notebook de saudação do Download")

Isso economiza notebook hello como um arquivo JSON em seu local de download.

## <a name="livy-session-management"></a>Gerenciamento de sessões do Livy
Quando você executa o primeiro parágrafo de código Olá no bloco de anotações Zeppelin, uma nova sessão Livy é criada em seu cluster HDInsight Spark. Essa sessão será compartilhada entre todos os notebooks Zeppelin que você criar posteriormente. Se, por algum Olá motivo Livy sessão for interrompida (reinicialização de cluster, etc.), não será capaz de toorun trabalhos do bloco de anotações de Zeppelin hello.

Nesse caso, você deve executar Olá etapas a seguir antes de iniciar trabalhos em execução de um bloco de anotações de Zeppelin. 

1. Reinicie Olá interpretador Livy do bloco de anotações de Zeppelin hello. toodo isso, abra as configurações do interpretador clicando Olá registrado no nome de usuário do canto superior direito de saudação e, em seguida, clique em **interpretador**.
   
    ![Iniciar o intérprete](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Saída do Hive")
2. Role a tela de configurações do interpretador tooLivy e, em seguida, clique em **reiniciar**.
   
    ![Reiniciar Olá Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "reiniciar Olá Zeppelin intepreter")
3. Execute uma célula de código de um notebook Zeppelin existente. Isso cria uma nova sessão Livy no cluster do HDInsight hello.

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
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar maiores Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







