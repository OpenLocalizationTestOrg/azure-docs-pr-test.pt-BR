---
title: 'Kit de Ferramentas do Azure para IntelliJ: criar aplicativos Spark para um cluster HDInsight | Microsoft Docs'
description: "Use Olá Kit de ferramentas do Azure para os aplicativos IntelliJ toodevelop Spark escritos em Scala e enviá-los tooan cluster HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Use o Kit de ferramentas do Azure para aplicativos de Spark toocreate IntelliJ para um cluster HDInsight

Use Olá Kit de ferramentas do Azure para aplicativos de Spark toodevelop plug-in IntelliJ escritos em Scala e, em seguida, enviá-los tooan cluster HDInsight Spark diretamente do ambiente de desenvolvimento integrado Olá IntelliJ (IDE). Você pode usar o plug-in de algumas maneiras de saudação:

* Desenvolver e enviar um aplicativo Scala Spark em um cluster HDInsight Spark.
* Acessar os recursos de cluster Spark do Azure HDInsight.
* Desenvolver e executar um aplicativo Scala Spark localmente.

toocreate seu projeto, a saudação de exibição [criar aplicativos de Spark com hello Azure Toolkit for IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) vídeo.

> [!IMPORTANT]
> Você pode usar esse plug-in toocreate e enviar aplicativos apenas para um cluster HDInsight Spark no Linux.
> 

## <a name="prerequisites"></a>Pré-requisitos

