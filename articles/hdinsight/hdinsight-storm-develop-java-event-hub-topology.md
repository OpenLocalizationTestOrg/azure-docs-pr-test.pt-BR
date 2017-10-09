---
title: eventos de aaaProcess dos Hubs de eventos com Storm no HDInsight usando Java | Microsoft Docs
description: Saiba como tooprocess dados de Hubs de eventos com uma topologia de Java Storm criados com o Maven.
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="e3d54-103">Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="e3d54-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="e3d54-104">Saiba como toouse Hubs de eventos do Azure com Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3d54-104">Learn how toouse Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="e3d54-105">Este exemplo usa componentes baseados em Java tooread e gravar dados em Hubs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d54-105">This example uses Java-based components tooread and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="e3d54-106">Hubs de eventos do Azure permite que você tooprocess grandes quantidades de dados de sites, aplicativos e dispositivos.</span><span class="sxs-lookup"><span data-stu-id="e3d54-106">Azure Event Hubs allows you tooprocess massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="e3d54-107">Olá spout Hub de eventos torna fácil toouse Apache Storm no HDInsight tooanalyze esses dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="e3d54-107">hello Event Hub spout makes it easy toouse Apache Storm on HDInsight tooanalyze this data in real time.</span></span> <span data-ttu-id="e3d54-108">Você também pode escrever dados tooEvent Hubs do Storm usando Olá parafuso de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="e3d54-108">You can also write data tooEvent Hubs from Storm by using hello Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3d54-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e3d54-109">Prerequisites</span></span>

