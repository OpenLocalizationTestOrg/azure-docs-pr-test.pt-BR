---
title: Processar eventos de Hubs de Eventos com o Storm no HDInsight usando o Java | Microsoft Docs
description: Saiba como processar dados de Hubs de Eventos com uma topologia Storm Java criada com o Maven.
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
ms.openlocfilehash: 2e8ebbdab2be7bed224a67facec798820615bb22
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a><span data-ttu-id="de4fe-103">Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="de4fe-103">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>

<span data-ttu-id="de4fe-104">Saiba como usar Hubs de Eventos do Azure com o Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de4fe-104">Learn how to use Azure Event Hubs with Storm on HDInsight.</span></span> <span data-ttu-id="de4fe-105">Este exemplo usa componentes baseados em Java para ler e gravar dados em Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="de4fe-105">This example uses Java-based components to read and write data in Azure Event Hubs.</span></span>

<span data-ttu-id="de4fe-106">Os Hubs de Eventos do Azure permitem processar grandes quantidades de dados de sites, aplicativos e dispositivos.</span><span class="sxs-lookup"><span data-stu-id="de4fe-106">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="de4fe-107">O spout de Hub de Eventos facilita o uso do Apache Storm no HDInsight para analisar esses dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="de4fe-107">The Event Hub spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span></span> <span data-ttu-id="de4fe-108">Você pode também gravar dados no Hub de Eventos usando o bolt dos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="de4fe-108">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de4fe-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="de4fe-109">Prerequisites</span></span>

