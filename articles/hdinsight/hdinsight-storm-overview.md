---
title: "aaaWhat é Apache Storm - HDInsight do Azure | Microsoft Docs"
description: "Apache Storm permite tooprocess fluxos de dados em tempo real. HDInsight do Azure permite que você tooeasily criar clusters Storm em Olá nuvem do Azure. Com o Visual Studio, você pode criar soluções Storm usando c# e implantar tooyour que clusters HDInsight Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "casos de uso do apache storm, cluster storm, o que é o apache storm"
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>O que é o Apache Storm no Azure HDInsight?

O [Apache Storm](http://storm.apache.org/) é um sistema de computação distribuída, tolerante a falhas e de software livre. Você pode usar fluxos de tooprocess profusão de dados em tempo real com Hadoop. Soluções Storm também podem fornecer garantia de processamento de dados, com hello capacidade tooreplay dados que não foi processado Olá primeira vez.

Storm no HDInsight fornece Olá principais vantagens a seguir:

* É executado como um serviço gerenciado com um SLA de 99,9% de tempo de atividade.

* Dá suporte à personalização fácil executando scripts em relação a um cluster Storm durante ou após a criação. Para obter mais informações, confira [Personalizar clusters HDInsight usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md).

* Usa vários idiomas. Você pode escrever componentes Storm no idioma de saudação de sua escolha, como Java, Python e c#.

    * Integra o Visual Studio HDInsight para desenvolvimento hello, gerenciamento e monitoramento de topologias de c#. Para obter mais informações, consulte [topologias de desenvolver c# Storm com hello ferramentas HDInsight para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

    * Interface de Java Trident de Olá oferece suporte. Você pode criar topologias Storm que dão suporte ao processamento de mensagens exatamente uma vez, à persistência de armazenamento de dados transacional e a um conjunto de operações de análise de fluxo comuns.

*  Dimensione clusters Storm facilmente. Você pode adicionar ou remover nós de trabalho com topologias de profusão de toorunning nenhum impacto.

* Integra-se com hello serviços do Azure a seguir:

    * Hubs de eventos do Azure

    * Rede Virtual do Azure

    * Banco de Dados SQL do Azure

    * Armazenamento do Azure

    * Azure Cosmos DB

* Com segurança combina recursos de saudação de vários clusters de HDInsight usando a rede Virtual. Você pode criar pipelines analíticos que usam clusters Storm, Kafka, Spark, HBase ou Hadoop.

Para obter uma lista de empresas que estão usando o Apache Storm em suas soluções de análise em tempo real, consulte [Empresas que estão usando o Apache Storm](https://storm.apache.org/documentation/Powered-By.html).

tooget iniciado usando Storm, consulte [Introdução ao Storm no HDInsight][gettingstarted].

## <a name="how-does-storm-work"></a>Como funciona o Storm

Tempestade executa topologias em vez da saudação trabalhos de MapReduce que você pode estar familiarizado com. As topologias do Storm são compostas por vários componentes organizados em um DAG (gráfico acíclico dirigido). Fluxos de dados entre os componentes de saudação no gráfico de saudação. Cada componente consome um ou mais fluxos de dados e, opcionalmente, pode emitir um ou mais fluxos. Olá diagrama a seguir ilustra como os dados fluem entre os componentes em uma topologia básica de contagem de palavras:

![Exemplo de como os componentes são organizados em uma topologia do Storm](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* Os componentes Spout trazem dados para uma topologia. Eles emitem um ou mais fluxos em topologia hello.

* Os componentes Bolt consomem fluxos emitidos de spouts ou de outros bolts. Parafusos opcionalmente podem emitir fluxos em topologia hello. Parafusos também serão responsáveis por gravar tooexternal os serviços de dados ou armazenamento, como o HDFS, Kafka ou HBase.

## <a name="ease-of-creation"></a>Fácil de criar

Você pode provisionar um novo cluster Storm no HDInsight em minutos. Para saber mais sobre como criar um cluster Storm, confira [Introdução ao Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

## <a name="ease-of-use"></a>Fácil de uso

* __Secure Shell (SSH) conectividade__: você pode acessar nós de cabeçalho de saudação do cluster Storm pela Olá Internet usando o SSH. Você pode executar comandos diretamente no cluster usando SSH.

  Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* __Web conectividade__: HDInsight todos os clusters fornecem Olá Ambari web da interface do usuário. Você pode facilmente monitorar, configurar e gerenciar serviços no seu cluster usando a interface da web hello Ambari. Clusters de Storm também fornecem Olá profusão de interface do usuário. Você pode monitorar e gerenciar as topologias Storm em execução no seu navegador usando Olá profusão de interface do usuário.

  Para obter mais informações, consulte Olá [HDInsight gerenciar usando Olá da interface do usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md) e [monitorar e gerenciar usando Olá profusão de interface do usuário](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) documentos.

* __Azure PowerShell e a CLI do Azure__: PowerShell e a CLI fornecem utilitários de linha de comando que você pode usar de seu toowork de sistema do cliente com o HDInsight e outros serviços do Azure.

* __Integração do Visual Studio__: Azure Data Lake Tools para Visual Studio inclui modelos de projeto para a criação de topologias de C# Storm usando Olá SCP.Net framework. Data Lake ferramentas também fornecem ferramentas toodeploy, monitorar e gerenciar soluções com Storm no HDInsight.

  Para obter mais informações, consulte [topologias de desenvolver c# Storm com hello ferramentas HDInsight para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="integration-with-other-azure-services"></a>Integração a outros serviços do Azure

* __Azure Data Lake Store__: para obter um exemplo de como usar o Data Lake Store com um cluster Storm, confira [Usar o Azure Data Lake Store com Apache Storm no HDInsight](hdinsight-storm-write-data-lake-store.md).

* __Hubs de eventos__: para obter um exemplo de como usar Hubs de eventos com um cluster Storm, consulte Olá documentos a seguir:

    * [Desenvolver uma topologia baseada em Java para Storm no HDInsight](hdinsight-storm-develop-java-topology.md)

    * [Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md)

* __Banco de dados SQL__, __Cosmos DB__, __Hubs de eventos__, e __HBase__: exemplos de modelo são incluídos na Olá Data Lake Tools para Visual Studio. Para saber mais,confira [Desenvolver uma topologia em C# para Storm no HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="reliability"></a>Confiabilidade

Apache Storm garante que cada mensagem de entrada é sempre totalmente processada, mesmo quando a análise de dados de saudação é distribuído entre centenas de nós.

nó de Nimbus Olá fornece funcionalidade semelhante toohello Hadoop JobTracker e atribui tarefas tooother nós em um cluster por meio de Zookeeper. Nós zookeeper fornecem coordenação de um cluster e facilitam a comunicação entre Nimbus e hello processo Supervisor em nós de trabalho hello. Se um nó de processamento falhar, nó de Nimbus Olá é informado e atribui tarefas hello e nó de tooanother dados associados.

configuração padrão de saudação para clusters do Apache Storm é apenas um nó de Nimbus toohave. O Storm no HDInsight oferece dois nós Nimbus. Se o nó primário Olá falhar, o cluster Storm de saudação alterna nó secundário toohello enquanto o nó primário Olá é recuperado. Olá diagrama a seguir ilustra configuração de fluxo de tarefa Olá para Storm no HDInsight:

![Diagrama do Nimbus, Zookeeper e Supervisor](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Escala

Os clusters HDInsight podem ser dimensionados dinamicamente com a adição ou remoção de nós de trabalho. Essa operação pode ser executada durante o processamento de dados.

> [!IMPORTANT]
> tootake proveito dos novos nós adicionados por meio de dimensionamento, precisa topologias de Storm toorebalance iniciadas antes de tamanho de cluster Olá foi aumentado.

## <a name="support"></a>Suporte

O Storm no HDInsight é fornecido com suporte contínuo completo de nível empresarial. O Storm no HDInsight também tem um SLA de 99,9%. Isso significa que podemos garantir que um cluster Storm tem conectividade externa pelo menos 99,9% de tempo de saudação.

Para saber mais, confira o [Suporte do Azure](https://azure.microsoft.com/support/options/).

## <a name="apache-storm-use-cases"></a>Casos de uso do Apache Storm

Olá seguem alguns cenários comuns para os quais você pode usar Storm no HDInsight:

* Internet das coisas (IoT)
* Detecção de fraude
* Análise das redes sociais
* Extração, transformação e carregamento (ETL)
* Monitoramento de rede
* Pesquisar
* Mobile Engagement

Para obter informações sobre cenários do mundo real, consulte Olá [como as empresas estão usando Storm](https://storm.apache.org/documentation/Powered-By.html) documento.

## <a name="development"></a>Desenvolvimento

Os desenvolvedores do .NET podem projetar e implementar topologias em C# usando Data Lake Tools para Visual Studio. Você também pode criar topologias híbridas que usam componentes Java e C#.

Para obter mais informações, consulte [Desenvolver topologias C# para o Storm no HDInsight usando o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Você também pode desenvolver soluções de Java usando Olá IDE de sua escolha. Para saber mais, confira [Desenvolver topologias em Java para o Storm no HDInsight](hdinsight-storm-develop-java-topology.md).

Python também pode ser usado toodevelop Storm componentes. Para saber mais, confira [Desenvolver topologias Storm usando Python no HDInsight](hdinsight-storm-develop-python-topology.md).

## <a name="common-development-patterns"></a>Padrões de desenvolvimento comuns

### <a name="guaranteed-message-processing"></a>Processamento de mensagem garantido

O Apache Storm pode oferecer diferentes níveis de processamento de mensagem garantido. Por exemplo, um aplicativo básico Storm pode garantir um processamento pelo menos uma vez e o Trident pode garantir o processamento exatamente uma vez.

Para obter mais informações, consulte [Garantias do processamento de dados](https://storm.apache.org/about/guarantees-data-processing.html) em apache.org.

### <a name="ibasicbolt"></a>IBasicBolt

Olá padrão de leitura de uma tupla de entrada, emitindo zero ou mais tuplas, e, em seguida, executar o método acking Olá entrada tupla imediatamente final Olá Olá é comum. Tempestade fornece Olá [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) interface tooautomate esse padrão.

### <a name="joins"></a>Junções

O modo como os fluxos de dados são unidos varia entre aplicativos. Por exemplo, você pode juntar cada tupla de vários fluxos em um novo fluxo ou pode juntar somente lotes de tuplas para uma janela específica. De qualquer forma, a junção pode ser realizada usando [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Campo de agrupamento é uma maneira de definir como tuplas são roteadas toobolts.

Olá Java de exemplo a seguir, fieldsGrouping é usado tooroute tuplas que se originam componentes "1", "2" e "3" toohello MyJoiner raio:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Lotes

O Apache Storm fornece um mecanismo de cronometragem interno conhecido como "tupla em escala". Você pode definir quantas vezes uma tupla em escala é emitida em sua topologia.

Para obter um exemplo de como usar uma tupla de escala de um componente em C#, confira [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).

### <a name="caches"></a>Caches

O cache na memória geralmente é usado como um mecanismo para acelerar o processamento, uma vez que mantém os ativos usados com mais frequência na memória. Como uma topologia é distribuída entre vários nós, e entre vários processos dentro de cada nó, considere o uso de [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-). Use `fieldsGrouping` tooensure tuplas contendo campos de saudação que são usados para pesquisa de cache sempre são roteada toohello mesmo processo. Essa funcionalidade de agrupamento evita a duplicação de entradas de cache entre os processos.

### <a name="stream-top-n"></a>Fluxo "N Superior"

Quando a topologia depende de calcular um valor top N, calcule o valor de N maiores de saudação em paralelo. Em seguida, mescle Olá saída desses cálculos em um valor global. Essa operação pode ser feita usando [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute por campo para processamento paralelo. Em seguida, você pode rotear o raio tooa que globalmente determina o valor de N maiores de saudação.

Para obter um exemplo de como calcular um valor top N, consulte Olá [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) exemplo.

## <a name="logging"></a>Registro em log

Tempestade usa Apache Log4j toolog informações. Por padrão, uma grande quantidade de dados é registrada e pode ser difícil toosort por meio das informações de saudação. Você pode incluir um arquivo de configuração de registro em log como parte de seu comportamento de registro em log toocontrol de topologia Storm.

Para uma topologia de exemplo que demonstra como tooconfigure log, consulte [baseados em Java WordCount](hdinsight-storm-develop-java-topology.md) exemplo para Storm no HDInsight.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre as soluções de análise em tempo real com o Storm no HDInsight:

* [Introdução ao Apache Storm no HDInsight][gettingstarted]
* [Topologias de exemplo para Apache Storm no HDInsight](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
