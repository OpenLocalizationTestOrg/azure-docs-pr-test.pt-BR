---
title: "aaaDebug Apache Spark trabalhos em execução no Azure HDInsight | Microsoft Docs"
description: "Usar YARN da interface do usuário, Spark da interface do usuário e o histórico de Spark servidor tootrack e depuração trabalhos em execução em um cluster Spark no HDInsight do Azure"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Depurar trabalhos do Apache Spark em execução no Azure HDInsight

Neste artigo, você aprenderá como tootrack e depuração despertar trabalhos executados em clusters de HDInsight usando Olá YARN da interface do usuário, Spark da interface do usuário e Olá Spark histórico de servidor. Neste artigo, vamos começar um trabalho do Spark usando um bloco de anotações disponível com o cluster do Spark hello, **aprendizado de máquina: análise de previsão em dados de inspeção de alimentos com MLLib**. Você pode usar etapas Olá abaixo tootrack um aplicativo que é enviado usando qualquer outra abordagem, por exemplo, **o envio spark**.

## <a name="prerequisites"></a>Pré-requisitos
Você deve ter o seguinte hello:

* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Você deve ter começou a executar notebook Olá,  **[aprendizado de máquina: análise de previsão em dados de inspeção de alimentos com MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**. Para obter instruções sobre como toorun este bloco de anotações, siga Olá link.  

## <a name="track-an-application-in-hello-yarn-ui"></a>Controlar um aplicativo hello YARN da interface do usuário
1. Inicie Olá YARN da interface do usuário. Na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **YARN**.
   
    ![Iniciar Interface do usuário do YARN](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > Como alternativa, você também pode iniciar Olá YARN da interface do usuário do hello Ambari UI. Olá toolaunch Ambari UI, na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **painel do Cluster HDInsight**. De Olá Ambari UI, clique em **YARN**, clique em **Links rápidos**, clique em Gerenciador de recursos ativo hello e, em seguida, clique em **ResourceManager UI**.    
   > 
   > 
2. Como você iniciou o trabalho do Spark hello usando blocos de anotações do Jupyter, o aplicativo hello tem nome hello **remotesparkmagics** (Este é o nome de Olá para todos os aplicativos que são iniciadas de blocos de anotações de saudação). Clique em ID do aplicativo hello contra Olá tooget de nome de aplicativo para obter mais informações sobre o trabalho de saudação. Isso inicia o modo de exibição de aplicativo hello.
   
    ![Localizar a ID de aplicativo Spark](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Para aplicativos que são iniciados a partir de blocos de anotações do Jupyter hello, status de saudação é sempre **executando** até que você sair do bloco de anotações de saudação.
3. Exibição do aplicativo hello, você pode fazer drill down mais toofind out contêineres Olá associados ao aplicativo hello e logs de saudação (stdout/stderr). Você também pode iniciar Olá Spark da interface do usuário clicando Olá vinculação correspondente toohello **controle URL**, conforme mostrado abaixo. 
   
    ![Baixar logs de contêiner](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>Controlar um aplicativo hello Spark da interface do usuário
Olá Spark da interface do usuário, você pode detalhar em trabalhos de Spark Olá que são gerados pelo aplicativo hello que tiver iniciado anteriormente.

1. Olá toolaunch Spark da interface do usuário, de modo de exibição de aplicativo hello, clique em link Olá contra Olá **controle URL**, conforme mostrado na captura de tela de saudação acima. Você pode ver todos os trabalhos do Spark Olá iniciados pelo aplicativo hello em execução em anotações do Jupyter hello.
   
    ![Exibir trabalhos do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Clique em Olá **executores** guia toosee informações de processamento e armazenamento para cada executor. Você também pode recuperar a pilha de chamadas Olá clicando em Olá **Thread despejo** link.
   
    ![Exibir executores do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Clique em Olá **estágios** guia toosee estágios de saudação associados ao aplicativo hello.
   
    ![Exibir estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    Cada estágio pode ter várias tarefas para as quais você pode exibir estatísticas de execução, como mostrado abaixo.
   
    ![Exibir estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. Na página de detalhes do estágio hello, você pode iniciar DAG visualização. Expanda Olá **DAG visualização** link na parte superior de saudação da página hello, conforme mostrado abaixo.
   
    ![Exibir a visualização de DAG dos estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    Gráfico de Aclyic direta ou DAG representa diferentes estágios Olá no aplicativo hello. Cada caixa azul no gráfico de saudação representa uma operação de Spark chamada a partir de aplicativo hello.
5. Na página de detalhes do hello estágio, você também pode iniciar o modo de exibição de tempo de aplicativo hello. Expanda Olá **cronograma do evento** link na parte superior de saudação da página hello, conforme mostrado abaixo.
   
    ![Exibir linha do tempo de evento de estágios do Spark](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Exibe eventos de Spark Olá na forma de saudação de uma linha do tempo. modo de exibição de tempo de saudação está disponível em três níveis, em trabalhos, dentro de um trabalho e em um estágio. imagem de saudação acima captura o modo de exibição de tempo de saudação para uma determinada fase.
   
   > [!TIP]
   > Se você selecionar Olá **habilitar o zoom** caixa de seleção, você pode rolar para a esquerda e direita em modo de exibição de tempo de saudação.
   > 
   > 
6. Outras guias Olá Spark da interface do usuário fornecem informações úteis sobre a instância do Spark Olá também.
   
   * Guia de armazenamento - se seu aplicativo cria um RDDs, você encontrará informações sobre os na guia de armazenamento de saudação.
   * Guia de ambiente - este guia fornece muitas informações úteis sobre sua instância do Spark como Olá 
     * Versão da escala
     * Diretório de log de eventos associado a saudação cluster
     * Número de núcleos de executor de aplicativo hello
     * Etc.

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>Para obter informações sobre trabalhos concluídos usando Olá Spark histórico de servidor
Quando um trabalho for concluído, informações de saudação sobre o trabalho de saudação são mantidas no hello Spark histórico de servidor.

1. Olá toolaunch Spark histórico de servidor, na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **Spark histórico servidor**.
   
    ![Iniciar o Servidor de Histórico do Spark](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > Como alternativa, você também pode iniciar Olá Spark histórico servidor UI do hello Ambari UI. Olá toolaunch Ambari UI, na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **painel do Cluster HDInsight**. De Olá Ambari UI, clique em **Spark**, clique em **Links rápidos**e, em seguida, clique em **Spark histórico servidor UI**.
   > 
   > 
2. Você verá todos os aplicativos de saudação concluída listados. Clique em um toodrill de ID do aplicativo para baixo em um aplicativo para obter mais informações.
   
    ![Iniciar o Servidor de Histórico do Spark](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>Consulte também
*  [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>Para analistas de dados

* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Análise da telemetria de dados do Application Insight usando o Spark no HDInsight](hdinsight-spark-analyze-application-insight-logs.md)
* [Usar o Caffe no Azure HDInsight Spark para aprendizado aprofundado distribuído](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Para desenvolvedores do Spark

* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