- Um cluster do Apache Spark no HDInsight no Linux. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
- Kit de desenvolvimento Oracle Java. Você pode instalá-lo de saudação [site Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. Este artigo usa a versão 2017.1. Você pode instalá-lo de saudação [JetBrains site](https://www.jetbrains.com/idea/download/).

## <a name="install-azure-toolkit-for-intellij"></a>Instalar Kit de Ferramentas do Azure para IntelliJ
Para obter instruções de instalação, confira [Instalação do Kit de Ferramentas do Azure para IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="sign-in-tooyour-azure-subscription"></a>Entrar tooyour assinatura do Azure

1. Inicie Olá IntelliJ IDE e abra o Gerenciador do Azure. Em Olá **exibição** menu, selecione **janelas de ferramentas**e, em seguida, selecione **Azure Explorer**.
       
   ![link do Hello Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. Saudação de atalho **Azure** nó e selecione **entrar**.

3. Em Olá **Azure entrar** caixa de diálogo, selecione **entrar**e, em seguida, insira suas credenciais do Azure.

    ![Hello Azure caixa de diálogo Conecte](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. Depois que você está conectado, Olá **selecione assinaturas** Olá a caixa de diálogo lista todos os Olá assinaturas do Azure que são associadas com as credenciais. Selecione Olá **selecione** botão.

    ![caixa de diálogo Selecionar assinaturas Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. Em Olá **Azure Explorer** guia, expanda **HDInsight** Olá tooview HDInsight Spark clusters que estão em sua assinatura.
   
    ![Clusters Spark do HDInsight no Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. tooview Olá recursos (por exemplo, contas de armazenamento) que estão associados com cluster hello, você pode expandir ainda mais um nó do nome do cluster.
   
    ![Um nó de nome de cluster expandido](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Executar um aplicativo Scala Spark em um cluster HDInsight Spark

1. Inicie o IDEA do IntelliJ e crie um projeto. Em Olá **novo projeto** caixa de diálogo caixa, Olá a seguir: 

   a. Selecione **HDInsight** > **Spark no HDInsight (Scala)**.

   b. Em Olá **ferramenta de compilação** , selecione qualquer uma das Olá a seguir, de acordo com a necessidade de tooyour:

      * **Maven**, para obter suporte ao assistente de criação de projetos Scala
      * **SBT**, para gerenciar dependências hello e criação de projeto de Scala Olá

    ![caixa de diálogo Novo projeto Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. Selecione **Avançar**.

3. Assistente de criação do projeto Scala Olá detecta automaticamente se você instalou Olá Scala plug-in. Selecione **Instalar**.

   ![Verificação do plug-in Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Olá toodownload Scala plug-in, selecione **Okey**. Siga as instruções de saudação toorestart IntelliJ. 

   ![caixa de diálogo Instalação do plug-in de Scala Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. Em Olá **novo projeto** janela, Olá a seguir:  

    ![Selecionando Olá Spark SDK](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. Insira um nome e o local do projeto.

   b. Em Olá **projeto SDK** lista suspensa, selecione **Java 1.8** para cluster de 2. x Spark hello, ou selecione **Java 1.7** para cluster 1. x do hello Spark.

   c. Em Olá **versão Spark** lista suspensa, o Assistente de criação de projeto Scala se integra a versão correta do Olá para Spark SDK e Scala SDK. Se a versão do cluster Spark Olá for anterior à 2.0, selecione **despertar 1. x**. Caso contrário, selecione **Spark 2.x**. Esse exemplo usa o **Spark 2.0.2 (Scala 2.11.8)**.

6. Selecione **Concluir**.

7. projeto do Spark Olá cria automaticamente um artefato para você. artefato de saudação tooview, Olá a seguir:

   a. Em Olá **arquivo** menu, selecione **estrutura do projeto**.

   b. Em Olá **estrutura do projeto** caixa de diálogo, selecione **artefatos** tooview artefato de padrão de saudação que é criado. Você também pode criar seu próprios artefato selecionando o sinal de adição hello (**+**).

      ![Informações de artefato na caixa de diálogo Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. Adicione seu código-fonte aplicativo hello seguinte:

   a. No Explorador de projeto, clique com botão direito **src**, ponto muito**novo**e, em seguida, selecione **Scala classe**.
      
      ![Comandos para criar uma classe Scala do Explorador do Projeto](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. Em Olá **criar nova classe Scala** caixa de diálogo caixa, forneça um nome, selecione **objeto** em Olá **tipo** caixa e, em seguida, selecione **Okey**.
      
      ![Criar caixa de diálogo Nova Classe Scala](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. Em Olá **MyClusterApp.scala** de arquivos, cole Olá código a seguir. Olá código lê os dados de saudação do HVAC.csv (disponível em todos os clusters de HDInsight Spark), recupera linhas de saudação que têm apenas um dígito na coluna de sétimo Olá no arquivo CSV de saudação e grava a saída de hello muito**/HVACOut** em padrão Olá contêiner de armazenamento de cluster hello.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Execute o aplicativo hello em um cluster HDInsight Spark fazendo Olá seguinte:

   a. No Explorador de projeto, nome do projeto hello e, em seguida, selecione **tooHDInsight enviar Spark aplicativo**.
      
      ![saudação de comando do aplicativo do Spark enviar tooHDInsight](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. Você está tooenter solicitada as credenciais de assinatura do Azure. Em Olá **envio Spark** caixa de diálogo, forneça Olá valores a seguir e, em seguida, selecione **enviar**.
      
      * Para **despertar clusters (Linux)**, selecione o aplicativo de cluster HDInsight Spark no qual você deseja toorun hello.

      * Selecione um artefato do projeto de IntelliJ hello, ou selecione um na unidade de disco rígido hello.

      * Em Olá **nome da classe principal** caixa reticências Olá select (**...** ), selecione a classe principal da saudação no código fonte do aplicativo e, em seguida, selecione **Okey**.

        ![caixa de diálogo Selecionar classe do principal Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * Porque o código do aplicativo hello neste exemplo não exigem argumentos de linha de comando ou referência JARs ou arquivos, você pode deixar Olá restantes caixas vazias. Depois de fornecer todas as informações de hello, caixa de diálogo Olá deve se assemelhar Olá a imagem a seguir.
        
        ![caixa de diálogo de envio Spark Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. Olá **envio Spark** guia na parte inferior da saudação da janela Olá deve iniciar exibindo andamento hello. Você também pode interromper o aplicativo hello, selecionando o botão Olá vermelho no hello **envio Spark** janela.
      
      ![janela de envio Spark Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn como tooaccess Olá saída de trabalho, consulte hello "acesso e gerenciar clusters de HDInsight Spark usando o Kit de ferramentas do Azure para IntelliJ" seção mais adiante neste artigo.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Executar ou depurar um aplicativo Scala Spark em um cluster Spark do HDInsight
Também é recomendável outra maneira de envio de cluster de toohello de aplicativo hello Spark. Você pode fazer isso definindo parâmetros de saudação no hello **configurações de execução/depuração** IDE. Para saber mais, confira [Depurar aplicativos Spark remotamente em um cluster HDInsight com o kit de ferramentas do Azure para IntelliJ por meio do SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>Acessar e gerenciar clusters Spark do HDInsight usando o Kit de Ferramentas do Azure para IntelliJ
Você pode executar várias operações usando o Kit de Ferramentas do Azure para IntelliJ.

### <a name="access-hello-job-view"></a>Modo de exibição de trabalho do Access Olá
1. No Pesquisador de objetos do Azure, expanda **HDInsight**, expanda o nome do cluster Spark hello e, em seguida, selecione **trabalhos**.  

    ![Nó de exibição de trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. No painel direito da saudação, Olá **Spark trabalho exibição** guia exibe todos os aplicativos de saudação que foram executados no cluster de saudação. Selecione o nome de saudação do aplicativo hello para o qual você deseja toosee obter mais detalhes.

    ![Detalhes do aplicativo](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay executando trabalho informações básicas, passe o mouse sobre o gráfico de trabalho hello. gráfico de estágios de saudação tooview e informações que gera todos os trabalhos, selecione um nó no gráfico de trabalho hello.

    ![Detalhes do estágio do trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. tooview os logs, usados com frequência, como *Driver Stderr*, *Driver Stdout*, e *informações do diretório*, selecione Olá **Log** guia.

    ![Detalhes do log](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. Você também pode exibir hello histórico Spark da interface do usuário e Olá YARN da interface do usuário (em nível de aplicativo hello) selecionando um link na parte superior de saudação da janela de saudação.

### <a name="access-hello-spark-history-server"></a>Servidor de histórico do acesso Olá Spark
1. No Azure Explorer, expanda o **HDInsight**, clique com o botão direito do mouse no nome do cluster Spark e selecione **Abrir IU do Histórico Spark**. 

2. Quando você for solicitado, insira as credenciais de administrador do cluster hello, que você especificou ao configurar o cluster de saudação.

3. No painel de servidor do histórico do Spark hello, você pode usar Olá toolook de nome de aplicativo para o aplicativo hello que você acabou de execução. Em Olá precede o código, você definir nome do aplicativo hello usando `val conf = new SparkConf().setAppName("MyClusterApp")`. Portanto, o nome do aplicativo Spark é **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Iniciar o portal do Ambari Olá
1. No Azure Explorer, expanda **HDInsight**, clique com o botão direito do mouse no nome do cluster Spark e selecione **Abrir Portal de Gerenciamento do Cluster (Ambari)**. 

2. Quando você for solicitado, insira as credenciais de administrador de saudação para cluster hello. Você especificou essas credenciais durante o processo de instalação de cluster hello.

### <a name="manage-azure-subscriptions"></a>Gerenciar assinaturas do Azure
Por padrão, o Kit de ferramentas do Azure para IntelliJ lista clusters do Spark saudação de todas as suas assinaturas do Azure. Se necessário, você pode especificar que você deseja tooaccess de assinaturas de saudação. 

1. No Pesquisador de objetos do Azure, clique com botão direito Olá **Azure** nó raiz e, em seguida, selecione **gerenciar assinaturas**. 

2. Na caixa de diálogo hello, desmarque Olá caixas de seleção próxima toohello assinaturas que não deseja tooaccess e, em seguida, selecione **fechar**. Você também pode selecionar **sair** se deseja toosign fora de sua assinatura do Azure.

## <a name="run-a-spark-scala-application-locally"></a>Executar um aplicativo Scala Spark localmente
Você pode usar o Kit de ferramentas do Azure para IntelliJ toorun Spark Scala aplicativos localmente em sua estação de trabalho. Olá aplicativos geralmente não precisam acessar toocluster recursos, como contêineres de armazenamento, e você pode executar e testá-las localmente.

### <a name="prerequisite"></a>Pré-requisito
Durante a execução do aplicativo do Olá local Spark Scala em um computador Windows, você pode obter uma exceção, conforme explicado em [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). ocorrerá uma exceção de saudação porque WinUtils.exe está ausente no Windows. 

tooresolve esse erro, [baixar Olá executável](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa local como **C:\WinUtils\bin**. Em seguida, adicione a variável de ambiente Olá **HADOOP_HOME**e defina o valor de saudação da variável de saudação muito**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Executar um aplicativo Scala Spark local
1. Inicie o IDEA do IntelliJ e crie um projeto. 

2. Em Olá **novo projeto** caixa de diálogo caixa, Olá a seguir:
   
    a. Escolha **HDInsight** > **Exemplo de Execução Local do Spark no HDInsight (Scala)**.

    b. Em Olá **ferramenta de compilação** , selecione qualquer uma das Olá a seguir, de acordo com a necessidade de tooyour:

      * **Maven**, para obter suporte ao assistente de criação de projetos Scala
      * **SBT**, para gerenciar dependências hello e criação de projeto de Scala Olá

    ![caixa de diálogo Novo projeto Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. Selecione **Avançar**.
 
4. Na próxima janela de hello, Olá a seguir:
   
    a. Insira um nome e o local do projeto.

    b. Em Olá **projeto SDK** lista suspensa, selecione uma versão de Java é posterior à versão 1.7.

    c. Em Olá **versão Spark** lista suspensa, versão select Olá de Scala que você deseja toouse: Scala 2.11.x Spark 2.0 ou Scala 2.10.x para Spark 1.6.

    ![caixa de diálogo Novo projeto Olá](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. Selecione **Concluir**.

6. modelo de saudação adiciona um código de exemplo (**LogQuery**) em Olá **src** pasta pode ser executada localmente no seu computador.
   
    ![Local do LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. Saudação de atalho **LogQuery** aplicativo e, em seguida, selecione **execução 'LogQuery'**. Em Olá **executar** guia na parte inferior do hello, verá uma saída semelhante Olá seguinte:
   
   ![Resultado da execução local do aplicativo Spark](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>Converter toouse de aplicativos existente IDEIA IntelliJ Kit de ferramentas do Azure para IntelliJ
Você pode converter Olá Spark Scala os aplicativos existentes que você criou no IntelliJ IDEIA toobe compatível com o Kit de ferramentas do Azure para IntelliJ. Você pode usar Olá toosubmit plug-in Olá aplicativos tooan cluster HDInsight Spark.

1. Para um aplicativo Spark Scala existente que foi criado por meio de IntelliJ IDEIA, abra o arquivo de .iml associados de saudação.

2. Na raiz da saudação nível é um **módulo** elemento como Olá a seguir:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Editar saudação elemento tooadd `UniqueKey="HDInsightTool"` assim que Olá **módulo** elemento semelhante ao seguinte hello:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Salve alterações de saudação. Seu aplicativo deve ser compatível com o Kit de Ferramentas do Azure para IntelliJ. Você pode testá-lo clicando com o nome do projeto Olá no Explorador de projeto. menu pop-up Olá agora tem a opção de saudação **tooHDInsight enviar Spark aplicativo**.

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>Erro na execução local: *Use um tamanho de heap maior*
Spark 1.6, se você estiver usando um SDK de Java de 32 bits durante a execução local, você pode encontrar hello os erros a seguir:

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

Esses erros ocorrem porque o tamanho do heap Olá não é grande o suficiente para toorun Spark. O Spark requer pelo menos 471 MB. (Para saber mais, confira [SPARK-12081](https://issues.apache.org/jira/browse/SPARK-12081).) Uma solução simple é toouse um SDK de Java de 64 bits. Você também pode alterar configurações da JVM Olá IntelliJ adicionando Olá as opções a seguir:

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Adicionando opções toohello "Opções de VM" caixa IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>Perguntas frequentes
toosubmit um repositório do aplicativo tooAzure Data Lake, escolha **interativo** modo durante o processo de saudação entrada do Azure. Se você selecionar o modo **Automatizado**, obterá um erro.

![interative-signin](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

Isso já está resolvido. Você pode escolher um Cluster do Azure Data Lake toosubmit seu aplicativo com qualquer método de entrada.

## <a name="feedback-and-known-issues"></a>Comentários e problemas conhecidos
Atualmente, não há suporte para exibir saídas do Spark diretamente.

Se você tiver sugestões ou comentários, ou se encontrar problemas ao usar esse plug-in, envie-nos um email para hdivstool@microsoft.com.

## <a name="seealso"></a>Próximas etapas
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demonstração
* Criar projeto do Scala (vídeo): [Criar aplicativos Scala Spark](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Depuração remota (vídeo): [Kit de ferramentas do uso do Azure para aplicativos de Spark toodebug IntelliJ remotamente no HDInsight Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com o aprendizado de máquina: Use o Spark no HDInsight tooanalyze criação temperatura usando dados HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: Use Spark no HDInsight toobuild aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Criando e executando aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio de VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio do SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Use as ferramentas do HDInsight no Kit de ferramentas do Azure para aplicativos do Eclipse toocreate Spark](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Gerenciando recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

