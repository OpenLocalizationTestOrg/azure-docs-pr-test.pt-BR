---
title: aaaAzure Kit de ferramentas do Eclipse - Scala criar aplicativos para HDInsight Spark | Microsoft Docs
description: "Usar ferramentas do HDInsight no Kit de ferramentas do Azure para os aplicativos Eclipse toodevelop Spark escritos em Scala e enviá-los tooan cluster HDInsight Spark, diretamente a partir deles Olá IDE do Eclipse."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Use o Kit de ferramentas do Azure para aplicativos de Spark toocreate Eclipse para um cluster HDInsight

Use ferramentas do HDInsight no Kit de ferramentas do Azure para Eclipse toodevelop despertar aplicativos escritos em Scala e enviá-los em cluster do Spark no HDInsight tooan, diretamente do hello IDE do Eclipse. Você pode usar as ferramentas do HDInsight Olá plug-in de algumas maneiras diferentes:

* toodevelop e enviar um aplicativo Scala Spark em um cluster HDInsight Spark
* tooaccess seus recursos de cluster do Spark no HDInsight
* toodevelop e executar um aplicativo Scala Spark localmente

> [!IMPORTANT]
> Essa ferramenta pode ser usada toocreate e enviar aplicativos apenas para um cluster HDInsight Spark no Linux.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos

* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit versão 8, que é usado para o tempo de execução do hello IDE do Eclipse. Você pode baixá-lo do hello [site Oracle](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Eclipse IDE. Este artigo usa o Eclipse Neon. Você pode instalá-lo de saudação [site Eclipse](https://www.eclipse.org/downloads/).   
* Spark SDK. Você pode baixá-lo do [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>Instalar as ferramentas do HDInsight no Kit de ferramentas do Azure para Eclipse e Scala plug-in
### <a name="install-hdinsight-tools"></a>Instalar Ferramentas do HDInsight
As Ferramentas do HDInsight para Eclipse estão disponíveis como parte do Kit de Ferramentas do Azure para Eclipse. Para obter instruções de instalação, consulte [Instalando o Kit de Ferramentas do Azure para Eclipse](../azure-toolkit-for-eclipse-installation.md).
### <a name="install-scala-plugin"></a>Instalar o plug-in de Scala
Quando você abre Olá Intellij, Olá ferramentas HDInsight automaticamente detecta se você instalou Scala plug-in ou não. Clique em **Okey** toocontinue e siga Olá tooinstall de instruções por Olá Marketplace do Eclipse.

 ![Plug-in Scala de instalação automática](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>Entrar tooyour assinatura do Azure
1. Inicie Olá IDE do Eclipse e abra o Gerenciador do Azure. Em Olá **janela** menu, clique em **exibição**e, em seguida, clique em **outros**. Na caixa de diálogo de saudação que é aberta, expanda **Azure**, clique em **Azure Explorer**e, em seguida, clique em **Okey**.

    ![Caixa de Diálogo Mostrar Modo de Exibição](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. Saudação de atalho **Azure** nó e, em seguida, clique **entrar**.
3. Em Olá **Azure entrar** caixa de diálogo, escolha o método de autenticação hello, clique em **entrar**e insira suas credenciais do Azure.
   
    ![Caixa de diálogo Entrar no Azure](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. Depois que você está conectado, Olá **assinaturas selecione** caixa de diálogo lista todos Olá assinaturas do Azure associadas Olá credenciais. Clique em **selecione** tooclose caixa de diálogo de saudação.

    ![Caixa de diálogo Selecionar Assinaturas](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. Em Olá **Azure Explorer** guia, expanda **HDInsight** toosee Olá clusters HDInsight Spark em sua assinatura.
   
    ![Clusters Spark do HDInsight no Azure Explorer](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. Ainda mais, você pode expandir um nome nó toosee Olá recursos de cluster (por exemplo, contas de armazenamento) associada Olá cluster.
   
    ![Expandindo um recurso de toosee de nome de cluster](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>Configurar um projeto Spark Scala para um cluster HDInsight Spark

1. No espaço de trabalho Olá IDE do Eclipse, clique em **arquivo**, clique em **novo**e, em seguida, clique em **projeto**. 
2. No Assistente de novo projeto hello, expanda **HDInsight**, selecione **Spark no HDInsight (Scala)**e, em seguida, clique em **próximo**.

    ![Selecionando Olá Spark no HDInsight (Scala) de projeto](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. automático de Assistente de criação do Hello Scala projeto detecta se você instalou Scala plug-in ou não. Clique em **Okey** toocontinue baixar o plug-in de Scala hello, em seguida, siga Olá instruções toorestart Eclipse.

    ![verificação do Scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. Em Olá **novo projeto de Scala HDInsight** caixa de diálogo, forneça Olá valores a seguir e, em seguida, clique em **próximo**:
   * Insira um nome para o projeto de saudação.
   * Em Olá **JRE** área, certifique-se de que **usar um ambiente de execução JRE** está definido muito**JavaSE 1.7** ou posterior.
   * Certifique-se de Spark SDK é conjunto toohello local onde você baixou Olá SDK. Olá local de download do link toohello está incluído no hello [pré-requisitos](#prerequisites) anteriormente neste artigo. Você também pode baixar Olá SDK da saudação incluído na caixa de diálogo de saudação do link.

    ![Caixa de diálogo Novo Projeto de Scala HDInsight](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  Na próxima caixa de diálogo hello, clique em Olá **bibliotecas** guia e manter padrões hello e, em seguida, clique em **concluir**. 
   
    ![Guia Bibliotecas](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>Criar um aplicativo Scala para cluster Spark no HDInsight

1. Em Olá IDE do Eclipse, do Explorador de pacotes, expanda o projeto de Olá que você criou anteriormente, com o botão direito **src**, ponto muito**novo**e, em seguida, clique em **outros**.
2. Em Olá **selecionar um assistente** caixa de diálogo caixa, expanda **Scala assistentes**, clique em **objeto Scala**e, em seguida, clique em **próximo**.
   
    ![Selecione uma caixa de diálogo do assistente](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. Em Olá **criar um novo arquivo** caixa de diálogo, digite um nome para o objeto hello e, em seguida, clique em **concluir**.
   
    ![Criar caixa de diálogo Novo Arquivo](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Cole Olá código no editor de texto de saudação a seguir:
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. Execute o aplicativo hello em um cluster do HDInsight Spark:
   
   1. Do Explorador de pacotes, nome do projeto hello e, em seguida, selecione **tooHDInsight enviar Spark aplicativo**.        
   2. Em Olá **envio Spark** caixa de diálogo, forneça Olá valores a seguir e, em seguida, clique em **enviar**:
      
      * Para **nome do Cluster**, selecione o aplicativo de cluster HDInsight Spark no qual você deseja toorun hello.
      * Selecione um artefato do projeto do Eclipse hello, ou selecione um de um disco rígido. valor padrão de saudação depende do item de saudação que você com o botão direito do Explorador de pacotes.
      * Em Olá **nome da classe principal** dropdownlist, envio assistente exibe todos os nomes de objeto do projeto selecionado. Selecione ou insira um que você deseja toorun. Se você selecionar um artefato do disco rígido, você precisará inserir o nome de classe principal sozinho. 
      * Porque o código do aplicativo hello neste exemplo não requer argumentos de linha de comando ou referência JARs ou arquivos, você pode deixar Olá restantes caixas de texto vazias.
        
       ![Caixa de diálogo Envio do Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. Olá **envio Spark** guia deve começar a exibir o progresso de saudação. Você pode parar o aplicativo hello botão Olá vermelho no hello **envio Spark** janela. Você também pode exibir os logs de saudação para esse aplicativo específico execute clicando Olá mundo ícone (indicado por caixa azul de saudação na imagem de saudação).
      
       ![Janela Envio do Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Acessar e gerenciar clusters HDInsight Spark usando as Ferramentas do HDInsight no Kit de Ferramentas do Azure para Eclipse
Você pode executar várias operações usando ferramentas de HDInsight, incluindo o acesso a saída de trabalho hello.

### <a name="access-hello-job-view"></a>Modo de exibição de trabalho do Access Olá
1. No Pesquisador de objetos do Azure, expanda **HDInsight**, expanda o nome do cluster Spark hello e, em seguida, clique em **trabalhos**. 

    ![Nó de exibição de trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Clique em Olá **trabalhos** nó. Ferramentas do HDInsight Olá detecta automaticamente se você instalou o plug-in do hello E (fx) clipse ou não. Clique em **Okey** toocontinue e siga instruções Olá tooinstall Olá Marketplace do Eclipse e reinicie o Eclipse.

    ![Instalar E(fx)clipse](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. Olá abrir modo de exibição do trabalho do hello **trabalhos** nó. No painel direito da saudação, Olá **Spark trabalho exibição** guia exibe todos os aplicativos de saudação que foram executados no cluster de saudação. Clique em nome de saudação do aplicativo hello para o qual você deseja toosee obter mais detalhes.

    ![Detalhes do aplicativo](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. Se você passar o mouse no gráfico de trabalho hello, ele exibe informações básicas de trabalho em execução. Clicando no gráfico de trabalho Olá mostra o gráfico de estágios de saudação e informações que gera todos os trabalhos.

    ![Detalhes do estágio do trabalho](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Logs usados com frequência, incluindo informações do diretório, Driver Stdout e Stderr do Driver estão listados no hello **Log** guia.

    ![Detalhes do log](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. Você também pode abrir Olá histórico Spark da interface do usuário e hello YARN da interface do usuário (em nível de aplicativo hello) clicando em hiperlink respectivos de saudação na parte superior de saudação da janela de saudação.

### <a name="access-hello-storage-container-for-hello-cluster"></a>Contêiner de armazenamento de saudação de acesso para cluster Olá
1. No Pesquisador de objetos do Azure, expanda Olá **HDInsight** toosee de nó raiz uma lista de clusters de HDInsight Spark que estão disponíveis.
2. Expanda conta de armazenamento de Olá Olá cluster nome toosee e contêiner de armazenamento padrão Olá para cluster hello.
   
    ![Contêiner de armazenamento padrão e a conta de armazenamento](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Clique no nome de contêiner de armazenamento Olá associada Olá cluster. No painel direito da saudação, clique duas vezes em Olá **HVACOut** pasta. Abra uma saudação **parte -** arquivos de saída de hello toosee do aplicativo hello.

### <a name="access-hello-spark-history-server"></a>Servidor de histórico do acesso Olá Spark
1. No Azure Explorer, clique com o botão direito do mouse no nome do cluster Spark e escolha **Abrir a Interface do Usuário de Histórico do Spark**. Quando você for solicitado, insira as credenciais de administrador de saudação para cluster hello. Você deve especificar esses durante o provisionamento de cluster hello.
2. No painel de servidor do histórico do Spark hello, você pode usar Olá toolook de nome de aplicativo para o aplicativo hello que você acabou de execução. Em Olá precede o código, você definir nome do aplicativo hello usando `val conf = new SparkConf().setAppName("MyClusterApp")`. Dessa forma, o nome do aplicativo Spark era **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Iniciar o portal do Ambari Olá
1. No Azure Explorer, clique com o botão direito do mouse no nome do cluster Spark e escolha **Abrir o Portal de Gerenciamento do Cluster (Ambari)**. 
2. Quando você for solicitado, insira as credenciais de administrador de saudação para cluster hello. Você deve especificar esses durante o provisionamento de cluster hello.

### <a name="manage-azure-subscriptions"></a>Gerenciar assinaturas do Azure
Por padrão, as ferramentas de HDInsight no Kit de ferramentas do Azure para Eclipse lista clusters do Spark saudação de todas as suas assinaturas do Azure. Se necessário, você pode especificar assinaturas Olá para o qual você deseja que o cluster de saudação tooaccess. 

1. No Pesquisador de objetos do Azure, clique com botão direito Olá **Azure** nó raiz e, em seguida, clique em **gerenciar assinaturas**. 
2. Na caixa de diálogo hello, desmarque caixas de seleção Olá assinatura Olá que você não deseja tooaccess e, em seguida, clique em **fechar**. Você também pode clicar em **sair** se deseja toosign fora de sua assinatura do Azure.

## <a name="run-a-spark-scala-application-locally"></a>Executar um aplicativo Scala Spark localmente
Você pode usar ferramentas do HDInsight no Kit de ferramentas do Azure para Eclipse toorun Spark Scala aplicativos localmente em sua estação de trabalho. Normalmente, esses aplicativos não precisam acessar os recursos toocluster como um contêiner de armazenamento, e você pode executar e testá-las localmente.

### <a name="prerequisite"></a>Pré-requisito
Durante a execução do aplicativo do Olá local Spark Scala em um computador Windows, você pode obter uma exceção, conforme explicado em [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). Essa exceção ocorre porque **WinUtils.exe** está ausente no Windows. 

tooresolve esse erro, você deve [baixar Olá executável](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa local como **C:\WinUtils\bin**. Em seguida, você deve adicionar variável de ambiente Olá **HADOOP_HOME** e defina o valor de saudação da variável de saudação muito**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Executar um aplicativo Scala Spark local
1. Inicie o Eclipse e crie um projeto. Em Olá **novo projeto** caixa de diálogo fazer Olá opções a seguir e, em seguida, clique em **próximo**.
   
   * No painel esquerdo do hello, selecione **HDInsight**.
   * No painel direito da saudação, selecione **Spark no exemplo de execução de HDInsight Local (Scala)**.

    ![Caixa de diálogo Novo Projeto](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. Olá de detalhes do projeto tooprovide hello, siga as etapas de 3 a 6 na seção anterior [configurar um projeto Scala Spark para um cluster HDInsight Spark](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).
3. modelo de saudação adiciona um código de exemplo (**LogQuery**) em Olá **src** pasta pode ser executada localmente no seu computador.
   
    ![Local do LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. Saudação do botão direito do mouse **LogQuery** aplicativo, aponte muito**executar como**e, em seguida, clique em **1 aplicativo Scala**. Você verá uma saída como esta no hello **Console** guia na parte inferior da saudação:
   
   ![Resultado da execução local do Aplicativo Spark](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>Perguntas frequentes
toosubmit um repositório do aplicativo tooAzure Data Lake, escolha **interativo** modo durante o processo de saudação entrada do Azure. Se você selecionar o modo **Automatizado**, obterá um erro.

![interative-signin](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

Isso já está resolvido. Você pode escolher um Cluster do Azure Data Lake toosubmit seu aplicativo com qualquer método de entrada.

## <a name="feedback-and-known-issues"></a>Comentários e problemas conhecidos
Atualmente, não há suporte para exibir saídas do Spark diretamente.

Se você tiver sugestões ou comentários, ou se você encontrar problemas ao usar essa ferramenta, sinta-se livre toosend em um email em hdivstool@microsoft.com.

## <a name="seealso"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Criando e executando aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Use o Kit de ferramentas do Azure para IntelliJ toocreate e enviar Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio de VPN](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Use o Kit de ferramentas do Azure para aplicativos de Spark toodebug IntelliJ remotamente por meio do SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Usar ferramentas do HDInsight para IntelliJ com a área restrita do Hortonworks](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Gerenciando recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

