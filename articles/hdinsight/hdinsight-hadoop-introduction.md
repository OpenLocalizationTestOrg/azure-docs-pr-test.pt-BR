---
title: "aaaWhat são HDInsight, pilha de tecnologia de Hadoop Olá & clusters? - Azure | Microsoft Docs"
description: "Pilha de tecnologia do Hadoop uma introdução tooHDInsight e hello e componentes, incluindo Spark, Kafka, Hive, HBase para análise de dados grande."
keywords: "hadoop do Azure, azure hadoop, gratuito do hadoop, introdução do hadoop, pilha de tecnologia do hadoop, toohadoop gratuito, toohadoop Introdução, o que é um cluster de hadoop, o que é o cluster de hadoop, que é hadoop usado"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>Introdução tooAzure HDInsight, pilha de tecnologia de Hadoop hello e clusters de Hadoop
 Este artigo fornece uma introdução tooAzure HDInsight, uma distribuição em nuvem Olá Hadoop da pilha de tecnologia. Ele também aborda o que é um cluster Hadoop e quando usá-lo. 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>O que é HDInsight e hello Hadoop pilha de tecnologia? 
HDInsight do Azure é uma distribuição em nuvem dos componentes de Hadoop de saudação do hello [Hortonworks Data Platform (HDP)](https://hortonworks.com/products/data-center/hdp/). [Apache Hadoop](http://hadoop.apache.org/) foi framework de código-fonte original Olá para processamento distribuído e análise de grandes conjuntos de dados em clusters de computadores. 


pilha de tecnologia de Hadoop Olá inclui softwares e utilitários, incluindo Apache Hive, HBase, Spark, Kafka e muitos outros. toosee Hadoop tecnologia pilha componentes disponíveis no HDInsight, consulte [componentes e as versões disponíveis com o HDInsight][component-versioning]. tooread mais sobre o Hadoop no HDInsight, consulte Olá [página de recursos do Azure para HDInsight](https://azure.microsoft.com/services/hdinsight/).

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>O que é um cluster Hadoop e quando usá-lo?
*Hadoop* também é um tipo de cluster que tem:

* YARN para gerenciamento de recursos e agendamento de trabalho
* MapReduce para processamento paralelo
* Olá sistema de arquivos distribuído de Hadoop (HDFS)
  
Os clusters Hadoop geralmente são usados para processamento de dados armazenados em lotes. Outros tipos de clusters no HDInsight têm recursos adicionais: o Spark ganhou popularidade devido ao seu processamento mais rápido na memória. Consulte [Tipos de Cluster no HDInsight](#overview) para obter detalhes.

## <a name="what-is-big-data"></a>O que é big data?
Big data descreve qualquer grande quantidade de informações digitais, como:

* Dados do sensor de equipamentos industriais
* Atividade de cliente coletada de um site
* Um feed de notícias do Twitter

O Big Data está sendo coletado em volumes crescentes, em velocidades mais altas e em uma maior variedade de formatos. Ele pode ser histórica (ou seja, armazenados) ou em tempo real (ou seja, de streaming da origem de saudação). 

## <a name="overview"></a>Tipos de cluster no HDInsight
O HDInsight inclui tipos específicos de cluster e recursos de personalização do cluster, como a adição de componentes, utilitários e idiomas.

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Spark, Kafka, Hive interativo, HBase, personalizado e outros tipos de cluster
HDInsight oferece Olá seguintes tipos de cluster:

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: usa [HDFS](#hdfs), [YARN](#yarn) gerenciamento de recursos e um simples [MapReduce](#mapreduce) tooprocess do modelo de programação e Analise dados em lotes em paralelo.
* **[Apache Spark](http://spark.apache.org/)**: uma estrutura de processamento paralelo que oferece suporte a processamento na memória tooboost Olá desempenho de aplicativos de análise de dados grande, despertar works para SQL, o fluxo de dados e aprendizado de máquina. Confira [O que é o Apache Spark no HDInsight?](hdinsight-apache-spark-overview.md)
* **[Apache HBase](http://hbase.apache.org/)**: um banco de dados NoSQL baseado em Hadoop que fornece acesso aleatório e coerência forte para big data não estruturado e semiestruturado (potencialmente, bilhões de linhas vezes milhões de colunas). Confira [O que é o HBase em HDInsight?](hdinsight-hbase-overview.md)
* **[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)**: um servidor para hospedagem e gerenciamento paralelo, processos R distribuídos. Ele fornece os cientistas de dados estatísticos e programadores de R com tooscalable acesso sob demanda, distribuídos métodos de análise no HDInsight. Consulte a [Visão geral do Servidor R no HDInsight](hdinsight-hadoop-r-server-overview.md).
* **[Apache Storm](https://storm.incubator.apache.org/)**: um sistema de computação distribuído e em tempo real para processar rapidamente grandes fluxos de dados. O Storm é oferecido como um cluster gerenciado no HDInsight. Consulte [Analisar dados do sensor em tempo real usando o Storm e o Hadoop](hdinsight-storm-sensor-data-analysis.md).
* **[Pré-visualização do Apache Interactive Hive (ou: vida longa e processo)](https://cwiki.apache.org/confluence/display/Hive/LLAP)**: cache na memória para consultas Hive interativas e mais rápidas. Consulte [Usar o Interactive Hive no HDInsight](hdinsight-hadoop-use-interactive-hive.md).
* **[Apache Kafka](https://kafka.apache.org/)**: uma plataforma de código-fonte aberto usada para criar aplicativos e pipelines de dados de transmissão. Kafka também fornece funcionalidade de fila de mensagens que permite que você toopublish e assina toodata fluxos. Consulte [tooApache Introdução Kafka no HDInsight](hdinsight-apache-kafka-introduction.md).

Você também pode configurar clusters usando Olá métodos a seguir:
* **[Visualização de clusters domínio](hdinsight-domain-joined-introduction.md)**: um cluster ingressados no domínio do Active Directory tooan para que você possa controlar o acesso e fornecer controle de dados.
* **[Clusters personalizados com ações de script](hdinsight-hadoop-customize-cluster-linux.md)**: clusters com scripts que são executados durante o provisionamento instalam componentes adicionais.

### <a name="example-cluster-customization-scripts"></a>Scripts de personalização de cluster de exemplo
Ações de script são scripts de Bash no Linux que executam o durante o provisionamento de cluster e que pode ser usado tooinstall de componentes adicionais no cluster de saudação. 

Olá scripts de exemplo a seguir são fornecidos pela equipe de HDInsight hello:

* **[Matiz](hdinsight-hadoop-hue-linux.md)**: um conjunto de web toointeract de aplicativos usados com um cluster. Somente clusters do Linux.
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**: gráfico de processamento toomodel relações entre itens ou pessoas.
* **[Solr](hdinsight-hadoop-solr-install-linux.md)**: uma plataforma de pesquisa de escala empresarial que permite a pesquisa de texto completo em dados.

Para saber mais sobre como desenvolver suas próprias ações de script, consulte [Desenvolvimento de ação de script com o HDInsight](hdinsight-hadoop-script-actions-linux.md).

## <a name="components-and-utilities-on-hdinsight-clusters"></a>Componentes e utilitários em clusters HDInsight
Olá utilitários e componentes a seguir estão incluídos nos clusters HDInsight:

* **[Ambari](#ambari)**: provisionamento, gerenciamento e monitoramento e utilitários de clusters.
* **[Avro](#avro)**  (biblioteca do Microsoft .NET para Avro): serialização de dados para o ambiente do Microsoft .NET hello. 
* **[Hive e HCatalog](#hive)**: consulta similar a SQL e uma camada de gerenciamento de armazenamento e tabela.
* **[Mahout](#mahout)**: aplicativos de aprendizado de máquina escalonáveis.
* **[MapReduce](#mapreduce)**: estrutura herdada para processamento e gerenciamento de recursos distribuídos do Hadoop. Confira [YARN](#yarn).
* **[Oozie](#oozie)**: gerenciamento de fluxo de trabalho.
* **[Phoenix](#phoenix)**: uma camada de banco de dados relacional em HBase.
* **[Pig](#pig)**: script mais simples para transformações de MapReduce.
* **[Sqoop](#sqoop)**: importação e exportação de dados.
* **[Tez](#tez)**: permite toorun processos com uso intenso de dados com eficiência em escala.
* **[YARN](#yarn)**: gerenciamento de recursos que faz parte da biblioteca principal do hello Hadoop.
* **[ZooKeeper](#zookeeper)**: coordenação de processos em sistemas distribuídos.

> [!NOTE]
> Para obter informações sobre componentes específicos de saudação e informações de versão, consulte [Hadoop componentes e as versões em HDInsight][component-versioning]
>
>

### <a name="ambari"></a>Ambari
O Apache Ambari serve para provisionar, gerenciar e monitorar clusters do Apache Hadoop. Ele inclui uma coleção de intuitiva das ferramentas de operador e um conjunto robusto de APIs que ocultam a complexidade de saudação do Hadoop, simplificando a operação de saudação de clusters. Clusters HDInsight no Linux fornecem ambos Olá Ambari web da interface do usuário e Olá Ambari REST API. As exibições da Ambari em clusters HDInsight permitem recursos de plug-in de interface de usuário.
Consulte [Gerenciar clusters HDInsight usando o Ambari](hdinsight-hadoop-manage-ambari.md) e <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Referência de API do Apache Ambari</a>.

### <a name="avro"></a>Avro (Biblioteca do Microsoft .NET para Avro)
Olá biblioteca do Microsoft .NET para Avro implementa o formato de intercâmbio de dados binários compact Olá Apache Avro para serialização para o ambiente do Microsoft .NET hello. Ele define um esquema com neutralidade de idioma para que os dados serializados em uma linguagem possam ser lidos em outra diferente. Informações detalhadas sobre o formato de saudação podem ser encontradas no hello < um destino = href de _ "em branco" = "http://avro.apache.org/docs/current/spec.html" > especificação do Apache Avro</a>. formato de saudação de saudação do Avro arquivos dá suporte a distributed MapReduce modelo de programação: arquivos são "divisíveis", que significa que você pode atingir qualquer ponto em um arquivo e iniciar a leitura de um bloco específico. toofind como, consulte [serializar dados com hello biblioteca do Microsoft .NET para Avro](hdinsight-dotnet-avro-serialization.md). Cluster baseado em Linux toocome de suporte.

### <a name="hdfs"></a>HDFS
Sistema de arquivos distribuído da Hadoop (HDFS) é um sistema de arquivos que, com YARN e MapReduce, é o núcleo de saudação do Hadoop tecnologia. Ele 's sistema de arquivos padrão de saudação para clusters de Hadoop no HDInsight. Confira [Consultar dados de armazenamento compatível com HDFS](hdinsight-hadoop-use-blob-storage.md).

### <a name="hive"></a>Hive & HCatalog
<a target="_blank" href="http://hive.apache.org/">O Apache Hive</a> é de data warehouse de software integrado no Hadoop que permite que você tooquery e gerenciar grandes conjuntos de dados no armazenamento distribuído usando uma linguagem semelhante a SQL chamada HiveQL. O Hive, como o Pig, é uma abstração sobre o MapReduce e converte consultas em uma série de trabalhos MapReduce. Seção é mais próximo sistema de gerenciamento de banco de dados relacional tooa de Pig e é usada com dados estruturados mais. Para dados não estruturados, Pig é Olá melhor opção. Consulte [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md).

O <a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> é uma camada de gerenciamento de armazenamento e de tabela para Hadoop que apresenta a você uma exibição de dados relacional. No HCatalog, você pode ler e gravar arquivos em qualquer formato que funcione para um Hive SerDe (serializador desserializador).

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> é uma biblioteca de algoritmos de aprendizado de máquina que são executados no Hadoop. Aplicativos de aprendizado de máquina usando princípios de estatísticas, ensinam toolearn de sistemas de dados e toouse ao resultados toodetermine futuras comportamento anterior. Consulte [Gerar recomendações de vídeo usando o Mahout no Hadoop](hdinsight-mahout.md).

### <a name="mapreduce"></a>MapReduce
MapReduce é a estrutura de software herdado de saudação para Hadoop para escrever aplicativos toobatch processo grandes conjuntos de dados em paralelo. Um trabalho de MapReduce divide grandes conjuntos de dados e organiza dados saudação em pares chave-valor para processamento. Os trabalhos MapReduce são executados em [YARN](#yarn). Consulte <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> em Olá Hadoop Wiki.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> é um sistema de coordenação do fluxo de trabalho que gerencia trabalhos do Hadoop. Ele é integrado com pilha de Hadoop hello e dá suporte a trabalhos do Hadoop para MapReduce e Sqoop, Hive e Pig. Ele também pode ser usado tooschedule trabalhos tooa específico sistema, como programas de Java ou scripts de shell. Confira [Usar o Oozie com o Hadoop](hdinsight-use-oozie-linux-mac.md).

### <a name="phoenix"></a>Phoenix
O <a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> é uma camada de banco de dados relacional em HBase. Phoenix inclui um driver JDBC que permite que você tooquery e gerencia tabelas SQL diretamente. O Phoenix converte consultas e outras instruções em chamadas de API NoSQL nativas, em vez de usar o MapReduce, permitindo, assim, aplicativos mais rápidos sobre repositórios NoSQL. Consulte [Usar Apache Phoenix e SQuirreL com clusters do HBase](hdinsight-hbase-phoenix-squirrel.md).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> é uma plataforma de alto nível que permite transformações complexas de MapReduce tooperform em grandes conjuntos de dados usando uma linguagem de script simple chamada Pig latino. Pig converte scripts de Pig latino Olá para eles executará no Hadoop. Você pode criar funções definidas pelo usuário (UDFs) tooextend Pig latino. Confira [Usar o Pig com o Hadoop](hdinsight-use-pig.md).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> é uma ferramenta que transferências dados em massa entre o Hadoop e bancos de dados relacionais, como um SQL, ou outros repositórios de dados estruturados, da forma mais eficiente possível. Consulte [Usar o Sqoop com o Hadoop](hdinsight-use-sqoop.md).

### <a name="tez"></a>Tez
O <a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> é uma estrutura de aplicativo baseada no Hadoop YARN que executa gráficos complexos, gráficos acíclicos de processamento geral de dados. É um mais flexível e poderosa sucessor toohello MapReduce framework que permite que os processos de volumes de dados, como o Hive, toorun com mais eficiência em escala. Consulte ["Usar o Apache Tez para melhorar o desempenho" em Usar o Hive e HiveQL](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Apache YARN é hello próxima geração de MapReduce (MapReduce 2.0 ou MRv2) e oferece suporte a cenários de processamento de dados além com maior escalabilidade e processamento em tempo real de processamento em lotes de MapReduce. O YARN fornece gerenciamento de recursos e uma estrutura de aplicativo distribuída. Trabalhos MapReduce executados em YARN. Consulte <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce (YARN)</a>.

### <a name="zookeeper"></a>ZooKeeper
O <a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> coordena processos em grandes sistemas distribuídos usando um namespace hierárquico compartilhado de registros de dados (znodes). Znodes conter pequenas quantidades de meta informações necessárias toocoordinate processos: status, local, configuração e assim por diante. Veja um exemplo de [ZooKeeper com um cluster HBase e Apache Phoenix](hdinsight-hbase-phoenix-squirrel-linux.md). 

## <a name="programming-languages-on-hdinsight"></a>Linguagens de programação no HDInsight
Os clusters de HDInsight - Spark, HBase, Kafka, Hadoop e outros clusters - dão suporte a várias linguagens de programação, mas alguns não estão instalados por padrão. Para bibliotecas, módulos ou pacotes não instalados por padrão, [usar um componente de saudação do script ação tooinstall](hdinsight-hadoop-script-actions-linux.md). 

### <a name="default-programming-language-support"></a>Suporte padrão à linguagem de programação
Por padrão, os clusters HDInsight são compatíveis com:

* Java
* Python

Idiomas adicionais podem ser instalados usando [ações de script](hdinsight-hadoop-script-actions-linux.md).

### <a name="java-virtual-machine-jvm-languages"></a>Linguagens JVM (máquina virtual Java)
Muitos idiomas diferentes do Java podem ser executado em uma máquina virtual de Java (JVM); No entanto, executar alguns desses idiomas pode exigir componentes adicionais instalados no cluster hello.

Essas linguagens baseadas em JVM são permitidas nos clusters HDInsight:

* Clojure
* Jython (Python para Java)
* Scala

### <a name="hadoop-specific-languages"></a>Linguagens específicas do Hadoop
Clusters HDInsight suportam Olá idiomas que são o conjunto de tecnologias de Hadoop toohello específicas a seguir:

* Pig Latin para trabalhos do Pig
* HiveQL para trabalhos do Hive e SparkSQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standard e HDInsight Premium
O HDInsight fornece ofertas de nuvem de big data em duas categorias, Standard e Premium. HDInsight padrão fornece um cluster de grande porte que as organizações podem usar toorun suas cargas de trabalho de dados grandes. O HDInsight Premium baseia-se nos recursos padrão e fornece recursos avançados de análise e segurança para um cluster HDInsight. Para obter mais informações, confira [Azure HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a name="microsoft-business-intelligence-and-hdinsight"></a>Microsoft Business Intelligence e HDInsight
Ferramentas familiares de business intelligence (BI) recuperar, analisar, dados integrados ao HDInsight usando qualquer Olá Power Query no relatam ou Olá Microsoft ODBC Driver Hive:

* [Conectar Excel tooHadoop com o Power Query](hdinsight-connect-excel-power-query.md): Saiba como tooconnect Excel toohello conta de armazenamento do Azure que armazena Olá dados do seu cluster HDInsight usando o Microsoft Power Query para Excel. Estação de trabalho do Windows necessária. 
* [Conectar Excel tooHadoop com hello Microsoft ODBC Driver Hive](hdinsight-connect-excel-hive-odbc-driver.md): Saiba como dados de tooimport de HDInsight com hello Microsoft ODBC Driver Hive. Estação de trabalho do Windows necessária. 
* [Plataforma de nuvem da Microsoft](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): Saiba mais sobre o Power BI para Office 365, baixe a avaliação do SQL Server hello e configurar o SharePoint Server 2013 e o BI do SQL Server.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [Serviços de Relatório do SQL Server](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>Próximas etapas

* [Introdução ao Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md): um tutorial de início rápido para provisionamento de clusters do Hadoop no HDInsight e execução de consultas Hive de exemplo.
* [Introdução ao Spark no HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md): um tutorial de início rápido para criar um cluster Spark e executar consultas interativas do Spark SQL.
* [Usar Servidor R no HDInsight](hdinsight-hadoop-r-server-get-started.md): comece a usar o Servidor R no HDInsight Premium.
* [Provisionar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Saiba como tooprovision uma HDInsight Hadoop de cluster por meio de hello Azure PowerShell, CLI do Azure ou portal do Azure.


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/