---
title: Receber eventos de Hubs de Eventos do Azure usando o Apache Storm | Microsoft Docs
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
ms.openlocfilehash: 3e15370c7602276ef323708632b324fe05497f41
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="1f7d4-103">Receber eventos de Hubs de Eventos usando o Apache Storm</span><span class="sxs-lookup"><span data-stu-id="1f7d4-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="1f7d4-104">[Apache Storm](https://storm.incubator.apache.org) é um sistema de computação distribuído em tempo real que simplifica o processamento confiável de fluxos de dados ilimitados.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="1f7d4-105">Esta seção mostra como usar um spout do Storm de Hubs de Eventos do Azure para receber eventos de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-105">This section shows how to use an Azure Event Hubs Storm spout to receive events from Event Hubs.</span></span> <span data-ttu-id="1f7d4-106">Usando o Apache Storm, você pode dividir eventos em vários processos hospedados em nós diferentes.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="1f7d4-107">A integração de Hubs de Eventos com o Storm simplifica o consumo de eventos pela verificação de forma transparente de seu progresso usando a instalação de Zookeeper do Storm, gerenciando pontos de verificação persistentes e recebimentos paralelos de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-107">The Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="1f7d4-108">Para obter mais informações sobre padrões de recebimento de Hubs de Eventos, consulte [Visão geral de hubs de eventos][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="1f7d4-108">For more information about Event Hubs receive patterns, see the [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="1f7d4-109">Criar o projeto e adicionar o código</span><span class="sxs-lookup"><span data-stu-id="1f7d4-109">Create project and add code</span></span>

<span data-ttu-id="1f7d4-110">Este tutorial usa uma instalação do [HDInsight Storm][HDInsight Storm], que acompanha o spout de Hubs de Eventos já disponível.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with the Event Hubs spout already available.</span></span>

1. <span data-ttu-id="1f7d4-111">Siga o procedimento [HDInsight Storm - Introdução](../hdinsight/hdinsight-storm-overview.md) para criar um novo cluster HDInsight e conectá-lo por meio da Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-111">Follow the [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure to create a new HDInsight cluster, and connect to it via Remote Desktop.</span></span>
2. <span data-ttu-id="1f7d4-112">Copie o arquivo `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` para seu ambiente de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-112">Copy the `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file to your local development environment.</span></span> <span data-ttu-id="1f7d4-113">Ele contém o events-storm-spout.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-113">This contains the events-storm-spout.</span></span>
3. <span data-ttu-id="1f7d4-114">Use o seguinte comando para instalar o pacote no armazenamento Maven local.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-114">Use the following command to install the package into the local Maven store.</span></span> <span data-ttu-id="1f7d4-115">Isso permite que você adicione-o como uma referência no projeto Storm em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-115">This enables you to add it as a reference in the Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="1f7d4-116">No Eclipse, crie um novo projeto Maven (clique em **Arquivo**, **Novo** e **Projeto**).</span><span class="sxs-lookup"><span data-stu-id="1f7d4-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="1f7d4-117">Selecione **Uso do local de espaço de trabalho padrão** e clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="1f7d4-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="1f7d4-118">Selecione o arquétipo **maven-archetype-quickstart**, depois clique em **Avançar**</span><span class="sxs-lookup"><span data-stu-id="1f7d4-118">Select the **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="1f7d4-119">Insira um **GroupId** e **ArtifactId** e clique em **Concluir**</span><span class="sxs-lookup"><span data-stu-id="1f7d4-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="1f7d4-120">Em **pom.xml**, adicione as seguintes dependências ao nó `<dependency>`.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-120">In **pom.xml**, add the following dependencies in the `<dependency>` node.</span></span>

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

9. <span data-ttu-id="1f7d4-121">Na pasta **src**, crie um arquivo chamado **Config.properties** e copie o seguinte conteúdo, substituindo os valores `receive rule key` e `event hub name`:</span><span class="sxs-lookup"><span data-stu-id="1f7d4-121">In the **src** folder, create a file called **Config.properties** and copy the following content, substituting the `receive rule key` and `event hub name` values:</span></span>

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
    <span data-ttu-id="1f7d4-122">O valor para **eventhub.receiver.credits** determina quantos eventos são divididos em lotes antes de liberá-los para o pipeline do Storm.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-122">The value for **eventhub.receiver.credits** determines how many events are batched before releasing them to the Storm pipeline.</span></span> <span data-ttu-id="1f7d4-123">Para simplificar, este exemplo define esse valor como 10.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-123">For the sake of simplicity, this example sets this value to 10.</span></span> <span data-ttu-id="1f7d4-124">Em produção, ele normalmente deve ser definido para valores mais altos; por exemplo, 1024.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-124">In production, it should usually be set to higher values; for example, 1024.</span></span>
10. <span data-ttu-id="1f7d4-125">Crie uma nova classe chamada **LoggerBolt** com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="1f7d4-125">Create a new class called **LoggerBolt** with the following code:</span></span>
    
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
    
    <span data-ttu-id="1f7d4-126">Este bolt do Storm registra o conteúdo dos eventos recebidos.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-126">This Storm bolt logs the content of the received events.</span></span> <span data-ttu-id="1f7d4-127">Isso pode ser estendido facilmente para armazenar tuplas em um serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-127">This can easily be extended to store tuples in a storage service.</span></span> <span data-ttu-id="1f7d4-128">O [tutorial de análise de sensor HDInsight] usa essa mesma abordagem para armazenar dados em HBase.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-128">The [HDInsight sensor analysis tutorial] uses this same approach to store data into HBase.</span></span>
11. <span data-ttu-id="1f7d4-129">Crie uma classe chamada **LogTopology** com o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f7d4-129">Create a class called **LogTopology** with the following code:</span></span>
    
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
        
            // set the number of workers to be the same as partition number.
            // the idea is to have a spout and a logger bolt co-exist in one
            // worker to avoid shuffling messages across workers in storm cluster.
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

    <span data-ttu-id="1f7d4-130">Essa classe cria um novo spout de Hubs de Eventos, usando as propriedades no arquivo de configuração para instanciá-lo.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-130">This class creates a new Event Hubs spout, using the properties in the configuration file to instantiate it.</span></span> <span data-ttu-id="1f7d4-131">É importante observar que esse exemplo cria tantas tarefas spouts quanto o número de partições no hub de eventos, para usar o paralelismo máximo permitido por esse hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="1f7d4-131">It is important to note that this example creates as many spouts tasks as the number of partitions in the event hub, in order to use the maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f7d4-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f7d4-132">Next steps</span></span>
<span data-ttu-id="1f7d4-133">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="1f7d4-133">You can learn more about Event Hubs by visiting the following links:</span></span>

* <span data-ttu-id="1f7d4-134">[Visão Geral dos Hubs de Eventos][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="1f7d4-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="1f7d4-135">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="1f7d4-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="1f7d4-136">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="1f7d4-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
<span data-ttu-id="1f7d4-137">[tutorial de análise de sensor HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span><span class="sxs-lookup"><span data-stu-id="1f7d4-137">[HDInsight sensor analysis tutorial]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md</span></span>

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