* <span data-ttu-id="e3d54-110">Um Apache Storm no cluster HDInsight versão 3.6.</span><span class="sxs-lookup"><span data-stu-id="e3d54-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="e3d54-111">Para obter mais informações, confira [Introdução ao Storm no cluster HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e3d54-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e3d54-112">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e3d54-112">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e3d54-113">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e3d54-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e3d54-114">Um [Hub de Eventos do Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="e3d54-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="e3d54-115">[Oracle JDK (Java Developer Kit) versão 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou equivalente, por exemplo [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="e3d54-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="e3d54-116">[Maven](https://maven.apache.org/download.cgi): o Maven é um sistema de criação de projetos para projetos Java.</span><span class="sxs-lookup"><span data-stu-id="e3d54-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="e3d54-117">Um editor de texto ou um IDE (ambiente de desenvolvimento integrado).</span><span class="sxs-lookup"><span data-stu-id="e3d54-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e3d54-118">Seu editor ou IDE pode ter uma funcionalidade específica para trabalhar com o Maven que não é abordada neste documento.</span><span class="sxs-lookup"><span data-stu-id="e3d54-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="e3d54-119">Para obter informações sobre os recursos de saudação do seu ambiente de edição, consulte a documentação Olá produto Olá que está usando.</span><span class="sxs-lookup"><span data-stu-id="e3d54-119">For information about hello capabilities of your editing environment, see hello documentation for hello product you are using.</span></span>

    * <span data-ttu-id="e3d54-120">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="e3d54-120">An SSH client.</span></span> <span data-ttu-id="e3d54-121">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e3d54-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="e3d54-122">Olá `ssh` e `scp` comandos.</span><span class="sxs-lookup"><span data-stu-id="e3d54-122">hello `ssh` and `scp` commands.</span></span> <span data-ttu-id="e3d54-123">Esses são o cluster do HDInsight usado toocopy arquivos toohello.</span><span class="sxs-lookup"><span data-stu-id="e3d54-123">These are used toocopy files toohello HDInsight cluster.</span></span> <span data-ttu-id="e3d54-124">No Windows, você pode obtê-los por meio do Bash no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="e3d54-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-hello-example"></a><span data-ttu-id="e3d54-125">Exemplo de hello Noções básicas sobre</span><span class="sxs-lookup"><span data-stu-id="e3d54-125">Understanding hello example</span></span>

<span data-ttu-id="e3d54-126">Olá [hdinsight-java storm eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) exemplo contém duas topologias:</span><span class="sxs-lookup"><span data-stu-id="e3d54-126">hello [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="e3d54-127">Olá `resources/writer.yaml` topologia grava dados aleatórios tooan Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3d54-127">hello `resources/writer.yaml` topology writes random data tooan Azure Event Hub.</span></span> <span data-ttu-id="e3d54-128">Olá dados são gerados por Olá `DeviceSpout` componente, e é uma ID de dispositivo aleatória e o valor do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="e3d54-128">hello data is generated by hello `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="e3d54-129">Dessa forma, ele está simulando um hardware que emite uma ID de cadeia de  caracteres e um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="e3d54-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="e3d54-130">Três `resources/reader.yaml` topologia lê dados de Hub de eventos (dados Olá gravados pelo EventHubWriter,) analisa os dados JSON Olá e, em seguida, registra Olá `deviceId` e `deviceValue` dados.</span><span class="sxs-lookup"><span data-stu-id="e3d54-130">Thee `resources/reader.yaml` topology reads data from Event Hub (hello data written by EventHubWriter,) parses hello JSON data, and then logs hello `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="e3d54-131">Olá dados estão formatados como um documento JSON antes de ser gravado tooEvent Hub e, em que é lido pelo leitor de saudação que é analisada de JSON e em tuplas.</span><span class="sxs-lookup"><span data-stu-id="e3d54-131">hello data is formatted as a JSON document before it is written tooEvent Hub, and when read by hello reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="e3d54-132">formato do Hello JSON é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e3d54-132">hello JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="e3d54-133">Configuração do projeto</span><span class="sxs-lookup"><span data-stu-id="e3d54-133">Project configuration</span></span>

<span data-ttu-id="e3d54-134">Olá `POM.xml` arquivo contém informações de configuração para este projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="e3d54-134">hello `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="e3d54-135">Olá interessantes são:</span><span class="sxs-lookup"><span data-stu-id="e3d54-135">hello interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="e3d54-136">Componentes do Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="e3d54-136">Event Hub components</span></span>

<span data-ttu-id="e3d54-137">componente de saudação que lê e grava tooAzure Hubs de eventos está localizado na Olá [HDInsight repositório](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="e3d54-137">hello component that reads and writes tooAzure Event Hubs is located in hello [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="e3d54-138">Olá seguintes seções Olá `POM.xml` arquivo carga Olá componentes deste repositório</span><span class="sxs-lookup"><span data-stu-id="e3d54-138">hello following sections in hello `POM.xml` file load hello components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a><span data-ttu-id="e3d54-139">Olá EventHubs Storm Spout dependência</span><span class="sxs-lookup"><span data-stu-id="e3d54-139">hello EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="e3d54-140">Esse xml define uma dependência para o pacote de eventhubs hello, que contém um spout para leitura dos Hubs de eventos e um raio de gravação tooit.</span><span class="sxs-lookup"><span data-stu-id="e3d54-140">This xml defines a dependency for hello eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing tooit.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="e3d54-141">Esse xml define a saída de toogenerate projeto Olá para Java 8, que é usado pelo HDInsight 3.5 ou superior.</span><span class="sxs-lookup"><span data-stu-id="e3d54-141">This xml configures hello project toogenerate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="hello-maven-shade-plugin"></a><span data-ttu-id="e3d54-142">Olá maven-tonalidade-plug-in</span><span class="sxs-lookup"><span data-stu-id="e3d54-142">hello maven-shade-plugin</span></span>

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

<span data-ttu-id="e3d54-143">Esse xml configura a saída de hello Olá solução toopackage em um jar grande.</span><span class="sxs-lookup"><span data-stu-id="e3d54-143">This xml configures hello solution toopackage hello output into an uber jar.</span></span> <span data-ttu-id="e3d54-144">jar Olá contém o código do projeto hello e dependências necessárias.</span><span class="sxs-lookup"><span data-stu-id="e3d54-144">hello jar contains both hello project code and required dependencies.</span></span> <span data-ttu-id="e3d54-145">Também é usado para:</span><span class="sxs-lookup"><span data-stu-id="e3d54-145">It is also used to:</span></span>

* <span data-ttu-id="e3d54-146">Renomear arquivos de licença para dependências de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d54-146">Rename license files for hello dependencies.</span></span>
* <span data-ttu-id="e3d54-147">Exclua a segurança/as assinaturas.</span><span class="sxs-lookup"><span data-stu-id="e3d54-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="e3d54-148">Certifique-se de que várias implementações de hello a mesma interface são mesclados em uma entrada.</span><span class="sxs-lookup"><span data-stu-id="e3d54-148">Ensure that multiple implementations of hello same interface are merged into one entry.</span></span>

<span data-ttu-id="e3d54-149">Essas definições de configuração evitam erros em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e3d54-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="e3d54-150">Definições de topologia</span><span class="sxs-lookup"><span data-stu-id="e3d54-150">Topology definitions</span></span>

<span data-ttu-id="e3d54-151">Este exemplo usa Olá [fluxo](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span><span class="sxs-lookup"><span data-stu-id="e3d54-151">This example uses hello [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="e3d54-152">Essa estrutura usa topologias de saudação toodefine YAML.</span><span class="sxs-lookup"><span data-stu-id="e3d54-152">This framework uses YAML toodefine hello topologies.</span></span> <span data-ttu-id="e3d54-153">Olá o principal benefício é que você não configurar a topologia de saudação em código Java.</span><span class="sxs-lookup"><span data-stu-id="e3d54-153">hello primary benefit is that you aren't hard coding hello topology in Java code.</span></span> <span data-ttu-id="e3d54-154">Como definição de saudação YAML, você pode alterá-la antes de enviar a topologia hello, sem ter que toorecompile tudo.</span><span class="sxs-lookup"><span data-stu-id="e3d54-154">Since hello definition is YAML, you can change it before submitting hello topology, without having toorecompile everything.</span></span>

<span data-ttu-id="e3d54-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="e3d54-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

<span data-ttu-id="e3d54-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="e3d54-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a><span data-ttu-id="e3d54-157">Conte-topologia Olá sobre Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="e3d54-157">Tell hello topology about Event Hub</span></span>

<span data-ttu-id="e3d54-158">Em tempo de execução, Olá `dev.properties` arquivo é usado toopass Olá Hub de eventos configuração toohello topologia.</span><span class="sxs-lookup"><span data-stu-id="e3d54-158">At run time, hello `dev.properties` file is used toopass hello Event Hub configuration toohello topology.</span></span> <span data-ttu-id="e3d54-159">Olá é um exemplo conteúdo de padrão de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="e3d54-159">hello following example is hello default contents of hello file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="e3d54-160">Configurar variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="e3d54-160">Configure environment variables</span></span>

<span data-ttu-id="e3d54-161">Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK em sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e3d54-161">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="e3d54-162">No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.</span><span class="sxs-lookup"><span data-stu-id="e3d54-162">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="e3d54-163">**JAVA_HOME** -deve apontar toohello diretório onde Olá o Java runtime environment (JRE) está instalado.</span><span class="sxs-lookup"><span data-stu-id="e3d54-163">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="e3d54-164">Por exemplo, em uma distribuição Unix ou Linux, ele deve ter um valor semelhante muito`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="e3d54-164">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="e3d54-165">No Windows, ele deve ter um valor semelhante muito`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="e3d54-165">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="e3d54-166">**CAMINHO** -deve conter Olá caminhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3d54-166">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="e3d54-167">**JAVA_HOME** (ou caminho equivalente Olá)</span><span class="sxs-lookup"><span data-stu-id="e3d54-167">**JAVA_HOME** (or hello equivalent path)</span></span>
  * <span data-ttu-id="e3d54-168">**JAVA_HOME\bin** (ou caminho equivalente Olá)</span><span class="sxs-lookup"><span data-stu-id="e3d54-168">**JAVA_HOME\bin** (or hello equivalent path)</span></span>
  * <span data-ttu-id="e3d54-169">diretório de saudação onde Maven está instalado</span><span class="sxs-lookup"><span data-stu-id="e3d54-169">hello directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="e3d54-170">Configurar o Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="e3d54-170">Configure Event Hub</span></span>

<span data-ttu-id="e3d54-171">Hubs de eventos é a fonte de dados de saudação para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="e3d54-171">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="e3d54-172">Use Olá etapas toocreate um Hub de eventos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e3d54-172">Use hello following steps toocreate a Event Hub.</span></span>

1. <span data-ttu-id="e3d54-173">De saudação [Portal clássico do Azure](https://manage.windowsazure.com), selecione **novo** > **Service Bus** > **Hub de eventos**  >  **Criação personalizada**.</span><span class="sxs-lookup"><span data-stu-id="e3d54-173">From hello [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="e3d54-174">Em Olá **adicionar um novo Hub de eventos** tela, insira um **nome do Hub de evento**.</span><span class="sxs-lookup"><span data-stu-id="e3d54-174">On hello **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="e3d54-175">Selecione Olá **região** toocreate Olá hub e, em seguida, criar um namespace ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="e3d54-175">Select hello **Region** toocreate hello hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="e3d54-176">Por fim, clique em Olá **seta** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="e3d54-176">Finally, click hello **Arrow** toocontinue.</span></span>

    ![página 1 do assistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="e3d54-178">Selecione Olá mesmo **local** como profusão de latência do HDInsight servidor tooreduce e os custos.</span><span class="sxs-lookup"><span data-stu-id="e3d54-178">Select hello same **Location** as your Storm on HDInsight server tooreduce latency and costs.</span></span>

3. <span data-ttu-id="e3d54-179">Em Olá **configurar Hub de eventos** tela, insira Olá **contagem de partição** e **retenção de mensagem** valores.</span><span class="sxs-lookup"><span data-stu-id="e3d54-179">On hello **Configure Event Hub** screen, enter hello **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="e3d54-180">Para este exemplo, use uma contagem de partições de 10 e uma retenção de mensagens de 1.</span><span class="sxs-lookup"><span data-stu-id="e3d54-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="e3d54-181">Observe a contagem de partição Olá porque esse valor é necessário mais tarde.</span><span class="sxs-lookup"><span data-stu-id="e3d54-181">Note hello partition count because you need this value later.</span></span>

    ![página 2 do assistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="e3d54-183">Depois que o hub de eventos de saudação tiver sido criado, marque Olá namespace, selecione **Hubs de eventos**e, em seguida, selecione o hub de eventos de saudação que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e3d54-183">After hello event hub has been created, select hello namespace, select **Event Hubs**, and then select hello event hub that you created earlier.</span></span>
5. <span data-ttu-id="e3d54-184">Selecione **configurar**, crie duas novas políticas de acesso usando Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3d54-184">Select **Configure**, then create two new access policies by using hello following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="e3d54-185">Nome</span><span class="sxs-lookup"><span data-stu-id="e3d54-185">Name</span></span></th><th><span data-ttu-id="e3d54-186">Permissões</span><span class="sxs-lookup"><span data-stu-id="e3d54-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="e3d54-187">Gravador</span><span class="sxs-lookup"><span data-stu-id="e3d54-187">Writer</span></span></td><td><span data-ttu-id="e3d54-188">Enviar</span><span class="sxs-lookup"><span data-stu-id="e3d54-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="e3d54-189">Leitor</span><span class="sxs-lookup"><span data-stu-id="e3d54-189">Reader</span></span></td><td><span data-ttu-id="e3d54-190">Escutar</span><span class="sxs-lookup"><span data-stu-id="e3d54-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="e3d54-191">Depois de criar permissões hello, selecione Olá **salvar** ícone final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="e3d54-191">After You create hello permissions, select hello **Save** icon at hello bottom of hello page.</span></span> <span data-ttu-id="e3d54-192">Essas políticas de acesso compartilhado são usada tooread e tooEvent Hub de gravação.</span><span class="sxs-lookup"><span data-stu-id="e3d54-192">These shared access policies are used tooread and write tooEvent Hub.</span></span>

    ![políticas](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="e3d54-194">Depois de salvar políticas hello, usar Olá **gerador de chave de acesso compartilhado** final Olá Olá página tooretrieve Olá chave Olá **gravador** e **leitor** políticas.</span><span class="sxs-lookup"><span data-stu-id="e3d54-194">After you save hello policies, use hello **Shared access key generator** at hello bottom of hello page tooretrieve hello key for hello **writer** and **reader** policies.</span></span> <span data-ttu-id="e3d54-195">Salve essas chaves.</span><span class="sxs-lookup"><span data-stu-id="e3d54-195">Save these keys.</span></span>

## <a name="download-and-build-hello-project"></a><span data-ttu-id="e3d54-196">Baixe e compilar o projeto de saudação</span><span class="sxs-lookup"><span data-stu-id="e3d54-196">Download and build hello project</span></span>

1. <span data-ttu-id="e3d54-197">Baixe o projeto de saudação do GitHub: [hdinsight-java storm eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="e3d54-197">Download hello project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="e3d54-198">Você pode baixar o pacote de saudação como um arquivo zip, ou usar [git](https://git-scm.com/) tooclone projeto de saudação localmente.</span><span class="sxs-lookup"><span data-stu-id="e3d54-198">You can either download hello package as a zip archive, or use [git](https://git-scm.com/) tooclone hello project locally.</span></span>

2. <span data-ttu-id="e3d54-199">Modificar Olá `dev.properties` arquivo de configuração de saudação para o Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="e3d54-199">Modify hello `dev.properties` file with hello configuration for your Event Hub.</span></span>

3. <span data-ttu-id="e3d54-200">Use Olá toobuild pacote hello projeto a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3d54-200">Use hello following toobuild and package hello project:</span></span>

        mvn package

    <span data-ttu-id="e3d54-201">Esse comando baixa dependências necessárias, compilações, e, em seguida, pacotes Olá projeto.</span><span class="sxs-lookup"><span data-stu-id="e3d54-201">This command downloads required dependencies, builds, and then packages hello project.</span></span> <span data-ttu-id="e3d54-202">Olá saída é armazenada no hello **/destino** diretório como **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="e3d54-202">hello output is stored in hello **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="e3d54-203">Testar localmente</span><span class="sxs-lookup"><span data-stu-id="e3d54-203">Test locally</span></span>

<span data-ttu-id="e3d54-204">Como essas topologias apenas ler e gravar tooEvent Hubs, você pode testá-las localmente, se você tiver um [ambiente de desenvolvimento Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="e3d54-204">Since these topologies just read and write tooEvent Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="e3d54-205">Use Olá toorun etapas localmente no ambiente de desenvolvimento Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3d54-205">Use hello following steps toorun locally in hello dev environment:</span></span>

1. <span data-ttu-id="e3d54-206">Execute o gravador de saudação:</span><span class="sxs-lookup"><span data-stu-id="e3d54-206">Run hello writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="e3d54-207">Execute o leitor hello:</span><span class="sxs-lookup"><span data-stu-id="e3d54-207">Run hello reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="e3d54-208">`--local`: Topologia de saudação executar em modo local (não distribuídas).</span><span class="sxs-lookup"><span data-stu-id="e3d54-208">`--local`: Run hello topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="e3d54-209">`-R /writer.yaml`: Carregar a definição de topologia de saudação do hello `resources` empacotados no jar hello.</span><span class="sxs-lookup"><span data-stu-id="e3d54-209">`-R /writer.yaml`: Load hello topology definition from hello `resources` packaged in hello jar.</span></span> <span data-ttu-id="e3d54-210">Se a topologia de saudação é um arquivo no sistema de arquivos local hello, especifique Olá caminho tooit como o último parâmetro de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d54-210">If hello topology is a file on hello local file system, specify hello path tooit as hello last parameter instead.</span></span>
> * <span data-ttu-id="e3d54-211">`--filter dev.properties`: Use o conteúdo de saudação do `dev.properties` toofill valores hello nas definições de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d54-211">`--filter dev.properties`: Use hello contents of `dev.properties` toofill in hello values in hello topology definitions.</span></span> <span data-ttu-id="e3d54-212">Por exemplo: `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="e3d54-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="e3d54-213">Saída é console toohello conectado ao executar localmente.</span><span class="sxs-lookup"><span data-stu-id="e3d54-213">Output is logged toohello console when running locally.</span></span> <span data-ttu-id="e3d54-214">Use __Ctrl + C__ toostop topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3d54-214">Use __Ctrl+C__ toostop hello topology.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="e3d54-215">Implantar topologias Olá</span><span class="sxs-lookup"><span data-stu-id="e3d54-215">Deploy hello topologies</span></span>

1. <span data-ttu-id="e3d54-216">Use SCP toocopy Olá jar pacote tooyour cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3d54-216">Use SCP toocopy hello jar package tooyour HDInsight cluster.</span></span> <span data-ttu-id="e3d54-217">Substitua o nome de usuário com o usuário SSH Olá para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e3d54-217">Replace USERNAME with hello SSH user for your cluster.</span></span> <span data-ttu-id="e3d54-218">Substitua CLUSTERNAME com nome de saudação do cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e3d54-218">Replace CLUSTERNAME with hello name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="e3d54-219">Se você usou uma senha para sua conta SSH, você é solicitadas tooenter Olá por senha.</span><span class="sxs-lookup"><span data-stu-id="e3d54-219">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="e3d54-220">Se você usou uma chave SSH com conta hello, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá caminho toohello arquivo de chave.</span><span class="sxs-lookup"><span data-stu-id="e3d54-220">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="e3d54-221">Por exemplo, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="e3d54-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="e3d54-222">Este comando copia a pasta base do hello arquivo toohello de usuário SSH no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e3d54-222">This command copies hello file toohello home directory of your SSH user on hello cluster.</span></span>

2. <span data-ttu-id="e3d54-223">Depois que o arquivo hello concluiu o carregamento, use SSH tooconnect toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="e3d54-223">Once hello file has finished uploading, use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="e3d54-224">Substituir **USERNAME** nome de saudação do seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="e3d54-224">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="e3d54-225">Substitua o **CLUSTERNAME** pelo nome do seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e3d54-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="e3d54-226">Se você usou uma senha para sua conta SSH, você é solicitadas tooenter Olá por senha.</span><span class="sxs-lookup"><span data-stu-id="e3d54-226">If you used a password for your SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="e3d54-227">Se você usou uma chave SSH com conta hello, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá caminho toohello arquivo de chave.</span><span class="sxs-lookup"><span data-stu-id="e3d54-227">If you used an SSH key with hello account, you may need toouse hello `-i` parameter toospecify hello path toohello key file.</span></span> <span data-ttu-id="e3d54-228">Olá, exemplo a seguir carrega a chave privada saudação do `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="e3d54-228">hello following example loads hello private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="e3d54-229">Use Olá topologias de saudação do toostart de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3d54-229">Use hello following command toostart hello topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="e3d54-230">`--remote`: Envia Olá topologia toohello serviço Nimbus, que inicia em nós de trabalho Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e3d54-230">`--remote`: Submits hello topology toohello Nimbus service, which starts it on hello worker nodes in hello cluster.</span></span>

4. <span data-ttu-id="e3d54-231">dados de saudação conectado tooview, vá toohttps://CLUSTERNAME.azurehdinsight.net/stormui, onde __CLUSTERNAME__ é o nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3d54-231">tooview hello logged data, go toohttps://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="e3d54-232">Selecione topologias hello e fazer drill down toohello componentes.</span><span class="sxs-lookup"><span data-stu-id="e3d54-232">Select hello topologies and drill down toohello components.</span></span> <span data-ttu-id="e3d54-233">Selecione Olá __porta__ entrada para uma instância de um componente tooview informações registradas em log.</span><span class="sxs-lookup"><span data-stu-id="e3d54-233">Select hello __port__ entry for an instance of a component tooview logged information.</span></span>

5. <span data-ttu-id="e3d54-234">Use Olá topologias de saudação toostop comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3d54-234">Use hello following commands toostop hello topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="e3d54-235">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="e3d54-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="e3d54-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3d54-236">Next steps</span></span>

* [<span data-ttu-id="e3d54-237">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3d54-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
