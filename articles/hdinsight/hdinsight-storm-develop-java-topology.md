---
title: aaaApache Storm exemplo de topologia de Java - HDInsight do Azure | Microsoft Docs
description: Saiba como topologias do Apache Storm toocreate em Java, criando uma palavra de exemplo contagem de topologia.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: apache storm, exemplo de apache storm, storm java, exemplo de topologia storm
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a>Criar uma topologia Apache Storm em Java

Saiba como toocreate uma topologia em Java para o Apache Storm. Crie uma topologia Storm que implementa um aplicativo de contagem de palavras. Use o Maven toobuild e pacote de saudação do projeto. Em seguida, você aprenderá como toodefine Olá topologia usando Olá framework de fluxo.

> [!NOTE]
> estrutura do fluxo de saudação está disponível no Storm 0.10.0 ou posterior. O Storm 0.10.0 está disponível com o HDInsight 3.3 e 3.4.

Depois de concluir as etapas de saudação neste documento, você pode implantar Olá topologia tooApache Storm no HDInsight.

> [!NOTE]
> Uma versão completa do exemplos de topologia Storm Olá criado neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).

## <a name="prerequisites"></a>Pré-requisitos

* [Java Developer Kit (JDK) versão 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* [Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven é um sistema de compilação do projeto para projetos Java.

* Um editor de texto ou IDE.

## <a name="configure-environment-variables"></a>Configurar variáveis de ambiente

Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK. No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.

* **JAVA_HOME** -deve apontar toohello diretório onde Olá o Java runtime environment (JRE) está instalado. Por exemplo, em uma distribuição Unix ou Linux, ele deve ter um valor semelhante muito`/usr/lib/jvm/java-7-oracle`. No Windows, ele deve ter um valor semelhante muito`c:\Program Files (x86)\Java\jre1.7`

* **CAMINHO** -deve conter Olá caminhos a seguir:

  * **JAVA_HOME** (ou caminho equivalente Olá)

  * **JAVA_HOME\bin** (ou caminho equivalente Olá)

  * diretório de saudação onde Maven está instalado

## <a name="create-a-maven-project"></a>Criar um projeto Maven

Na linha de comando hello, use Olá comando a seguir toocreate um projeto Maven chamado **WordCount**:

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> Se você estiver usando o PowerShell, coloque os parâmetros `-D` com aspas duplas.
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

Este comando cria um diretório chamado `WordCount` no local atual do hello, que contém um projeto Maven básico. Olá `WordCount` diretório contém Olá itens a seguir:

* `pom.xml`: Contém configurações para o projeto Maven hello.
* `src\main\java\com\microsoft\example`: contém o código do aplicativo.
* `src\test\java\com\microsoft\example`: contém testes para o seu aplicativo. 

### <a name="remove-hello-generated-example-code"></a>Remover o código de exemplo hello gerado

Exclua arquivos de aplicativo de hello e teste Olá gerado:

* **src\test\java\com\microsoft\example\AppTest.java**
* **src\main\java\com\microsoft\example\App.java**

## <a name="add-maven-repositories"></a>Adicionar repositórios Maven

HDInsight é baseado nos Olá HDP Hortonworks Data Platform (), portanto, é recomendável usar as dependências do hello Hortonworks repositório toodownload para seus projetos do Apache Storm. Em Olá __pom.xml__ de arquivo, adicione Olá XML a seguir após Olá `<url>http://maven.apache.org</url>` linha:

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a>Adicionar propriedades

Maven permite valores de nível de projeto toodefine chamados de propriedades. Em Olá __pom.xml__, adicionar Olá após o texto após Olá `</repositories>` linha:

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

Agora você pode usar esse valor em outras seções Olá `pom.xml`. Por exemplo, ao especificar versão Olá componentes Storm, você pode usar `${storm.version}` em vez de um valor de codificação.

## <a name="add-dependencies"></a>Adicionar dependências

Adicione uma dependência para componentes do Storm. Olá abrir `pom.xml` de arquivos e adicionar Olá Olá código a seguir `<dependencies>` seção:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

Em tempo de compilação, Maven usa esse toolook informações `storm-core` no repositório de Maven hello. Parece primeiro repositório Olá no computador local. Se os arquivos de saudação não existe, Maven baixa os arquivos de Repositório Maven público de saudação e os armazena no repositório local hello.

> [!NOTE]
> Saudação de aviso `<scope>provided</scope>` linha nesta seção. Essa configuração informa Maven tooexclude **storm core** de todos os arquivos JAR que são criados, porque ele é fornecido pelo sistema hello.

## <a name="build-configuration"></a>Configuração de compilação

Maven plug-ins permitem fases de compilação Olá toocustomize do projeto de saudação. Por exemplo, como o projeto de saudação é compilado ou como toopackage-lo em um arquivo JAR. Olá abrir `pom.xml` de arquivos e adicionar Olá seguindo o código diretamente acima Olá `</project>` linha.

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

Esta seção é usado tooadd plug-ins, recursos e outras opções de configuração de compilação. Para obter uma referência completa de saudação **pom.xml** de arquivos, consulte [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).

### <a name="add-plug-ins"></a>Adicionar plug-ins

Para obter topologias Apache Storm implementadas em Java, Olá [plug-in do Exec Maven](http://www.mojohaus.org/exec-maven-plugin/) é útil porque permite tooeasily executar topologia Olá localmente no seu ambiente de desenvolvimento. Adicionar Olá após toohello `<plugins>` seção Olá `pom.xml` tooinclude Olá Exec Maven plugin do arquivo:

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

Útil outro plug-in é hello [plug-in do Apache Maven compilador](http://maven.apache.org/plugins/maven-compiler-plugin/), que é usado toochange opções de compilação. alterações de Olá Olá versão do Java que usa Maven para origem de saudação e de destino para o seu aplicativo.

* Para HDInsight __3.4 ou anteriores__, definir a origem da saudação e too__1.7__ de versão do Java de destino.

* Para HDInsight __3.5__, definir a origem da saudação e too__1.8__ de versão do Java de destino.

Adicionar Olá depois do texto de saudação `<plugins>` seção Olá `pom.xml` tooinclude Olá Apache Maven compilador plugin do arquivo. Este exemplo especifica 1.8, para a versão do HDInsight de destino Olá é 3.5.

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a>Configurar recursos

Olá seção de recursos permite que você tooinclude recursos de código não como arquivos de configuração necessários pelos componentes na topologia de saudação. Neste exemplo, adicionar Olá depois do texto de saudação `<resources>` seção Olá ' pom.xml arquivo.

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

Este exemplo adiciona o diretório de recursos de saudação na raiz de saudação do projeto da saudação (`${basedir}`) como um local que contém recursos e inclui o arquivo hello chamado `log4j2.xml`. Esse arquivo é usado tooconfigure quais informações são registradas pelo topologia hello.

## <a name="create-hello-topology"></a>Criar topologia Olá

Uma topologia Apache Storm baseada em Java consiste em três componentes que você deve criar (ou referenciar) como uma dependência.

* **Spouts**: Leituras de fontes de dados externos e emite os fluxos de dados na topologia de saudação.

* **Bolts**: executa processamento em fluxos emitidos por spouts ou outros bolts e emite um ou mais fluxos.

* **Topologia**: define como Olá spouts e parafusos são organizados e fornece o ponto de entrada hello para a topologia de saudação.

### <a name="create-hello-spout"></a>Criar spout Olá

requisitos de tooreduce para configurar fontes de dados externas, Olá após spout simplesmente emite sentenças aleatórias. É uma versão modificada de um spout que é fornecido com hello [exemplos Storm Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).

> [!NOTE]
> Para obter um exemplo de um spout que lê a partir de uma fonte de dados externa, consulte um dos Olá exemplos a seguir:
>
> * [TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): um spout de exemplo que lê do Twitter
> * [Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): um spout que lê do Kafka

Para spout hello, crie um arquivo chamado `RandomSentenceSpout.java` em Olá `src\main\java\com\microsoft\example` Olá diretório e usar código Java a seguir como conteúdo hello:

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> Embora essa topologia usa apenas um spout, outros podem ter vários que feed de dados de origens diferentes em topologia hello.

### <a name="create-hello-bolts"></a>Criar hello parafusos

Parafusos tratar Olá processamento de dados. Essa topologia usa dois bolts:

* **SplitSentence**: divide sentenças Olá emitidas pelo **RandomSentenceSpout** em palavras individuais.

* **WordCount**: conta quantas vezes cada palavra ocorreu.

> [!NOTE]
> Parafusos podem fazer qualquer coisa, por exemplo, computação, persistência ou falando tooexternal componentes.

Crie dois novos arquivos, `SplitSentence.java` e `WordCount.java` em Olá `src\main\java\com\microsoft\example` directory. Use Olá depois do texto como conteúdo Olá para arquivos de saudação:

#### <a name="splitsentence"></a>SplitSentence

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a>WordCount

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-hello-topology"></a>Definir a topologia de saudação

topologia de saudação vincula Olá spouts e bolts juntos em um gráfico, que define como os dados fluem entre os componentes de saudação. Ele também fornece dicas de paralelismo Storm usa ao criar instâncias de componentes de saudação no cluster hello.

Olá imagem a seguir é um diagrama básico do gráfico de saudação de componentes para esta topologia.

![saudação de exibição de diagrama spouts e bolts organização](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

tooimplement Olá topologia, crie um arquivo chamado `WordCountTopology.java` em Olá `src\main\java\com\microsoft\example` directory. Saudação de usar código Java a seguir como conteúdo de saudação do arquivo hello:

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a>Configurar o registro em log

Tempestade usa Apache Log4j toolog informações. Se você não configurar o registro em log, a topologia de saudação emite informações de diagnóstico. toocontrol que é registrado em log, crie um arquivo chamado `log4j2.xml` em Olá `resources` directory. Use Olá XML a seguir como conteúdo de saudação do arquivo hello.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

Esse XML configura um novo agente para Olá `com.microsoft.example` classe, que inclui componentes de saudação nessa topologia de exemplo. nível de saudação é definido tootrace para esse agente, que captura qualquer informação de registro em log emitida pelos componentes nesta topologia.

Olá `<Root level="error">` seção configura o nível de raiz de saudação do log (tudo o que não está em `com.microsoft.example`) tooonly informações de erro de log.

Para saber mais sobre como configurar o registro em log para Log4j, confira [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).

> [!NOTE]
> Storm versão 0.10.0 e superior usa Log4j 2.x. Versões mais antigas do storm usavam Log4j 1.x, que usava um formato diferente para a configuração de log. Para obter informações sobre a configuração anterior hello, consulte [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).

## <a name="test-hello-topology-locally"></a>Topologia de saudação do teste localmente

Depois de salvar arquivos hello, use Olá comando tootest Olá topologia do local a seguir.

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

Como ele é executado, topologia Olá exibe informações de inicialização. Olá, texto a seguir é um exemplo de saída de contagem de palavras hello:

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

Esse log de exemplo indica que o word Olá ' e ' 113 vezes foi emitido. Olá contagem continuar toogo backup como topologia Olá executa porque spout Olá continuamente emite Olá mesmo sentenças.

Há um intervalo de cinco segundos entre a emissão de palavras e as contagens. Olá **WordCount** componente está configurado tooonly emitir informações quando chega uma tupla de escala. Ele solicita que as tuplas de escala sejam entregues somente a cada cinco segundos.

## <a name="convert-hello-topology-tooflux"></a>Converter Olá topologia tooFlux

Fluxo é uma nova estrutura disponível com Storm 0.10.0 e superior, que permite a configuração tooseparate da implementação. Os componentes ainda são definidos em Java, mas a topologia de saudação é definida usando um arquivo YAML. Você pode empacotar uma definição de topologia padrão com o seu projeto, ou usar um arquivo autônomo ao enviar a topologia de saudação. Ao enviar Olá topologia tooStorm, você pode usar variáveis de ambiente ou valores de toopopulate de arquivos de configuração Olá definição de topologia YAML.

arquivo YAML de saudação define Olá componentes toouse topologia hello e saudação de fluxo de dados entre eles. Você pode incluir um arquivo YAML como parte do arquivo jar do hello, ou você pode usar um arquivo YAML externo.

Para saber mais sobre o Flux, veja [Estrutura do Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

> [!WARNING]
> Vencimento tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) com Storm 1.0.1, talvez seja necessário tooinstall um [ambiente de desenvolvimento Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun localmente topologias de fluxo.

1. Mover Olá `WordCountTopology.java` arquivo fora do projeto de saudação. Anteriormente, esse arquivo definido topologia hello, mas não é necessária com o fluxo.

2. Em Olá `resources` diretório, crie um arquivo chamado `topology.yaml`. Use Olá depois do texto como o conteúdo deste arquivo hello.

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. Verifique Olá toohello alterações a seguir `pom.xml` arquivo.
   
   * Adicionar Olá após nova dependência no hello `<dependencies>` seção:
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * Adicionar Olá seguindo o plug-in toohello `<plugins>` seção. Este plug-in lida com a criação de um pacote (arquivo jar) Olá para projeto de saudação e aplica alguns tooFlux de transformações específicas ao criar o pacote de saudação.
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer tooit as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
                    </transformer>
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

   * Em Olá **exec de plugin maven** `<configuration>` seção, altere o valor de saudação para `<mainClass>` muito`org.apache.storm.flux.Flux`. Essa configuração permite que o fluxo toohandle executando topologia Olá localmente em desenvolvimento.

   * Em Olá `<resources>` seção, adicione Olá após toohello `<includes>`. Esse XML inclui arquivo YAML Olá que define a topologia de saudação como parte do projeto de saudação.

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a>Topologia de fluxo de saudação teste localmente

1. Use Olá toocompile a seguir e execute a topologia de fluxo hello usando Maven:

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    Se você estiver usando o PowerShell, use Olá comando a seguir:

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > Se a topologia usar bits do Storm 1.0.1, esse comando falhará. Essa falha é causada por [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055). Em vez disso, [instalar Storm em seu ambiente de desenvolvimento](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) e use Olá informações a seguir.

    Se você tiver [instalado Storm em seu ambiente de desenvolvimento](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), você pode usar o hello comandos a seguir em vez disso:

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    Olá `--local` parâmetro executa topologia Olá em modo local no seu ambiente de desenvolvimento. Olá `-R /topology.yaml` usa o parâmetro hello `topology.yaml` recursos de arquivo de topologia de Olá Olá jar arquivo toodefine.

    Como ele é executado, topologia Olá exibe informações de inicialização. Olá texto a seguir é um exemplo de saída de hello:

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    Há um atraso de 10 segundos entre os lotes das informações registradas em log.

2. Faça uma cópia do hello `topology.yaml` arquivo de projeto do hello. Novo arquivo de saudação nome `newtopology.yaml`. Em Olá `newtopology.yaml` de arquivo, localize a seguinte Olá seção e altera o valor de saudação do `10` muito`5`. Esse intervalo de saudação modificação alterações entre a emissão de lotes de palavra contagens de too5 de 10 segundos.

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    Se preferir, se você tiver o Storm no ambiente de desenvolvimento:

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    Saudação de alteração `/path/to/newtopology.yaml` toohello caminho toohello newtopology.yaml arquivo criado na etapa anterior hello. Esse comando usa Olá newtopology.yaml como definição de topologia de saudação. Como não incluímos Olá `compile` parâmetro, Maven usa a versão de saudação do projeto de saudação criado nas etapas anteriores.

    Uma vez Olá topologia é iniciado, você deve observar que o tempo de saudação entre os lotes emitidos alterou o valor de saudação de tooreflect em newtopology.yaml. Como você pode ver que você pode alterar sua configuração por meio de um arquivo YAML sem a necessidade de topologia de saudação toorecompile.

Para obter mais informações sobre esses e outros recursos da estrutura do fluxo de hello, consulte [fluxo (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).

## <a name="trident"></a>Trident

O Trident é uma abstração de alto nível fornecida pelo Storm. Ele dá suporte ao processamento com monitoramento de estado. Olá principal vantagem do Trident é que possa garantir que cada mensagem que entra em topologia Olá é processada apenas uma vez. Sem usar o Trident, sua topologia só pode garantir que as mensagens sejam processadas pelo menos uma vez. Também existem outras diferenças, como componentes internos que podem ser usados em vez da criação de bolts. Na verdade, os bolts são substituídos por componentes menos genéricos, como filtros, projeções e funções.

Os aplicativos Trident podem ser criados usando projetos Maven. Use Olá basic mesmo etapas, conforme apresentado anteriormente neste artigo — somente código Olá é diferente. Trident também (atualmente) não pode ser usado com o framework de fluxo de saudação.

Para obter mais informações sobre Trident, consulte Olá [visão geral da API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).

Para obter um exemplo de um aplicativo Trident, consulte [Trending topics do Twitter com Apache Storm no HDInsight](hdinsight-storm-twitter-trending.md).

## <a name="next-steps"></a>Próximas etapas

Você aprendeu como toocreate uma topologia Storm usando Java. Agora saiba como:

* [Implantar e gerenciar topologias Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology.md)

* [Desenvolver topologias C# para o Apache Storm no HDInsight usando o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Para obter mais topologias Storm, consulte [Topologias de exemplo para o Storm no HDInsight](hdinsight-storm-example-topology.md).

