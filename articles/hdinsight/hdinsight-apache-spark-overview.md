---
title: tooSpark aaaIntroduction no Azure HDInsight | Microsoft Docs
description: "Este artigo fornece uma introdução tooSpark em HDInsight e hello cenários diferentes nos quais você pode usar o cluster Spark no HDInsight."
keywords: "o que é spark apache, cluster spark, toospark de Introdução, spark no hdinsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>Introdução tooSpark no HDInsight

Este artigo fornece uma tooSpark de Introdução no HDInsight. <a href="http://spark.apache.org/" target="_blank">Apache Spark</a> é uma estrutura de processamento paralelo do código-fonte aberto que dá suporte à memória no desempenho do processamento tooboost Olá de aplicativos analíticos grandes de dados. O cluster do Spark no HDInsight é compatível com o WASB (Armazenamento do Azure) e com o Azure Data Lake Store e, portanto, seus dados existentes armazenados no Azure poderão ser processados facilmente por meio de um cluster do Spark.

Quando você cria um cluster do Spark no HDInsight, cria recursos de computação do Azure com o Spark instalado e configurado. Leva apenas cerca de dez minutos cluster toocreate um Spark no HDInsight. Olá toobe de dados processado é armazenado no armazenamento do Azure ou do repositório Azure Data Lake. Veja [Usar o Armazenamento do Azure com HDInsight](hdinsight-hadoop-use-blob-storage.md).

