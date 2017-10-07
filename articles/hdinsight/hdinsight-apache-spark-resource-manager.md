---
title: cluster de aaaManage recursos para o Apache Spark no HDInsight do Azure | Microsoft Docs
description: Saiba como toouse gerenciar os recursos de clusters Spark no Azure HDInsight para melhorar o desempenho.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Gerenciar os recursos para o cluster do Apache Spark no Azure HDInsight 

Neste artigo, você aprenderá como interfaces de saudação tooaccess como Ambari UI, YARN da interface do usuário e Olá Spark histórico servidor associado ao seu cluster Spark. Você também aprenderá como tootune Olá configuração de cluster para o desempenho ideal.

**Pré-requisitos:**

Você deve ter o seguinte hello:

* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>Como iniciar o hello da interface do usuário do Ambari Web?
1. De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial). Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.
2. Na folha de cluster do Spark hello, clique em **painel**. Quando solicitado, insira as credenciais de administrador Olá para o cluster do Spark hello.

    ![Inicie o Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "iniciar o Gerenciador de recursos")
3. Isso deve abrir Olá Ambari Web da interface do usuário, conforme mostrado abaixo.

    ![Interface da Web Ambari](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web da interface do usuário")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>Como iniciar o hello Spark histórico servidor?
1. De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial).
2. De saudação do cluster folha, em **Links rápidos**, clique em **painel Cluster**. Em Olá **painel Cluster** folha, clique em **Spark histórico servidor**.

    ![Spark History Server](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark History Server")

    Quando solicitado, insira as credenciais de administrador Olá para o cluster do Spark hello.

## <a name="how-do-i-launch-hello-yarn-ui"></a>Como iniciar o hello Yarn da interface do usuário?
Você pode usar o hello YARN UI toomonitor os aplicativos que estão sendo executados no cluster do Spark hello.

1. Na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **YARN**.

    ![Iniciar Interface do usuário do YARN](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > Como alternativa, você também pode iniciar Olá YARN da interface do usuário do hello Ambari UI. Olá toolaunch Ambari UI, na folha de cluster hello, clique em **painel Cluster**e, em seguida, clique em **painel do Cluster HDInsight**. De Olá Ambari UI, clique em **YARN**, clique em **Links rápidos**, clique em Gerenciador de recursos ativo hello e, em seguida, clique em **ResourceManager UI**.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>O que é Olá ideal configuração toorun Spark de aplicativos de cluster?
Olá três parâmetros de chave que podem ser usados para a configuração do Spark dependendo dos requisitos de aplicativo são `spark.executor.instances`, `spark.executor.cores`, e `spark.executor.memory`. Um Executor é um processo iniciado por um aplicativo Spark. Ele é executado no nó do operador hello e é responsável toocarry tarefas Olá para o aplicativo hello. número padrão de saudação de executores e tamanhos de executor de saudação para cada cluster é calculado com base no número de saudação de nós de trabalho e tamanho de nó do operador de saudação. Eles são armazenados no `spark-defaults.conf` em nós de cluster de Olá cabeçalho.

três parâmetros de configuração Olá podem ser configurados no nível do cluster hello (para todos os aplicativos executados no cluster Olá) ou podem ser especificados para cada aplicativo individual também.

### <a name="change-hello-parameters-using-ambari-ui"></a>Alterar os parâmetros de saudação usando Ambari UI
1. De saudação Ambari UI clique **Spark**, clique em **configurações**e, em seguida, expanda **padrões spark personalizado**.

    ![Definir parâmetros usando o Ambari](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. valores padrão de saudação são aplicativos de Spark de BOM toohave 4 executados simultaneamente em cluster hello. Você pode alterações esses valores da interface do usuário hello, conforme mostrado abaixo.

    ![Definir parâmetros usando o Ambari](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Clique em **salvar** toosave alterações de configuração de saudação. Na parte superior de saudação da página hello, você será solicitado toorestart todos Olá afetados serviços. Clique em **Reiniciar**.

    ![Reiniciar serviços](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Alterar os parâmetros de saudação para um aplicativo em execução no bloco de anotações do Jupyter
Para aplicativos executados em anotações do Jupyter hello, você pode usar o hello `%%configure` magic toomake alterações de configuração de saudação. Idealmente, você deve fazer essas alterações no início de saudação do aplicativo hello, antes de executar a primeira célula de código. Isso garante que a configuração hello está aplicada toohello Livy sessão, quando ele é criado. Se desejar que a configuração de saudação toochange em um estágio posterior no aplicativo hello, você deve usar o hello `-f` parâmetro. No entanto, ao fazer isso, todos de progresso em hello aplicativo serão perdido.

trecho de saudação abaixo mostra como toochange Olá a configuração de um aplicativo em execução no Jupyter.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

Parâmetros de configuração devem ser passados como uma cadeia de caracteres JSON e devem estar na próxima linha de saudação após magic Olá, conforme mostrado na coluna de exemplo hello.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>Alterar Olá parâmetros para um aplicativo enviada usando o envio spark
Comando a seguir está um exemplo de como toochange Olá parâmetros de configuração para um aplicativo de lote que é enviado usando `spark-submit`.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>Alterar os parâmetros de saudação para um aplicativo enviado usando ondulação
Comando a seguir é um exemplo de como toochange Olá parâmetros de configuração para um aplicativo de lote que é enviado usando a rotação.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Como altero esses parâmetros em um Servidor Thrift Spark?
Spark Thrift Server fornece cluster Spark do JDBC/ODBC acesso tooa e é usado tooservice consultas Spark SQL. Ferramentas como Power BI, Tableau, etc. Use ODBC protocolo toocommunicate com consultas do servidor do Spark Thrift tooexecute Spark SQL como um aplicativo do Spark. Quando um cluster Spark é criado, duas instâncias do hello Spark Thrift Server forem iniciados, uma em cada nó de cabeçalho. Cada servidor do Spark Thrift está visível como um aplicativo Spark Olá YARN da interface do usuário.

Spark Thrift Server usa despertar alocação dinâmica de executor e, portanto, Olá `spark.executor.instances` não é usado. Em vez disso, usa o servidor do Spark Thrift `spark.dynamicAllocation.minExecutors` e `spark.dynamicAllocation.maxExecutors` toospecify contagem de executor de saudação. parâmetros de configuração de Olá `spark.executor.cores` e `spark.executor.memory` é toomodify Olá executor tamanho usado. É possível alterar esses parâmetros, conforme mostrado abaixo.

* Expanda Olá **avançado spark-thrift-sparkconf** parâmetros de saudação do categoria tooupdate `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, e `spark.executor.memory`.

    ![Configurar o servidor Thrift Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Expanda Olá **personalizado spark thrift sparkconf** parâmetro hello da categoria tooupdate `spark.executor.cores`.

    ![Configurar o servidor Thrift Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>Como alterar a memória de driver de saudação do hello Spark Thrift servidor?
Memória do servidor do Spark Thrift driver é configurado too25% do tamanho do nó principal RAM hello, desde que o tamanho total de RAM saudação do nó principal Olá é maior do que 14GB. Você pode usar o hello configuração de memória do driver Ambari UI toochange hello, conforme mostrado abaixo.

* De saudação Ambari UI, clique em **Spark**, clique em **configurações**, expanda **avançado spark env**e, em seguida, forneça o valor de saudação para **spark_thrift_cmd_opts**.

    ![Configurar a RAM do servidor Thrift Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>Não uso o BI com cluster Spark. Como obter os recursos de saudação novamente?
Uma vez que usamos alocação dinâmica Spark, hello somente os recursos consumidos pelo servidor thrift são Olá recursos para dois mestres de aplicativo hello. tooreclaim esses recursos, que você deve interromper Olá serviços Thrift Server em execução no cluster de saudação.

1. De saudação Ambari UI, no painel esquerdo do hello, clique em **Spark**.
2. Na página seguinte do hello, clique em **Spark Thrift servidores**.

    ![Reiniciar o servidor Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Você deve ver Olá dois headnodes no qual Olá Spark Thrift Server está em execução. Clique em uma saudação headnodes.

    ![Reiniciar o servidor Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. próxima página de saudação lista todos os serviços de saudação em execução em que um nó principal. Na lista de saudação clique tooSpark próximo do botão suspenso de saudação Thrift servidor e, em seguida, clique em **parar**.

    ![Reiniciar o servidor Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Repita essas etapas em Olá também outros um nó principal.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>Meus blocos de anotações do Jupyter não estão sendo executados conforme esperado. Como reiniciar o serviço Olá?
Inicie a saudação da interface do usuário do Ambari Web como mostrado acima. Olá à esquerda no painel de navegação, clique em **Jupyter**, clique em **ações de serviço**e, em seguida, clique em **reiniciar todos os**. Isso iniciará o serviço de Jupyter de saudação em todos os headnodes de saudação.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>Como fazer para saber se estou ficando sem recursos?
Inicie Olá Yarn da interface do usuário, como mostrado acima. Na tabela de métricas de Cluster na parte superior da tela hello, verifique os valores de **memória usada** e **memória Total** colunas. Se os valores hello 2 são muito próximos, pode não haver próximo aplicativo suficiente recursos toostart hello. Olá mesmo se aplica a toohello **VCores usado** e **VCores Total** colunas. Além disso, no modo de exibição principal hello, se houver um aplicativo continuaram em **aceito** estado e não a transição para **executando** nem **falha** estado, isso também pode ser uma indicação Se não estiver recebendo suficiente toostart de recursos.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>Como interromper a execução toofree aplicativo recurso?
1. No hello Yarn da interface do usuário, no painel esquerdo do hello, clique em **executando**. Na lista de saudação de aplicativos em execução, determinar Olá aplicativo toobe interrompida e clique em Olá **ID**.

    ![Eliminar App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Eliminar App1")

2. Clique em **aplicativo Kill** na Olá canto superior direito, em seguida, clique em **Okey**.

    ![Eliminar App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Eliminar App2")

## <a name="see-also"></a>Consulte também
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

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
