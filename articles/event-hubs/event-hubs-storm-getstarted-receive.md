---
title: eventos de aaaReceive de Hubs de eventos do Azure usando o Apache Storm | Microsoft Docs
description: Comece a receber de Hubs de Eventos usando o Apache Storm
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a0ab860ee8d504a28aac380c504c928f0d6dbc1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a>Receber eventos de Hubs de Eventos usando o Apache Storm

[Apache Storm](https://storm.incubator.apache.org) é um sistema de computação distribuído em tempo real que simplifica o processamento confiável de fluxos de dados ilimitados. Esta seção mostra como toouse uma profusão de Hubs de eventos do Azure spout tooreceive eventos dos Hubs de eventos. Usando o Apache Storm, você pode dividir eventos em vários processos hospedados em nós diferentes. Olá integração com Hubs de evento com Storm simplifica consumo de eventos pelo ponto de verificação transparente seu progresso usando a instalação de Zookeeper do Storm, gerenciar pontos de verificação persistentes e paralelo recebe de Hubs de eventos.

Para obter mais informações sobre Hubs de eventos de recebimento padrões, consulte Olá [visão geral de Hubs de eventos][Event Hubs overview].

## <a name="create-project-and-add-code"></a>Criar o projeto e adicionar o código

Este tutorial usa um [profusão de HDInsight] [ HDInsight Storm] instalação, o que vem com hello spout Hubs de eventos já disponível.

1. Siga Olá [HDInsight Storm - Introdução](../hdinsight/hdinsight-storm-overview.md) procedimento toocreate HDInsight um novo cluster e conectar-se tooit por meio da área de trabalho remota.
2. Saudação de cópia `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` ambiente de desenvolvimento local do arquivo tooyour. Ele contém Olá eventos storm spout.
3. Saudação de uso após o pacote de saudação do comando tooinstall no repositório local de Maven hello. Isso permite que você tooadd-lo como uma referência em Olá profusão de projeto em uma etapa posterior.

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. No Eclipse, crie um novo projeto Maven (clique em **Arquivo**, **Novo** e **Projeto**).
   
    ![][12]
5. Selecione **Uso do local de espaço de trabalho padrão** e clique em **Avançar**
6. Selecione Olá **maven-arquétipo-quickstart** arquétipo, em seguida, clique em **Avançar**
7. Insira um **GroupId** e **ArtifactId** e clique em **Concluir**
8. Em **pom.xml**, adicionar Olá seguindo as dependências no hello `<dependency>` nó.

    ```xml  
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>0.9.2-incubating</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.microsoft.eventhubs</groupId>
        <artifactId>eventhubs-storm-spout</artifactId>
        <version>0.9</version>
    </dependency>
    <dependency>
        <groupId>com.netflix.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>1.3.3</version>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
        <scope>provided</scope>
    </dependency>
    ```

9. Em Olá **src** pasta, crie um arquivo chamado **config** e cópia hello conteúdo a seguir, substituindo Olá `receive rule key` e `event hub name` valores:

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    Olá valor **eventhub.receiver.credits** determina quantos eventos são em lote antes de liberar o pipeline de profusão de toohello. Para a mesma Olá de simplicidade, este exemplo define too10 esse valor. Em produção, normalmente, ele deve ser definido toohigher valores; Por exemplo, 1024.
10. Criar uma nova classe chamada **LoggerBolt** com hello código a seguir:
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    Este raio Storm registra o conteúdo de saudação do eventos Olá recebida. Isso pode ser facilmente estendido toostore tuplas em um serviço de armazenamento. Olá [tutorial de análise de sensor HDInsight] usa os mesmos dados toostore abordagem em HBase.
11. Criar uma classe chamada **LogTopology** com hello código a seguir:
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set hello number of workers toobe hello same as partition number.
            // hello idea is toohave a spout and a logger bolt co-exist in one
            // worker tooavoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    Essa classe cria um novo spout de Hubs de eventos, usando as propriedades de saudação no hello tooinstantiate de arquivo de configuração-lo. É importante toonote Este exemplo cria quantas spouts tarefas como número de saudação de partições no hub de eventos hello, em ordem toouse Olá máximo paralelismo permitido por esse hub de eventos.

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos][Event Hubs overview]
* [Criar um hub de eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[tutorial de análise de sensor HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
