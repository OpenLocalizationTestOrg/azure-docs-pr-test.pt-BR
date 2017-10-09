---
title: cluster de aaaTroubleshoot problemas com o Apache Spark no HDInsight do Azure | Microsoft Docs
description: Saiba mais sobre problemas relacionados tooApache clusters de Spark no HDInsight do Azure e como toowork em torno das.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Problemas conhecidos do cluster do Apache Spark no HDInsight

Este documento controla de saudação todos os problemas de saudação visualização pública do HDInsight Spark.  

## <a name="livy-leaks-interactive-session"></a>Sessão interativa de vazamentos do Livy
Quando Livy for reiniciado (do Ambari ou devido a reinicialização da máquina virtual de tooheadnode 0) com uma sessão interativa ainda existe, uma sessão interativa do trabalho será perdida. Por isso, pode novo de trabalhos presa no hello estado aceito e não pode ser iniciado.

**Atenuação:**

Use Olá problema de saudação tooworkaround procedimento a seguir:

1. SSH no nó principal. Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Olá execução após o aplicativo do comando toofind hello IDs dos trabalhos interativo Olá iniciada por Livy. 
   
        yarn application –list
   
    Olá nomes de trabalho padrão será Livy se trabalhos de saudação foram iniciados com uma sessão interativa Livy sem nenhum nome explícito especificado por Olá sessão Livy iniciado por notebook Jupyter, o nome do trabalho Olá iniciará com remotesparkmagics_ *. 
3. Execute Olá tookill de comando a seguir esses trabalhos. 
   
        yarn application –kill <Application ID>

A execução de novos trabalhos terá início. 

## <a name="spark-history-server-not-started"></a>Servidor de histórico Spark não iniciado
O servidor de histórico Spark não é iniciado automaticamente depois de um cluster ser criado.  

**Atenuação:** 

Inicie manualmente o servidor de histórico de saudação do Ambari.

## <a name="permission-issue-in-spark-log-directory"></a>Problema de permissão no diretório de log do Spark
Quando hdiuser enviar um trabalho com spark-submit, há um erro java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (permissão negada) e hello log de driver não será gravado. 

**Atenuação:**

1. Adicione grupo de Hadoop toohello hdiuser. 
2. Forneça 777 permissões em /var/log/spark após a criação do cluster. 
3. Atualize Olá spark log local usando o Ambari toobe um diretório com 777 permissões.  
4. Execute spark-submit como sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Não há suporte para o conector Spark Phoenix

Atualmente, Olá Spark Phoenix conector não tem suporte com um cluster HDInsight Spark.

**Atenuação:**

Você deve usar o conector do HBase Spark hello. Para obter instruções, consulte [como conector toouse Spark HBase](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-toojupyter-notebooks"></a>Problemas relacionados tooJupyter notebooks
A seguir estão alguns problemas conhecidos relacionados tooJupyter blocos de anotações.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Notebooks com caracteres não ASCII nos nomes de arquivos
Os notebooks do Jupyter que podem ser usados em clusters HDInsight do Spark não devem ter caracteres não ASCII nos nomes de arquivos. Se você tentar tooupload um arquivo por meio de saudação UI Jupyter que tem um nome de arquivo não-ASCII, ele falhará em modo silencioso (ou seja, Jupyter não permite que você carregar o arquivo hello, mas ela não gerar um erro visível ou). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Erro ao carregar notebooks de tamanhos maiores
Você pode encontrar um erro **`Error loading notebook`** ao carregar notebooks com um tamanho maior.  

**Atenuação:**

Se você visualizar esse erro, não significa que seus dados estão corrompidos ou foram perdidos.  Os blocos de anotações ainda estão no disco no `/var/lib/jupyter`, e poderá SSH para Olá cluster tooaccess-los. Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Depois de conectar o cluster toohello usando SSH, você pode copiar seus blocos de anotações do cluster tooyour computador local (usando o SCP ou WinSCP) como uma perda de saudação tooprevent backup de quaisquer dados importantes no bloco de anotações de saudação. Você pode, em seguida, túnel SSH no seu nó principal na porta 8001 tooaccess Jupyter sem passar pelo gateway hello.  A partir daí, você pode limpar a saída de saudação do bloco de notas e salvá-lo novamente tamanho toominimize saudação do bloco de anotações.

tooprevent esse erro ocorra em Olá futura, você deve seguir algumas práticas recomendadas:

* É tookeep importante pequenos de tamanho de bloco de anotações de hello. Todas as saídas de seus trabalhos Spark que é enviada de volta tooJupyter é mantido no bloco de anotações de saudação.  É uma prática recomendada Jupyter geral tooavoid executando `.collect()` em RDD grandes ou quadros de dados; em vez disso, se você quiser toopeek no conteúdo de um RDD, considere executar `.take()` ou `.sample()` para que a saída não fica muito grande.
* Além disso, quando você salva um bloco de anotações, desmarque todas as saída tamanho de saudação tooreduce células.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>A inicialização inicial do notebook demora mais do que o esperado
A primeira instrução de código no notebook Jupyter usando a mágica do Spark pode demorar mais de um minuto.  

**Explicação:**

Isso ocorre porque quando a primeira célula de código Olá é executada. No plano de fundo Olá Isso inicia a configuração de sessão e Spark, SQL e contextos de Hive são definidos. Após configurar nesses contextos, Olá primeira instrução é executada e isso oferece impressão Olá instrução Olá levou toocomplete um longo tempo.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>Tempo limite de notebook Jupyter na criação de sessão Olá
Quando o cluster Spark está sem recursos, hello Spark e kernels Pyspark em anotações do Jupyter Olá atingirá o tempo limite tentar toocreate sessão de saudação. 

**Atenuações:** 

1. Libere alguns recursos do cluster Spark:
   
   * Parar outros blocos de anotações do Spark toohello vai fechar e menu de parada ou clicando desligamento no explorer de notebook hello.
   * Interrompendo outros aplicativos Spark do YARN.
2. Reinicie o notebook Olá que estivesse tentando toostart backup. Há recursos suficientes devem estar disponíveis para você toocreate agora uma sessão.

## <a name="see-also"></a>Consulte também
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
* [Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Usar pacotes externos com blocos de notas Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Gerenciar recursos
* [Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure](hdinsight-apache-spark-resource-manager.md)
* [Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight](hdinsight-apache-spark-job-debugging.md)

