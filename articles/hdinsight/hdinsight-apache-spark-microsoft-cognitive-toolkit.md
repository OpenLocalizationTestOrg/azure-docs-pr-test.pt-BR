---
title: aaaMicrosoft cognitivas Toolkit com Spark no HDInsight para aprendizado | Microsoft Docs
description: "Saiba como um treinado Microsoft cognitivas Toolkit profunda modelo de aprendizado pode ser o conjunto de dados de tooa aplicada usando Olá Spark Python API em um cluster Spark no HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Use o modelo de aprendizado profundo treinado das Ferramentas Cognitivas da Microsoft com o cluster do Azure HDInsight Spark

Neste artigo, você Olá seguintes etapas.

1. Execute um script personalizado de tooinstall cognitivas Kit de ferramentas do Microsoft em um cluster do Spark no HDInsight.

2. Carregar um Jupyter notebook toohello Spark cluster toosee como tooapply um treinado Microsoft cognitivas Toolkit profunda aprendizado toofiles de modelo em uma conta de armazenamento de Blob do Azure usando Olá [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**. Antes de começar este tutorial, você deverá ter uma assinatura do Azure. Consulte [Criar sua conta gratuita do Azure hoje](https://azure.microsoft.com/free).

* **Cluster do Azure HDInsight Spark**. Para este artigo, crie um cluster Spark 2.0. Para obter instruções, consulte [Criar um cluster do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-does-this-solution-flow"></a>Como é o fluxo dessa solução?

Essa solução é dividida entre este artigo e um Notebook Jupyter que é carregado como parte deste tutorial. Neste artigo, você deve concluir Olá etapas a seguir:

* Execute uma ação de script em um cluster do HDInsight Spark tooinstall Microsoft cognitivas Toolkit e Python pacotes.
* Carregamento de anotações do Jupyter Olá executado Olá solução toohello cluster HDInsight Spark.

Olá seguir etapas restantes são abordadas em anotações do Jupyter hello.

- Carregar imagens de exemplo em um Conjunto de dados distribuído resiliente, ou RDD, do Spark
   - Carregar módulos e definir predefinições
   - Baixar o dataset Olá localmente no cluster do Spark Olá
   - Converter o conjunto de dados de saudação em um RDD
- Imagens de saudação de pontuação usando um kit de ferramentas cognitivas treinado
   - Baixar Olá treinado Toolkit cognitivas modelo toohello Spark cluster
   - Definir funções toobe usada por nós de trabalho
   - Imagens de pontuação Olá em nós de trabalho
   - Avaliar a precisão do modelo


## <a name="install-microsoft-cognitive-toolkit"></a>Instalar o Kit de Ferramentas Cognitivas da Microsoft

Você pode instalar o Kit de Ferramentas Cognitivas da Microsoft em um cluster do Spark usando ação de script. Ação de script usa componentes de tooinstall scripts personalizados no cluster Olá que não estão disponíveis por padrão. Você pode usar o script personalizado de saudação do hello Portal do Azure, usando o SDK do HDInsight .NET ou usando o PowerShell do Azure. Você também pode usar o Kit de ferramentas do hello script tooinstall hello ou como parte da criação do cluster, ou depois que o cluster hello está em execução. 

Neste artigo, usamos Olá tooinstall portal Olá toolkit, depois Olá cluster foi criado. Para outro maneiras toorun Olá script personalizado, consulte [HDInsight personalizar clusters usando a ação de Script](hdinsight-hadoop-customize-cluster-linux.md).

### <a name="using-hello-azure-portal"></a>Usando Olá Portal do Azure

Para obter instruções sobre como toouse hello Azure Portal toorun scripts de ação, consulte [HDInsight personalizar clusters usando a ação de Script](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation). Certifique-se de que fornecer Olá entradas tooinstall cognitivas Kit de ferramentas da Microsoft a seguir.

* Forneça um valor para o nome de ação de script hello.

* Para uma **URI do script Bash**, insira `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.

* Verifique se você executar script hello apenas em Olá nós de cabeçalho e de trabalho e desmarque todas Olá outras caixas de seleção.

* Clique em **Criar**.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Carregar tooAzure de notebook Jupyter de saudação cluster HDInsight Spark

Olá toouse Microsoft cognitivas Toolkit com cluster do Azure HDInsight Spark hello, você deve carregar anotações do Jupyter Olá **CNTK_model_scoring_on_Spark_walkthrough.ipynb** cluster do Spark no HDInsight toohello. Esse bloco de anotações está disponível no GitHub em [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).

1. Repositório do GitHub Olá clone [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration). Para obter instruções tooclone, consulte [clonando um repositório](https://help.github.com/articles/cloning-a-repository/).

2. Em Olá Portal do Azure, abra a folha de cluster do Spark Olá já provisionada, clique **painel Cluster**e, em seguida, clique em **notebook Jupyter**.

    Você também pode iniciar de anotações do Jupyter Olá indo URL toohello `https://<clustername>.azurehdinsight.net/jupyter/`. Substituir \<clustername > pelo nome de saudação do seu cluster HDInsight.

3. De anotações do Jupyter hello, clique em **carregar** em Olá canto superior direito e navegue toohello local em que você clonou repositório do GitHub hello.

    ![Carregar tooAzure de notebook Jupyter cluster HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "tooAzure de notebook Jupyter carregar cluster HDInsight Spark")

4. Clique em **Carregar** novamente.

5. Depois notebook Olá é carregado, clique em nome de saudação do bloco de anotações de saudação e siga as instruções de Olá no bloco de anotações de saudação em si no como tooload Olá conjunto de dados e executar o tutorial hello.

## <a name="see-also"></a>Consulte também
* [Visão geral: Apache Spark no Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Cenários
* [Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI](hdinsight-apache-spark-use-bi-tools.md)
* [Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real](hdinsight-apache-spark-eventhub-streaming.md)
* [Análise de log do site usando o Spark no HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Análise da telemetria de dados do Application Insight usando o Spark no HDInsight](hdinsight-spark-analyze-application-insight-logs.md)

### <a name="create-and-run-applications"></a>Criar e executar aplicativos
* [Criar um aplicativo autônomo usando Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Executar trabalhos remotamente em um cluster do Spark usando Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Ferramentas e extensões
* [Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar Spark Scala aplicativos](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
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
