---
title: "Kit de Ferramentas do Azure para IntelliJ – Depurar aplicativos Spark remotamente por meio do SSH | Microsoft Docs"
description: "Orientações passo a passo sobre como toouse ferramentas HDInsight no Kit de ferramentas do Azure para aplicativos de toodebug IntelliJ remotamente no HDInsight clusters por meio do SSH"
keywords: "depurar o intellij remotamente, depuração remota do intellij, ssh, intellij, hdinsight, depurar o intellij, depuração"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>Depurar aplicativos Spark em um cluster HDInsight com o Kit de Ferramentas do Azure para IntelliJ por meio do SSH

Este artigo fornece orientação passo a passo sobre como toouse ferramentas HDInsight no Kit de ferramentas do Azure para IntelliJ toodebug aplicativos remotamente em um cluster HDInsight. toodebug seu projeto, você também pode exibir uma saudação [aplicativos de depurar HDInsight Spark com o Kit de ferramentas do Azure para IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) vídeo.

**Pré-requisitos**

* **Ferramentas do HDInsight no Kit de Ferramentas do Azure para IntelliJ**. Essa ferramenta faz parte do Kit de Ferramentas do Azure para IntelliJ. Para mais informações, consulte [Instalar o Kit de Ferramentas do Azure para IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).
* **Kit de Ferramentas do Azure para IntelliJ**. Use estes aplicativos de Spark toocreate Kit de ferramentas para um cluster HDInsight. Para obter mais informações, siga as instruções de saudação em [Kit de ferramentas do uso do Azure para aplicativos de Spark toocreate IntelliJ para um cluster HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).
* **Serviço SSH do HDInsight com gerenciamento de nome de usuário e senha**. Para obter mais informações, consulte [conectar tooHDInsight (Hadoop) usando o SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [usar SSH túnel tooaccess Ambari web da interface do usuário, JobHistory, NameNode, Oozie e outras interfaces do usuário da web](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel). 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a>Criar um aplicativo Spark Scala e configurá-lo para depuração remota

1. Inicie o IDEA do IntelliJ e crie um projeto. Em Olá **novo projeto** caixa de diálogo caixa, Olá a seguir:

   a. Selecione **HDInsight**. 

   b. Selecione um modelo Java ou Scala com base em sua preferência. Selecione entre hello as opções a seguir:

      - **Spark no HDInsight (Scala)**

      - **Spark no HDInsight (Java)**

      - **Amostra de execução do Spark no Cluster HDInsight (Scala)**

      Este exemplo usa um modelo de **Amostra de Execução do Spark no Cluster do HDInsight (Scala)**.

   c. Em Olá **ferramenta de compilação** , selecione qualquer uma das Olá a seguir, de acordo com a necessidade de tooyour:

      - **Maven**, para obter suporte ao assistente de criação de projetos Scala

      -  **SBT**, para gerenciar dependências hello e criação de projeto de Scala Olá 

      ![Criar um projeto de depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   d. Selecione **Avançar**.     
 
3. Em Olá próximo **novo projeto** janela, Olá a seguir:

   ![Selecione Olá Spark SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   a. Insira um nome de projeto e o local do projeto.

   b. Em Olá **projeto SDK** lista suspensa, selecione **Java 1.8** para **despertar 2. x** do cluster ou selecione **Java 1.7** para **Spark 1. x** cluster.

   c. Em Olá **versão Spark** lista suspensa, o Assistente de criação de projeto Olá Scala se integra a versão correta do Olá para Spark SDK e Scala SDK. Se a versão do cluster spark Olá for anterior à 2.0, selecione **despertar 1. x**. Caso contrário, selecione **Spark 2.x.** Esse exemplo usa o **Spark 2.0.2 (Scala 2.11.8)**.

   d. Selecione **Concluir**.

4. Selecione **src** > **principal** > **scala** tooopen seu código no projeto de saudação. Este exemplo usa Olá **SparkCore_wasbloTest** script.

5. Olá tooaccess **editar configurações** menu, ícone Olá seleção no canto superior direito de saudação. Nesse menu, você pode criar ou editar as configurações de saudação para depuração remota.

   ![Editar configurações](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. Em Olá **configurações de execução/depuração** caixa de diálogo, selecione hello mais sinal (**+**). Em seguida, selecione Olá **enviar trabalho de Spark** opção.

   ![Adicionar nova configuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. Insira as informações em **Nome**, **Cluster do Spark** e **Nome da classe principal**. Em seguida, selecione **Configurações avançadas**. 

   ![Executar configurações de depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. Em Olá **configuração avançada de envio Spark** caixa de diálogo, selecione **depuração remota Spark habilitar**. Insira nome de usuário do hello SSH, digite uma senha ou usar um arquivo de chave privado. configuração de saudação toosave, selecione **Okey**.

   ![Habilitar depuração remota do Spark](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. configuração Olá agora é salvo com o nome hello fornecido. detalhes da configuração tooview Olá, nome da configuração Olá select. alterações de toomake, selecione **editar configurações**. 

10. Depois de concluir as definições de configuração Olá, você pode executar o projeto de saudação no cluster remoto hello ou realizar a depuração remota.

## <a name="learn-how-tooperform-remote-debugging"></a>Saiba como tooperform a depuração remota
### <a name="scenario-1-perform-remote-run"></a>Cenário 1: realizar a execução remota

Nesta seção, mostraremos como toodebug executores e drivers.

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. Configurar pontos de quebra e, em seguida, selecione Olá **depurar** ícone.

   ![Selecione o ícone de depuração Olá](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. Quando a execução do programa hello atinge o ponto de interrupção Olá, você verá um **Driver** guia e dois **Executor** guias no hello **depurador** painel. Selecione Olá **retomar programa** toocontinue ícone executar código hello, que atinge o próximo ponto de interrupção de saudação e enfoca Olá correspondente **Executor** guia. Você pode examinar os logs de execução de saudação em Olá correspondente **Console** guia.

   ![Guia depuração](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a>Cenário 2: Executar depuração remota e correção de bugs
Nesta seção, mostraremos como toodynamically atualização Olá valor de variável usando Olá IntelliJ capacidade para uma solução simple de depuração. Em Olá exemplo de código a seguir, uma exceção será lançada porque já existe um arquivo de destino de saudação.
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a>depuração remota de tooperform e correção de bug
1. Configurar dois pontos de quebra e selecione Olá **depurar** Olá de toostart ícone processo de depuração remota.

2. código Olá para Olá primeiro ponto de interrupção e parâmetro hello e informações de variáveis são mostrados no hello **variáveis** painel. 

3. Selecione Olá **retomar programa** toocontinue ícone. Olá para de código no segundo ponto de saudação. exceção de saudação é detectada conforme o esperado.

  ![Gerar erro](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. Selecione Olá **retomar programa** ícone novamente. Olá **HDInsight Spark envio** janela exibe um erro "Falha na execução de trabalho".

  ![Envio de erro](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. toodynamically atualização Olá valor variável usando o recurso de depuração de IntelliJ hello, selecione **depurar** novamente. Olá **variáveis** painel é exibida novamente. 

6. Destino de saudação com o botão direito em Olá **depurar** guia e, em seguida, selecione **definir valor**. Em seguida, insira um novo valor para a variável de saudação. Em seguida, selecione **Enter** toosave valor de saudação. 

  ![Definir valor](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. Selecione Olá **retomar programa** programa de saudação do ícone toocontinue toorun. Neste momento, nenhuma exceção é detectada. Você pode ver o que projeto Olá for executado com êxito sem exceções.

  ![Depurar sem exceção](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>Próximas etapas
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demonstração
* Criar projeto do Scala (vídeo): [Criar aplicativos Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Depuração remota (vídeo): [Kit de ferramentas do uso do Azure para aplicativos de Spark toodebug IntelliJ remotamente em um cluster HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com o aprendizado de máquina: Use o Spark no HDInsight tooanalyze criação temperatura usando dados HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: Use Spark no HDInsight toobuild aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Use o Kit de ferramentas do Azure para aplicativos de Spark toocreate IntelliJ para um cluster HDInsight](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio de VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Use as ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações do Jupyter no cluster do hello Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)