* <span data-ttu-id="de4fe-110">Um Apache Storm no cluster HDInsight versão 3.6.</span><span class="sxs-lookup"><span data-stu-id="de4fe-110">An Apache Storm on HDInsight cluster version 3.6.</span></span> <span data-ttu-id="de4fe-111">Para obter mais informações, confira [Introdução ao Storm no cluster HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="de4fe-111">For more information, see [Get started with Storm on HDInsight cluster](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="de4fe-112">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="de4fe-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="de4fe-113">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="de4fe-113">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="de4fe-114">Um [Hub de Eventos do Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="de4fe-114">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="de4fe-115">[Oracle JDK (Java Developer Kit) versão 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou equivalente, por exemplo [OpenJDK](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="de4fe-115">[Oracle Java Developer Kit (JDK) version 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or equivalent, such as [OpenJDK](http://openjdk.java.net/).</span></span>

* <span data-ttu-id="de4fe-116">[Maven](https://maven.apache.org/download.cgi): o Maven é um sistema de criação de projetos para projetos Java.</span><span class="sxs-lookup"><span data-stu-id="de4fe-116">[Maven](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="de4fe-117">Um editor de texto ou um IDE (ambiente de desenvolvimento integrado).</span><span class="sxs-lookup"><span data-stu-id="de4fe-117">A text editor or integrated development environment (IDE).</span></span>

    > [!NOTE]
    > <span data-ttu-id="de4fe-118">Seu editor ou IDE pode ter uma funcionalidade específica para trabalhar com o Maven que não é abordada neste documento.</span><span class="sxs-lookup"><span data-stu-id="de4fe-118">Your editor or IDE may have specific functionality for working with Maven that is not addressed in this document.</span></span> <span data-ttu-id="de4fe-119">Para obter informações sobre os recursos do seu ambiente de edição, consulte a documentação do produto que você está usando.</span><span class="sxs-lookup"><span data-stu-id="de4fe-119">For information about the capabilities of your editing environment, see the documentation for the product you are using.</span></span>

    * <span data-ttu-id="de4fe-120">Um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="de4fe-120">An SSH client.</span></span> <span data-ttu-id="de4fe-121">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="de4fe-121">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="de4fe-122">Os comandos `ssh` e `scp`.</span><span class="sxs-lookup"><span data-stu-id="de4fe-122">The `ssh` and `scp` commands.</span></span> <span data-ttu-id="de4fe-123">Eles são usados para copiar arquivos para o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de4fe-123">These are used to copy files to the HDInsight cluster.</span></span> <span data-ttu-id="de4fe-124">No Windows, você pode obtê-los por meio do Bash no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="de4fe-124">On Windows, you can get these through Bash on Windows 10.</span></span>

## <a name="understanding-the-example"></a><span data-ttu-id="de4fe-125">Compreendendo o exemplo</span><span class="sxs-lookup"><span data-stu-id="de4fe-125">Understanding the example</span></span>

<span data-ttu-id="de4fe-126">O exemplo [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) contém duas topologias:</span><span class="sxs-lookup"><span data-stu-id="de4fe-126">The [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) example contains two topologies:</span></span>

<span data-ttu-id="de4fe-127">A topologia `resources/writer.yaml` grava dados aleatórios em um Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="de4fe-127">The `resources/writer.yaml` topology writes random data to an Azure Event Hub.</span></span> <span data-ttu-id="de4fe-128">Os dados são gerados pelo componente `DeviceSpout` e são um valor de dispositivo e ID de dispositivo aleatório.</span><span class="sxs-lookup"><span data-stu-id="de4fe-128">The data is generated by the `DeviceSpout` component, and is a random device ID and device value.</span></span> <span data-ttu-id="de4fe-129">Dessa forma, ele está simulando um hardware que emite uma ID de cadeia de  caracteres e um valor numérico.</span><span class="sxs-lookup"><span data-stu-id="de4fe-129">So it's simulating some hardware that emits a string ID and a numeric value.</span></span>

<span data-ttu-id="de4fe-130">A topologia do `resources/reader.yaml` lê dados do Hub de Eventos (os dados gravados pelo EventHubWriter,) analisa os dados JSON e, em seguida, registra os dados `deviceId` e `deviceValue`.</span><span class="sxs-lookup"><span data-stu-id="de4fe-130">Thee `resources/reader.yaml` topology reads data from Event Hub (the data written by EventHubWriter,) parses the JSON data, and then logs the `deviceId` and `deviceValue` data.</span></span>

<span data-ttu-id="de4fe-131">Os dados são formatados como um documento JSON antes de serem gravados no Hub de Eventos. Quando eles forem lidos pelo leitor, serão analisados pelo JSON em tuplas.</span><span class="sxs-lookup"><span data-stu-id="de4fe-131">The data is formatted as a JSON document before it is written to Event Hub, and when read by the reader it is parsed out of JSON and into tuples.</span></span> <span data-ttu-id="de4fe-132">O formato JSON é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="de4fe-132">The JSON format is as follows:</span></span>

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a><span data-ttu-id="de4fe-133">Configuração do projeto</span><span class="sxs-lookup"><span data-stu-id="de4fe-133">Project configuration</span></span>

<span data-ttu-id="de4fe-134">O arquivo `POM.xml` contém informações de configuração deste projeto Maven.</span><span class="sxs-lookup"><span data-stu-id="de4fe-134">The `POM.xml` file contains configuration information for this Maven project.</span></span> <span data-ttu-id="de4fe-135">As partes interessantes são:</span><span class="sxs-lookup"><span data-stu-id="de4fe-135">The interesting pieces are:</span></span>

#### <a name="event-hub-components"></a><span data-ttu-id="de4fe-136">Componentes do Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="de4fe-136">Event Hub components</span></span>

<span data-ttu-id="de4fe-137">O componente que lê e grava os Hubs de Eventos do Azure está localizado no [repositório do HDInsight](https://github.com/hdinsight/mvn-rep).</span><span class="sxs-lookup"><span data-stu-id="de4fe-137">The component that reads and writes to Azure Event Hubs is located in the [HDInsight repository](https://github.com/hdinsight/mvn-rep).</span></span> <span data-ttu-id="de4fe-138">As seguintes seções no arquivo `POM.xml` carregam os componentes desse repositório</span><span class="sxs-lookup"><span data-stu-id="de4fe-138">The following sections in the `POM.xml` file load the components from this repository</span></span>

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="the-eventhubs-storm-spout-dependency"></a><span data-ttu-id="de4fe-139">A dependência do Spout Storm dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="de4fe-139">The EventHubs Storm Spout dependency</span></span>

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

<span data-ttu-id="de4fe-140">Esse xml define uma dependência ao pacote eventhubs, que contém um spout para leitura dos Hubs de Eventos e um bolt para a gravação neles.</span><span class="sxs-lookup"><span data-stu-id="de4fe-140">This xml defines a dependency for the eventhubs package, which contains both a spout for reading from Event Hubs, and a bolt for writing to it.</span></span>

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

<span data-ttu-id="de4fe-141">Esse xml configura o projeto para gerar uma saída para Java 8, que é usada pelo HDInsight 3.5 ou superior.</span><span class="sxs-lookup"><span data-stu-id="de4fe-141">This xml configures the project to generate output for Java 8, which is used by HDInsight 3.5 or higher.</span></span>

#### <a name="the-maven-shade-plugin"></a><span data-ttu-id="de4fe-142">O maven-shade-plugin</span><span class="sxs-lookup"><span data-stu-id="de4fe-142">The maven-shade-plugin</span></span>

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

<span data-ttu-id="de4fe-143">Esse xml configura a solução para empacotar a saída em um uber jar.</span><span class="sxs-lookup"><span data-stu-id="de4fe-143">This xml configures the solution to package the output into an uber jar.</span></span> <span data-ttu-id="de4fe-144">O jar contém o código do projeto e as dependências necessárias.</span><span class="sxs-lookup"><span data-stu-id="de4fe-144">The jar contains both the project code and required dependencies.</span></span> <span data-ttu-id="de4fe-145">Também é usado para:</span><span class="sxs-lookup"><span data-stu-id="de4fe-145">It is also used to:</span></span>

* <span data-ttu-id="de4fe-146">Renomeie os arquivos de licença para as dependências.</span><span class="sxs-lookup"><span data-stu-id="de4fe-146">Rename license files for the dependencies.</span></span>
* <span data-ttu-id="de4fe-147">Exclua a segurança/as assinaturas.</span><span class="sxs-lookup"><span data-stu-id="de4fe-147">Exclude security/signatures.</span></span>
* <span data-ttu-id="de4fe-148">Verifique se as várias implementações da mesma interface estão mescladas em uma entrada.</span><span class="sxs-lookup"><span data-stu-id="de4fe-148">Ensure that multiple implementations of the same interface are merged into one entry.</span></span>

<span data-ttu-id="de4fe-149">Essas definições de configuração evitam erros em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="de4fe-149">These configuration settings prevent errors at runtime.</span></span>

#### <a name="topology-definitions"></a><span data-ttu-id="de4fe-150">Definições de topologia</span><span class="sxs-lookup"><span data-stu-id="de4fe-150">Topology definitions</span></span>

<span data-ttu-id="de4fe-151">Este exemplo usa a estrutura [Fluxo](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="de4fe-151">This example uses the [Flux](https://storm.apache.org/releases/1.1.0/flux.html) framework.</span></span> <span data-ttu-id="de4fe-152">Essa estrutura usa YAML para definir as topologias.</span><span class="sxs-lookup"><span data-stu-id="de4fe-152">This framework uses YAML to define the topologies.</span></span> <span data-ttu-id="de4fe-153">O principal benefício é que você não embute a topologia em código Java.</span><span class="sxs-lookup"><span data-stu-id="de4fe-153">The primary benefit is that you aren't hard coding the topology in Java code.</span></span> <span data-ttu-id="de4fe-154">Como a definição é YAML, você pode alterá-la antes de enviar a topologia sem precisar recompilar tudo.</span><span class="sxs-lookup"><span data-stu-id="de4fe-154">Since the definition is YAML, you can change it before submitting the topology, without having to recompile everything.</span></span>

<span data-ttu-id="de4fe-155">__writer.yaml__:</span><span class="sxs-lookup"><span data-stu-id="de4fe-155">__writer.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure the Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through the components
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

<span data-ttu-id="de4fe-156">__reader.yaml__:</span><span class="sxs-lookup"><span data-stu-id="de4fe-156">__reader.yaml__:</span></span>

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure the Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from the .properties file when the topology is started
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
    # parallelism hint. This should be the same as the number of partitions for your Event Hub, so we read it from the dev.properties file passed at run time.
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

# How data flows through the components
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

#### <a name="tell-the-topology-about-event-hub"></a><span data-ttu-id="de4fe-157">Informar a topologia sobre o Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="de4fe-157">Tell the topology about Event Hub</span></span>

<span data-ttu-id="de4fe-158">No tempo de execução, o arquivo `dev.properties` é usado para passar a configuração de Hub de Eventos à topologia.</span><span class="sxs-lookup"><span data-stu-id="de4fe-158">At run time, the `dev.properties` file is used to pass the Event Hub configuration to the topology.</span></span> <span data-ttu-id="de4fe-159">O exemplo a seguir é o conteúdo padrão do arquivo:</span><span class="sxs-lookup"><span data-stu-id="de4fe-159">The following example is the default contents of the file:</span></span>

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a><span data-ttu-id="de4fe-160">Configurar variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="de4fe-160">Configure environment variables</span></span>

<span data-ttu-id="de4fe-161">As seguintes variáveis de ambiente podem ser definidas quando você instala o Java e o JDK em sua estação de trabalho de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="de4fe-161">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="de4fe-162">No entanto, você deve verificar se elas existem e se contêm os valores corretos para o seu sistema.</span><span class="sxs-lookup"><span data-stu-id="de4fe-162">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="de4fe-163">**JAVA_HOME** - deve apontar para o diretório onde o JRE (Java runtime environment) está instalado.</span><span class="sxs-lookup"><span data-stu-id="de4fe-163">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="de4fe-164">Por exemplo, em uma distribuição Unix ou Linux, ele deve ter um valor semelhante a `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="de4fe-164">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="de4fe-165">No Windows, ele teria um valor semelhante a `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="de4fe-165">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>
* <span data-ttu-id="de4fe-166">**PATH** - deve conter os seguintes caminhos:</span><span class="sxs-lookup"><span data-stu-id="de4fe-166">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="de4fe-167">**JAVA_HOME** (ou o caminho equivalente)</span><span class="sxs-lookup"><span data-stu-id="de4fe-167">**JAVA_HOME** (or the equivalent path)</span></span>
  * <span data-ttu-id="de4fe-168">**JAVA_HOME\bin** (ou o caminho equivalente)</span><span class="sxs-lookup"><span data-stu-id="de4fe-168">**JAVA_HOME\bin** (or the equivalent path)</span></span>
  * <span data-ttu-id="de4fe-169">O diretório onde o Maven está instalado</span><span class="sxs-lookup"><span data-stu-id="de4fe-169">The directory where Maven is installed</span></span>

## <a name="configure-event-hub"></a><span data-ttu-id="de4fe-170">Configurar o Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="de4fe-170">Configure Event Hub</span></span>

<span data-ttu-id="de4fe-171">Hubs de Eventos é a fonte de dados para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="de4fe-171">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="de4fe-172">Use as etapas a seguir para criar um novo hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="de4fe-172">Use the following steps to create a Event Hub.</span></span>

1. <span data-ttu-id="de4fe-173">No [Portal Clássico do Azure](https://manage.windowsazure.com), selecione **NOVO** > **Barramento de Serviço** > **Hub de Eventos** > **Criação Personalizada**.</span><span class="sxs-lookup"><span data-stu-id="de4fe-173">From the [Azure Classic Portal](https://manage.windowsazure.com), select **NEW** > **Service Bus** > **Event Hub** > **Custom Create**.</span></span>

2. <span data-ttu-id="de4fe-174">Na tela **Adicionar um novo Hub de Eventos**, insira um **Nome do Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="de4fe-174">On the **Add a new Event Hub** screen, enter an **Event Hub Name**.</span></span> <span data-ttu-id="de4fe-175">Selecione a **Região** para criar o hub e, em seguida, crie um namespace ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="de4fe-175">Select the **Region** to create the hub in, and then create a namespace or select an existing one.</span></span> <span data-ttu-id="de4fe-176">Por fim, clique na **Seta** para continuar.</span><span class="sxs-lookup"><span data-stu-id="de4fe-176">Finally, click the **Arrow** to continue.</span></span>

    ![página 1 do assistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > <span data-ttu-id="de4fe-178">Selecione o mesmo **Local** do seu Storm no servidor HDInsight para reduzir a latência e os custos.</span><span class="sxs-lookup"><span data-stu-id="de4fe-178">Select the same **Location** as your Storm on HDInsight server to reduce latency and costs.</span></span>

3. <span data-ttu-id="de4fe-179">Na tela **Configurar o Hub de Eventos**, insira os valores de **Contagem de partições** e **Retenção de Mensagem**.</span><span class="sxs-lookup"><span data-stu-id="de4fe-179">On the **Configure Event Hub** screen, enter the **Partition count** and **Message Retention** values.</span></span> <span data-ttu-id="de4fe-180">Para este exemplo, use uma contagem de partições de 10 e uma retenção de mensagens de 1.</span><span class="sxs-lookup"><span data-stu-id="de4fe-180">For this example, use a partition count of 10 and a message retention of 1.</span></span> <span data-ttu-id="de4fe-181">Anote a contagem de partições, pois você precisará desse valor posteriormente.</span><span class="sxs-lookup"><span data-stu-id="de4fe-181">Note the partition count because you need this value later.</span></span>

    ![página 2 do assistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. <span data-ttu-id="de4fe-183">Depois que o hub de eventos tiver sido criado, selecione o namespace, selecione **Hubs de Eventos**e, em seguida, selecione o hub de eventos criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="de4fe-183">After the event hub has been created, select the namespace, select **Event Hubs**, and then select the event hub that you created earlier.</span></span>
5. <span data-ttu-id="de4fe-184">Selecione **Configurar**e crie duas novas políticas de acesso usando as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="de4fe-184">Select **Configure**, then create two new access policies by using the following information:</span></span>

    <table>
    <tr><th><span data-ttu-id="de4fe-185">Nome</span><span class="sxs-lookup"><span data-stu-id="de4fe-185">Name</span></span></th><th><span data-ttu-id="de4fe-186">Permissões</span><span class="sxs-lookup"><span data-stu-id="de4fe-186">Permissions</span></span></th></tr>
    <tr><td><span data-ttu-id="de4fe-187">Gravador</span><span class="sxs-lookup"><span data-stu-id="de4fe-187">Writer</span></span></td><td><span data-ttu-id="de4fe-188">Enviar</span><span class="sxs-lookup"><span data-stu-id="de4fe-188">Send</span></span></td></tr>
    <tr><td><span data-ttu-id="de4fe-189">Leitor</span><span class="sxs-lookup"><span data-stu-id="de4fe-189">Reader</span></span></td><td><span data-ttu-id="de4fe-190">Escutar</span><span class="sxs-lookup"><span data-stu-id="de4fe-190">Listen</span></span></td></tr>
    </table>

    <span data-ttu-id="de4fe-191">Depois de criar permissões, selecione o ícone **Salvar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="de4fe-191">After You create the permissions, select the **Save** icon at the bottom of the page.</span></span> <span data-ttu-id="de4fe-192">Essas políticas de acesso compartilhado são usadas para ler e gravar no Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="de4fe-192">These shared access policies are used to read and write to Event Hub.</span></span>

    ![políticas](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. <span data-ttu-id="de4fe-194">Depois de salvar as políticas, use o **Gerador de chave de acesso compartilhada** na parte inferior da página para recuperar a chave para as políticas **gravador** e **leitor**.</span><span class="sxs-lookup"><span data-stu-id="de4fe-194">After you save the policies, use the **Shared access key generator** at the bottom of the page to retrieve the key for the **writer** and **reader** policies.</span></span> <span data-ttu-id="de4fe-195">Salve essas chaves.</span><span class="sxs-lookup"><span data-stu-id="de4fe-195">Save these keys.</span></span>

## <a name="download-and-build-the-project"></a><span data-ttu-id="de4fe-196">Baixar e compilar o projeto</span><span class="sxs-lookup"><span data-stu-id="de4fe-196">Download and build the project</span></span>

1. <span data-ttu-id="de4fe-197">Baixe o projeto do GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="de4fe-197">Download the project from GitHub: [hdinsight-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub).</span></span> <span data-ttu-id="de4fe-198">Você pode baixar o pacote como um arquivo zip, ou usar o [git](https://git-scm.com/) para clonar o projeto localmente.</span><span class="sxs-lookup"><span data-stu-id="de4fe-198">You can either download the package as a zip archive, or use [git](https://git-scm.com/) to clone the project locally.</span></span>

2. <span data-ttu-id="de4fe-199">Modifique o arquivo `dev.properties` com a configuração para o Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="de4fe-199">Modify the `dev.properties` file with the configuration for your Event Hub.</span></span>

3. <span data-ttu-id="de4fe-200">Use o seguinte para criar e empacotar o projeto:</span><span class="sxs-lookup"><span data-stu-id="de4fe-200">Use the following to build and package the project:</span></span>

        mvn package

    <span data-ttu-id="de4fe-201">Esse comando baixa as dependências exigidas, as compila e então empacota o projeto.</span><span class="sxs-lookup"><span data-stu-id="de4fe-201">This command downloads required dependencies, builds, and then packages the project.</span></span> <span data-ttu-id="de4fe-202">A saída é armazenada no diretório **/target** como **EventHubExample-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="de4fe-202">The output is stored in the **/target** directory as **EventHubExample-1.0-SNAPSHOT.jar**.</span></span>

## <a name="test-locally"></a><span data-ttu-id="de4fe-203">Testar localmente</span><span class="sxs-lookup"><span data-stu-id="de4fe-203">Test locally</span></span>

<span data-ttu-id="de4fe-204">Uma vez que essas topologias somente leem e gravam em Hubs de Eventos, você poderá testá-las localmente se tiver um [ambiente de desenvolvimento do Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span><span class="sxs-lookup"><span data-stu-id="de4fe-204">Since these topologies just read and write to Event Hubs, you can test them locally if you have a [Storm development environment](http://storm.apache.org/releases/current/Setting-up-development-environment.html).</span></span> <span data-ttu-id="de4fe-205">Use as etapas a seguir execução local no ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="de4fe-205">Use the following steps to run locally in the dev environment:</span></span>

1. <span data-ttu-id="de4fe-206">Execute o gravador:</span><span class="sxs-lookup"><span data-stu-id="de4fe-206">Run the writer:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. <span data-ttu-id="de4fe-207">Execute o leitor:</span><span class="sxs-lookup"><span data-stu-id="de4fe-207">Run the reader:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * <span data-ttu-id="de4fe-208">`--local`: execute a topologia em modo local (não distribuído).</span><span class="sxs-lookup"><span data-stu-id="de4fe-208">`--local`: Run the topology in local mode (non-distributed).</span></span>
> * <span data-ttu-id="de4fe-209">`-R /writer.yaml`: carregue a definição de topologia do `resources` empacotada no jar.</span><span class="sxs-lookup"><span data-stu-id="de4fe-209">`-R /writer.yaml`: Load the topology definition from the `resources` packaged in the jar.</span></span> <span data-ttu-id="de4fe-210">Se a topologia for um arquivo no sistema de arquivos local, especifique o caminho para ela como o último parâmetro.</span><span class="sxs-lookup"><span data-stu-id="de4fe-210">If the topology is a file on the local file system, specify the path to it as the last parameter instead.</span></span>
> * <span data-ttu-id="de4fe-211">`--filter dev.properties`: use o conteúdo de `dev.properties` para preencher os valores nas definições de topologia.</span><span class="sxs-lookup"><span data-stu-id="de4fe-211">`--filter dev.properties`: Use the contents of `dev.properties` to fill in the values in the topology definitions.</span></span> <span data-ttu-id="de4fe-212">Por exemplo: `${eventhub.read.policy.name}`.</span><span class="sxs-lookup"><span data-stu-id="de4fe-212">For example, `${eventhub.read.policy.name}`.</span></span>

<span data-ttu-id="de4fe-213">A saída é registrada no console quando ao executar localmente.</span><span class="sxs-lookup"><span data-stu-id="de4fe-213">Output is logged to the console when running locally.</span></span> <span data-ttu-id="de4fe-214">Use __Ctrl+C__ para interromper a topologia.</span><span class="sxs-lookup"><span data-stu-id="de4fe-214">Use __Ctrl+C__ to stop the topology.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="de4fe-215">Implantar as topologias</span><span class="sxs-lookup"><span data-stu-id="de4fe-215">Deploy the topologies</span></span>

1. <span data-ttu-id="de4fe-216">Use o SCP para copiar o pacote jar para seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de4fe-216">Use SCP to copy the jar package to your HDInsight cluster.</span></span> <span data-ttu-id="de4fe-217">Substitua USERNAME pelo usuário SSH para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="de4fe-217">Replace USERNAME with the SSH user for your cluster.</span></span> <span data-ttu-id="de4fe-218">Substitua CLUSTERNAME pelo nome do seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="de4fe-218">Replace CLUSTERNAME with the name of your HDInsight cluster:</span></span>

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    <span data-ttu-id="de4fe-219">Se você tiver usado uma senha para sua conta SSH, será necessário inserir a senha.</span><span class="sxs-lookup"><span data-stu-id="de4fe-219">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="de4fe-220">Se você tiver usado uma chave SSH com a conta, talvez seja necessário usar o parâmetro `-i` para especificar o caminho para o arquivo de chave.</span><span class="sxs-lookup"><span data-stu-id="de4fe-220">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="de4fe-221">Por exemplo, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span><span class="sxs-lookup"><span data-stu-id="de4fe-221">For example, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`</span></span>

    <span data-ttu-id="de4fe-222">Esse comando copia o arquivo para o diretório base do usuário SSH no cluster.</span><span class="sxs-lookup"><span data-stu-id="de4fe-222">This command copies the file to the home directory of your SSH user on the cluster.</span></span>

2. <span data-ttu-id="de4fe-223">Após a conclusão do carregamento do arquivo, use o SSH para se conectar ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de4fe-223">Once the file has finished uploading, use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="de4fe-224">Substitua o **USERNAME** pelo nome do seu logon SSH.</span><span class="sxs-lookup"><span data-stu-id="de4fe-224">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="de4fe-225">Substitua o **CLUSTERNAME** pelo nome do seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="de4fe-225">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > <span data-ttu-id="de4fe-226">Se você tiver usado uma senha para sua conta SSH, será necessário inserir a senha.</span><span class="sxs-lookup"><span data-stu-id="de4fe-226">If you used a password for your SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="de4fe-227">Se você tiver usado uma chave SSH com a conta, talvez seja necessário usar o parâmetro `-i` para especificar o caminho para o arquivo de chave.</span><span class="sxs-lookup"><span data-stu-id="de4fe-227">If you used an SSH key with the account, you may need to use the `-i` parameter to specify the path to the key file.</span></span> <span data-ttu-id="de4fe-228">O exemplo a seguir carregará a chave privada de `~/.ssh/id_rsa`:</span><span class="sxs-lookup"><span data-stu-id="de4fe-228">The following example loads the private key from `~/.ssh/id_rsa`:</span></span>
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. <span data-ttu-id="de4fe-229">Use o comando a seguir para iniciar as topologias:</span><span class="sxs-lookup"><span data-stu-id="de4fe-229">Use the following command to start the topologies:</span></span>

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * <span data-ttu-id="de4fe-230">`--remote`: envia a topologia para o serviço Nimbus, que inicia nos nós de trabalho no cluster.</span><span class="sxs-lookup"><span data-stu-id="de4fe-230">`--remote`: Submits the topology to the Nimbus service, which starts it on the worker nodes in the cluster.</span></span>

4. <span data-ttu-id="de4fe-231">Para exibir os dados registrados, vá para https://CLUSTERNAME.azurehdinsight.net/stormui, em que __CLUSTERNAME__ é o nome do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de4fe-231">To view the logged data, go to https://CLUSTERNAME.azurehdinsight.net/stormui, where __CLUSTERNAME__ is the name of your HDInsight cluster.</span></span> <span data-ttu-id="de4fe-232">Selecione as topologias e faça drill down até os componentes.</span><span class="sxs-lookup"><span data-stu-id="de4fe-232">Select the topologies and drill down to the components.</span></span> <span data-ttu-id="de4fe-233">Selecione a entrada __porta__ para uma instância de um componente para exibir informações registradas.</span><span class="sxs-lookup"><span data-stu-id="de4fe-233">Select the __port__ entry for an instance of a component to view logged information.</span></span>

5. <span data-ttu-id="de4fe-234">Use os comandos a seguir para parar as topologias:</span><span class="sxs-lookup"><span data-stu-id="de4fe-234">Use the following commands to stop the topologies:</span></span>

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a><span data-ttu-id="de4fe-235">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="de4fe-235">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="de4fe-236">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="de4fe-236">Next steps</span></span>

* [<span data-ttu-id="de4fe-237">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="de4fe-237">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