**cluster toocreate um Spark no HDInsight**, consulte [início rápido: criar um cluster Spark no HDInsight e execute a consulta interativa usando Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>O que é o Apache Spark no Azure HDInsight?
Os clusters do Spark oferecem um serviço Spark totalmente gerenciado. Os benefícios da criação de um cluster do Spark no HDInsight estão listados aqui.

| Recurso | Descrição |
| --- | --- |
| Facilidade de criação de clusters do Spark |Você pode criar um novo cluster Spark no HDInsight em minutos usando Olá Portal do Azure, Azure PowerShell ou Olá HDInsight .NET SDK. Confira [Introdução ao cluster do Spark no HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) |
| Fácil de uso |O cluster do Spark no HDInsight inclui blocos de anotações do Jupyter e do Zeppelin. Você pode usá-los para processar e visualizar dados interativamente.|
| APIs REST |Incluem clusters Spark no HDInsight [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server), um Spark com base em REST API trabalho server tooremotely enviar e monitorar trabalhos. |
| Suporte ao Repositório Azure Data Lake | Cluster Spark no HDInsight pode ser configurado toouse repositório Azure Data Lake como um armazenamento adicional, bem como armazenamento primário (apenas com clusters de HDInsight 3.5). Para saber mais sobre o Repositório Data Lake, veja [Visão geral do Repositório Azure Data Lake](../data-lake-store/data-lake-store-overview.md). |
| Integração com serviços do Azure |Cluster Spark no HDInsight vem com um conector tooAzure Hubs de eventos. Os clientes podem criar aplicativos de streaming usando Hubs de eventos hello, muito além disso[Kafka](http://kafka.apache.org/), que já está disponível como parte do Spark. |
| Suporte para Servidor R | Você pode configurar um servidor de R no HDInsight Spark toorun cluster distribuído cálculos de R com velocidades Olá prometidas com um cluster Spark. Para saber mais, veja [Introdução ao uso do Servidor R no HDInsight](hdinsight-hadoop-r-server-get-started.md). |
| Integração com IDEs de terceiros | HDInsight fornece plug-ins para IDEs como IntelliJ IDEIA e Eclipse, você pode usar toocreate e enviar aplicativos tooan cluster HDInsight Spark. Para saber mais, confira [Usar kit de ferramentas do uso do Azure para IntelliJ IDEA](hdinsight-apache-spark-intellij-tool-plugin.md) e [Usar kit de ferramentas do Azure para Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md).|
| Consultas simultâneas |Os clusters do Spark no HDInsight dão suporte a consultas simultâneas. Isso permite que várias consultas de usuário de uma ou várias consultas de vários usuários e aplicativos tooshare Olá os mesmos recursos de cluster. |
| Armazenamento em cache no SSDs |Você pode escolher o toocache dados na memória ou no SSDs anexado toohello nós de cluster. Cache na memória oferece melhor desempenho de consulta hello, mas pode ser caro; o cache no SSDs fornece uma ótima opção para melhorar o desempenho de consulta sem a necessidade de saudação toocreate um cluster de um tamanho que seja necessário toofit Olá todo conjunto de dados na memória. |
| Integração com ferramentas de BI |Os clusters do Spark no  HDInsight fornecem conectores para ferramentas de BI como o [Power BI](http://www.powerbi.com/) e o [Tableau](http://www.tableau.com/products/desktop), para análise de dados. |
| Bibliotecas Anaconda pré-carregadas |Os clusters do Spark no HDInsight são fornecidos com bibliotecas Anaconda pré-instaladas. [Anaconda](http://docs.continuum.io/anaconda/) fornece bibliotecas too200 Fechar para aprendizado de máquina, análise de dados, visualização, etc. |
| Escalabilidade |Embora você possa especificar o número de saudação de nós em seu cluster durante a criação, você pode desejar toogrow ou reduzir a carga de trabalho do hello cluster toomatch. Todos os clusters de HDInsight permitem toochange número de saudação de nós no cluster de saudação. Além disso, os clusters Spark podem ser descartados sem perda de dados desde que todos os dados de saudação são armazenados no armazenamento do Azure ou repositório Data Lake. |
| Suporte contínuo |Os clusters do Spark no HDInsight vêm com suporte de nível empresarial 24 horas por dia, 7 dias por semana, e um SLA de 99,9% de tempo de atividade. |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>Quais são os casos de uso de saudação para Spark no HDInsight?
Clusters Spark no HDInsight habilitar Olá cenários principais a seguir.

### <a name="interactive-data-analysis-and-bi"></a>Análise de dados interativa e BI
[Examinar um tutorial](hdinsight-apache-spark-use-bi-tools.md)

O Apache Spark no HDInsight armazena dados no Armazenamento do Azure ou no Azure Data Lake Store. Especialistas comerciais principais tomadores de decisão podem analisar e criar relatórios sobre dados e usar relatórios interativos do Microsoft Power BI toobuild de dados analisado de saudação. Analistas podem iniciar a partir de dados não estruturados/semi estruturado no armazenamento de cluster, defina um esquema para dados de saudação usando blocos de anotações e, em seguida, criar modelos de dados usando o Microsoft Power BI. Os clusters do Spark no HDInsight também dão suporte a várias ferramentas de BI de terceiros, como o Tableau, tornando-os uma plataforma ideal para analistas de dados, especialistas de negócios e os principais responsáveis por tomar decisões.

### <a name="spark-machine-learning"></a>Machine Learning do Spark
[Examine um tutorial: prever temperaturas de prédios usando dados do sistema HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[Examine um tutorial: prever resultados da inspeção de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

O Apache Spark vem com [MLlib](http://spark.apache.org/mllib/), uma biblioteca de machine learning criada com base no Spark que pode ser usada em um cluster do Spark no HDInsight. O cluster Spark no HDInsight também inclui o Anaconda, uma distribuição do Python com uma variedade de pacotes para aprendizado de máquina. Junte isso a um suporte interno para blocos de anotações do Jupyter e do Zeppelin e terá um ambiente de alto nível para criar aplicativos de aprendizado de máquina.

### <a name="spark-streaming-and-real-time-data-analysis"></a>Análise de dados de streaming e em tempo real do Spark
[Examinar um tutorial](hdinsight-apache-spark-eventhub-streaming.md)

Os clusters Spark no HDInsight dão suporte avançado para criar soluções de análise em tempo real. Embora o Spark já tenha dados tooingest dos conectores de várias fontes, como soquetes TCP, Flume, Twitter, ZeroMQ ou Kafka, Spark no HDInsight adiciona suporte de primeira classe para a ingestão de dados de Hubs de eventos do Azure. Hubs de eventos são Olá usados amplamente o serviço de enfileiramento de mensagens no Azure. Ter um excelente suporte pronto para uso para hubs de eventos torna os clusters Spark no HDInsight a plataforma ideal para a criação de pipeline de análise em tempo real.

## <a name="next-steps"></a>Quais componentes estão incluídos como parte de um cluster do Spark?
Clusters Spark no HDInsight incluem hello componentes que estão disponíveis em clusters de saudação por padrão a seguir.

* [Núcleo do Spark](https://spark.apache.org/docs/1.5.1/). Inclui Spark Core, Spark SQL, APIs de streaming do Spark, GraphX e MLlib.
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Bloco de anotações do Jupyter](https://jupyter.org)
* [Bloco de anotações do Zeppelin](http://zeppelin-project.org/)

Os clusters Spark no HDInsight também fornecem um [driver ODBC](http://go.microsoft.com/fwlink/?LinkId=616229) para clusters de tooSpark de conectividade no HDInsight das ferramentas de BI, como o Microsoft Power BI e Tableau.

## <a name="where-do-i-start"></a>Por onde começo?
Inicie com a criação de um cluster Spark no HDInsight. Confira [Início rápido: provisionar um cluster do Spark no HDInsight e executar consulta interativa usando o Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="next-steps"></a>Próximas etapas
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
* [Problemas conhecidos do Apache Spark no HDInsight](hdinsight-apache-spark-known-issues.md).
