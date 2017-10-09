---
title: "ação de aaaScript - pacotes do Python instalar com Jupyter no Azure HDInsight | Microsoft Docs"
description: "Instruções passo a passo sobre como toouse script ação tooconfigure Jupyter notebooks disponíveis com o HDInsight Spark clusters toouse pacotes de python externo."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Usar pacotes de Python ação de Script tooinstall externos para blocos de anotações do Jupyter em clusters Apache Spark no HDInsight
> [!div class="op_single_selector"]
> * [Usando a mágica da célula](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Usando a ação de script](hdinsight-apache-spark-python-package-installation.md)
>
>

Saiba como toouse ações de Script tooconfigure um cluster do Apache Spark no HDInsight (Linux) toouse externo, contribuído pela comunidade **python** pacotes que não são incluídas de caixa Olá cluster.

> [!NOTE]
> Você também pode configurar um bloco de anotações do Jupyter usando `%%configure` magic pacotes externos toouse. Para obter instruções, confira [Usar pacotes externos com notebooks Jupyter em clusters do Apache Spark no HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

Você pode pesquisar Olá [índice pacote](https://pypi.python.org/pypi) para a lista completa de saudação dos pacotes que estão disponíveis. Você também pode obter uma lista de pacotes disponíveis de outras fontes. Por exemplo, você pode instalar pacotes disponibilizados por meio de [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) ou [conda-forge](https://conda-forge.github.io/feedstocks.html).

Neste artigo, você aprenderá como Olá tooinstall [TensorFlow](https://www.tensorflow.org/) pacote usando o Script Actoin no cluster e usá-lo por meio de anotações do Jupyter hello.

## <a name="prerequisites"></a>Pré-requisitos
Você deve ter o seguinte hello:

* Uma assinatura do Azure. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Um cluster do Apache Spark no HDInsight. Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Se você ainda não tiver um cluster Spark no HDInsight Linux, poderá executar ações de script durante a criação do cluster. Visite documentação Olá no [como ações de script personalizado toouse](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Usar pacotes externos com blocos de notas Jupyter

1. De saudação [Portal do Azure](https://portal.azure.com/), do quadro de saudação inicial, clique em bloco de saudação para seu cluster Spark (se tê-fixado quadro toohello inicial). Você também pode navegar cluster tooyour em **procurar todos os** > **Clusters HDInsight**.   

2. Na folha de cluster do Spark hello, clique em **ações de Script** em **uso**. Execute a ação personalizada de saudação que instala TensorFlow em nós de cabeçalho hello e nós de trabalho hello. scripts de bash Olá podem ser referenciado de: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh visita Olá documentação [como ações de script personalizado toouse](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Há dois python instalações em cluster hello. Spark usará a instalação de python Anaconda Olá localizada em `/usr/bin/anaconda/bin`. Faça referência a essa instalação em suas ações personalizadas por meio de `/usr/bin/anaconda/bin/pip` e `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Abrir um PySpark Jupyter Notebook

    ![Criar um novo bloco de anotações do Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Criar um novo bloco de anotações do Jupyter")

4. Um novo bloco de anotações é criado e aberto com o nome hello Untitled.pynb. Clique em nome do bloco de anotações de saudação na parte superior da saudação e insira um nome amigável.

    ![Forneça um nome para o bloco de anotações de saudação](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "forneça um nome para o bloco de anotações de saudação")

5. Agora, você fará `import tensorflow` e executará um exemplo de hello world. 

    Toocopy de código:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    resultado de saudação será assim:
    
    ![Execução de código TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Executar código TensorFlow")



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
* [Usar pacotes externos com notebooks Jupyter em clusters Apache Spark no HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)
