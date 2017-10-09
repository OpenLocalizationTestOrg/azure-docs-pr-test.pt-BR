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
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="07ff5-103">Receber eventos de Hubs de Eventos usando o Apache Storm</span><span class="sxs-lookup"><span data-stu-id="07ff5-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="07ff5-104">[Apache Storm](https://storm.incubator.apache.org) é um sistema de computação distribuído em tempo real que simplifica o processamento confiável de fluxos de dados ilimitados.</span><span class="sxs-lookup"><span data-stu-id="07ff5-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="07ff5-105">Esta seção mostra como toouse uma profusão de Hubs de eventos do Azure spout tooreceive eventos dos Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="07ff5-105">This section shows how toouse an Azure Event Hubs Storm spout tooreceive events from Event Hubs.</span></span> <span data-ttu-id="07ff5-106">Usando o Apache Storm, você pode dividir eventos em vários processos hospedados em nós diferentes.</span><span class="sxs-lookup"><span data-stu-id="07ff5-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="07ff5-107">Olá integração com Hubs de evento com Storm simplifica consumo de eventos pelo ponto de verificação transparente seu progresso usando a instalação de Zookeeper do Storm, gerenciar pontos de verificação persistentes e paralelo recebe de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="07ff5-107">hello Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="07ff5-108">Para obter mais informações sobre Hubs de eventos de recebimento padrões, consulte Olá [visão geral de Hubs de eventos][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="07ff5-108">For more information about Event Hubs receive patterns, see hello [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="07ff5-109">Criar o projeto e adicionar o código</span><span class="sxs-lookup"><span data-stu-id="07ff5-109">Create project and add code</span></span>

<span data-ttu-id="07ff5-110">Este tutorial usa um [profusão de HDInsight] [ HDInsight Storm] instalação, o que vem com hello spout Hubs de eventos já disponível.</span><span class="sxs-lookup"><span data-stu-id="07ff5-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with hello Event Hubs spout already available.</span></span>

1. <span data-ttu-id="07ff5-111">Siga Olá [HDInsight Storm - Introdução](../hdinsight/hdinsight-storm-overview.md) procedimento toocreate HDInsight um novo cluster e conectar-se tooit por meio da área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="07ff5-111">Follow hello [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure toocreate a new HDInsight cluster, and connect tooit via Remote Desktop.</span></span>
2. <span data-ttu-id="07ff5-112">Saudação de cópia `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` ambiente de desenvolvimento local do arquivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="07ff5-112">Copy hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file tooyour local development environment.</span></span> <span data-ttu-id="07ff5-113">Ele contém Olá eventos storm spout.</span><span class="sxs-lookup"><span data-stu-id="07ff5-113">This contains hello events-storm-spout.</span></span>
3. <span data-ttu-id="07ff5-114">Saudação de uso após o pacote de saudação do comando tooinstall no repositório local de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="07ff5-114">Use hello following command tooinstall hello package into hello local Maven store.</span></span> <span data-ttu-id="07ff5-115">Isso permite que você tooadd-lo como uma referência em Olá profusão de projeto em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="07ff5-115">This enables you tooadd it as a reference in hello Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="07ff5-116">No Eclipse, crie um novo projeto Maven (clique em **Arquivo**, **Novo** e **Projeto**).</span><span class="sxs-lookup"><span data-stu-id="07ff5-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="07ff5-117">Selecione **Uso do local de espaço de trabalho padrão** e clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="07ff5-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="07ff5-118">Selecione Olá **maven-arquétipo-quickstart** arquétipo, em seguida, clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="07ff5-118">Select hello **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="07ff5-119">Insira um **GroupId** e **ArtifactId** e clique em **Concluir**</span><span class="sxs-lookup"><span data-stu-id="07ff5-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="07ff5-120">Em **pom.xml**, adicionar Olá seguindo as dependências no hello `<dependency>` nó.</span><span class="sxs-lookup"><span data-stu-id="07ff5-120">In **pom.xml**, add hello following dependencies in hello `<dependency>` node.</span></span>

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

9. <span data-ttu-id="07ff5-121">Em Olá **src** pasta, crie um arquivo chamado **config** e cópia hello conteúdo a seguir, substituindo Olá `receive rule key` e `event hub name` valores:</span><span class="sxs-lookup"><span data-stu-id="07ff5-121">In hello **src** folder, create a file called **Config.properties** and copy hello following content, substituting hello `receive rule key` and `event hub name` values:</span></span>

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
    <span data-ttu-id="07ff5-122">Olá valor **eventhub.receiver.credits** determina quantos eventos são em lote antes de liberar o pipeline de profusão de toohello.</span><span class="sxs-lookup"><span data-stu-id="07ff5-122">hello value for **eventhub.receiver.credits** determines how many events are batched before releasing them toohello Storm pipeline.</span></span> <span data-ttu-id="07ff5-123">Para a mesma Olá de simplicidade, este exemplo define too10 esse valor.</span><span class="sxs-lookup"><span data-stu-id="07ff5-123">For hello sake of simplicity, this example sets this value too10.</span></span> <span data-ttu-id="07ff5-124">Em produção, normalmente, ele deve ser definido toohigher valores; Por exemplo, 1024.</span><span class="sxs-lookup"><span data-stu-id="07ff5-124">In production, it should usually be set toohigher values; for example, 1024.</span></span>
10. <span data-ttu-id="07ff5-125">Criar uma nova classe chamada **LoggerBolt** com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="07ff5-125">Create a new class called **LoggerBolt** with hello following code:</span></span>
    
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
    
    <span data-ttu-id="07ff5-126">Este raio Storm registra o conteúdo de saudação do eventos Olá recebida.</span><span class="sxs-lookup"><span data-stu-id="07ff5-126">This Storm bolt logs hello content of hello received events.</span></span> <span data-ttu-id="07ff5-127">Isso pode ser facilmente estendido toostore tuplas em um serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="07ff5-127">This can easily be extended toostore tuples in a storage service.</span></span> <span data-ttu-id="07ff5-128">Olá [tutorial de análise de sensor HDInsight] usa os mesmos dados toostore abordagem em HBase.</span><span class="sxs-lookup"><span data-stu-id="07ff5-128">hello [HDInsight sensor analysis tutorial] uses this same approach toostore data into HBase.</span></span>
11. <span data-ttu-id="07ff5-129">Criar uma classe chamada **LogTopology** com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="07ff5-129">Create a class called **LogTopology** with hello following code:</span></span>
    
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

    <span data-ttu-id="07ff5-130">Essa classe cria um novo spout de Hubs de eventos, usando as propriedades de saudação no hello tooinstantiate de arquivo de configuração-lo.</span><span class="sxs-lookup"><span data-stu-id="07ff5-130">This class creates a new Event Hubs spout, using hello properties in hello configuration file tooinstantiate it.</span></span> <span data-ttu-id="07ff5-131">É importante toonote Este exemplo cria quantas spouts tarefas como número de saudação de partições no hub de eventos hello, em ordem toouse Olá máximo paralelismo permitido por esse hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="07ff5-131">It is important toonote that this example creates as many spouts tasks as hello number of partitions in hello event hub, in order toouse hello maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07ff5-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07ff5-132">Next steps</span></span>
<span data-ttu-id="07ff5-133">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="07ff5-133">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="07ff5-134">[Visão Geral dos Hubs de Eventos][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="07ff5-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="07ff5-135">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="07ff5-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="07ff5-136">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="07ff5-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[tutorial de análise de sensor HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
