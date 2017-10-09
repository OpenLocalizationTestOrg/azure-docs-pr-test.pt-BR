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
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (Java)

Saiba como toouse Hubs de eventos do Azure com Storm no HDInsight. Este exemplo usa componentes baseados em Java tooread e gravar dados em Hubs de eventos do Azure.

Hubs de eventos do Azure permite que você tooprocess grandes quantidades de dados de sites, aplicativos e dispositivos. Olá spout Hub de eventos torna fácil toouse Apache Storm no HDInsight tooanalyze esses dados em tempo real. Você também pode escrever dados tooEvent Hubs do Storm usando Olá parafuso de Hubs de eventos.

## <a name="prerequisites"></a>Pré-requisitos

* Um Apache Storm no cluster HDInsight versão 3.6. Para obter mais informações, confira [Introdução ao Storm no cluster HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

    > [!IMPORTANT]
    > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Um [Hub de Eventos do Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

* [Oracle JDK (Java Developer Kit) versão 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou equivalente, por exemplo [OpenJDK](http://openjdk.java.net/).

* [Maven](https://maven.apache.org/download.cgi): o Maven é um sistema de criação de projetos para projetos Java.

* Um editor de texto ou um IDE (ambiente de desenvolvimento integrado).

    > [!NOTE]
    > Seu editor ou IDE pode ter uma funcionalidade específica para trabalhar com o Maven que não é abordada neste documento. Para obter informações sobre os recursos de saudação do seu ambiente de edição, consulte a documentação Olá produto Olá que está usando.

    * Um cliente SSH. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Olá `ssh` e `scp` comandos. Esses são o cluster do HDInsight usado toocopy arquivos toohello. No Windows, você pode obtê-los por meio do Bash no Windows 10.

## <a name="understanding-hello-example"></a>Exemplo de hello Noções básicas sobre

Olá [hdinsight-java storm eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) exemplo contém duas topologias:

Olá `resources/writer.yaml` topologia grava dados aleatórios tooan Hub de eventos do Azure. Olá dados são gerados por Olá `DeviceSpout` componente, e é uma ID de dispositivo aleatória e o valor do dispositivo. Dessa forma, ele está simulando um hardware que emite uma ID de cadeia de  caracteres e um valor numérico.

Três `resources/reader.yaml` topologia lê dados de Hub de eventos (dados Olá gravados pelo EventHubWriter,) analisa os dados JSON Olá e, em seguida, registra Olá `deviceId` e `deviceValue` dados.

Olá dados estão formatados como um documento JSON antes de ser gravado tooEvent Hub e, em que é lido pelo leitor de saudação que é analisada de JSON e em tuplas. formato do Hello JSON é da seguinte maneira:

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>Configuração do projeto

Olá `POM.xml` arquivo contém informações de configuração para este projeto Maven. Olá interessantes são:

#### <a name="event-hub-components"></a>Componentes do Hub de Eventos

componente de saudação que lê e grava tooAzure Hubs de eventos está localizado na Olá [HDInsight repositório](https://github.com/hdinsight/mvn-rep). Olá seguintes seções Olá `POM.xml` arquivo carga Olá componentes deste repositório

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>Olá EventHubs Storm Spout dependência

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

Esse xml define uma dependência para o pacote de eventhubs hello, que contém um spout para leitura dos Hubs de eventos e um raio de gravação tooit.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

Esse xml define a saída de toogenerate projeto Olá para Java 8, que é usado pelo HDInsight 3.5 ou superior.

#### <a name="hello-maven-shade-plugin"></a>Olá maven-tonalidade-plug-in

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

Esse xml configura a saída de hello Olá solução toopackage em um jar grande. jar Olá contém o código do projeto hello e dependências necessárias. Também é usado para:

* Renomear arquivos de licença para dependências de saudação.
* Exclua a segurança/as assinaturas.
* Certifique-se de que várias implementações de hello a mesma interface são mesclados em uma entrada.

Essas definições de configuração evitam erros em tempo de execução.

#### <a name="topology-definitions"></a>Definições de topologia

Este exemplo usa Olá [fluxo](https://storm.apache.org/releases/1.1.0/flux.html) framework. Essa estrutura usa topologias de saudação toodefine YAML. Olá o principal benefício é que você não configurar a topologia de saudação em código Java. Como definição de saudação YAML, você pode alterá-la antes de enviar a topologia hello, sem ter que toorecompile tudo.

__writer.yaml__:

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

__reader.yaml__:

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

#### <a name="tell-hello-topology-about-event-hub"></a>Conte-topologia Olá sobre Hub de eventos

Em tempo de execução, Olá `dev.properties` arquivo é usado toopass Olá Hub de eventos configuração toohello topologia. Olá é um exemplo conteúdo de padrão de saudação do arquivo hello:

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>Configurar variáveis de ambiente

Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK em sua estação de trabalho de desenvolvimento. No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.

* **JAVA_HOME** -deve apontar toohello diretório onde Olá o Java runtime environment (JRE) está instalado. Por exemplo, em uma distribuição Unix ou Linux, ele deve ter um valor semelhante muito`/usr/lib/jvm/java-7-oracle`. No Windows, ele deve ter um valor semelhante muito`c:\Program Files (x86)\Java\jre1.7`
* **CAMINHO** -deve conter Olá caminhos a seguir:

  * **JAVA_HOME** (ou caminho equivalente Olá)
  * **JAVA_HOME\bin** (ou caminho equivalente Olá)
  * diretório de saudação onde Maven está instalado

## <a name="configure-event-hub"></a>Configurar o Hub de Eventos

Hubs de eventos é a fonte de dados de saudação para este exemplo. Use Olá etapas toocreate um Hub de eventos a seguir.

1. De saudação [Portal clássico do Azure](https://manage.windowsazure.com), selecione **novo** > **Service Bus** > **Hub de eventos**  >  **Criação personalizada**.

2. Em Olá **adicionar um novo Hub de eventos** tela, insira um **nome do Hub de evento**. Selecione Olá **região** toocreate Olá hub e, em seguida, criar um namespace ou selecione um existente. Por fim, clique em Olá **seta** toocontinue.

    ![página 1 do assistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > Selecione Olá mesmo **local** como profusão de latência do HDInsight servidor tooreduce e os custos.

3. Em Olá **configurar Hub de eventos** tela, insira Olá **contagem de partição** e **retenção de mensagem** valores. Para este exemplo, use uma contagem de partições de 10 e uma retenção de mensagens de 1. Observe a contagem de partição Olá porque esse valor é necessário mais tarde.

    ![página 2 do assistente](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Depois que o hub de eventos de saudação tiver sido criado, marque Olá namespace, selecione **Hubs de eventos**e, em seguida, selecione o hub de eventos de saudação que você criou anteriormente.
5. Selecione **configurar**, crie duas novas políticas de acesso usando Olá informações a seguir:

    <table>
    <tr><th>Nome</th><th>Permissões</th></tr>
    <tr><td>Gravador</td><td>Enviar</td></tr>
    <tr><td>Leitor</td><td>Escutar</td></tr>
    </table>

    Depois de criar permissões hello, selecione Olá **salvar** ícone final Olá Olá página. Essas políticas de acesso compartilhado são usada tooread e tooEvent Hub de gravação.

    ![políticas](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. Depois de salvar políticas hello, usar Olá **gerador de chave de acesso compartilhado** final Olá Olá página tooretrieve Olá chave Olá **gravador** e **leitor** políticas. Salve essas chaves.

## <a name="download-and-build-hello-project"></a>Baixe e compilar o projeto de saudação

1. Baixe o projeto de saudação do GitHub: [hdinsight-java storm eventhub](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub). Você pode baixar o pacote de saudação como um arquivo zip, ou usar [git](https://git-scm.com/) tooclone projeto de saudação localmente.

2. Modificar Olá `dev.properties` arquivo de configuração de saudação para o Hub de eventos.

3. Use Olá toobuild pacote hello projeto a seguir:

        mvn package

    Esse comando baixa dependências necessárias, compilações, e, em seguida, pacotes Olá projeto. Olá saída é armazenada no hello **/destino** diretório como **EventHubExample-1.0-SNAPSHOT.jar**.

## <a name="test-locally"></a>Testar localmente

Como essas topologias apenas ler e gravar tooEvent Hubs, você pode testá-las localmente, se você tiver um [ambiente de desenvolvimento Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html). Use Olá toorun etapas localmente no ambiente de desenvolvimento Olá a seguir:

1. Execute o gravador de saudação:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Execute o leitor hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Topologia de saudação executar em modo local (não distribuídas).
> * `-R /writer.yaml`: Carregar a definição de topologia de saudação do hello `resources` empacotados no jar hello. Se a topologia de saudação é um arquivo no sistema de arquivos local hello, especifique Olá caminho tooit como o último parâmetro de saudação.
> * `--filter dev.properties`: Use o conteúdo de saudação do `dev.properties` toofill valores hello nas definições de topologia de saudação. Por exemplo: `${eventhub.read.policy.name}`.

Saída é console toohello conectado ao executar localmente. Use __Ctrl + C__ toostop topologia de saudação.

## <a name="deploy-hello-topologies"></a>Implantar topologias Olá

1. Use SCP toocopy Olá jar pacote tooyour cluster HDInsight. Substitua o nome de usuário com o usuário SSH Olá para o cluster. Substitua CLUSTERNAME com nome de saudação do cluster HDInsight:

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    Se você usou uma senha para sua conta SSH, você é solicitadas tooenter Olá por senha. Se você usou uma chave SSH com conta hello, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá caminho toohello arquivo de chave. Por exemplo, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    Este comando copia a pasta base do hello arquivo toohello de usuário SSH no cluster hello.

2. Depois que o arquivo hello concluiu o carregamento, use SSH tooconnect toohello HDInsight cluster. Substituir **USERNAME** nome de saudação do seu logon SSH. Substitua o **CLUSTERNAME** pelo nome do seu cluster HDInsight:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > Se você usou uma senha para sua conta SSH, você é solicitadas tooenter Olá por senha. Se você usou uma chave SSH com conta hello, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá caminho toohello arquivo de chave. Olá, exemplo a seguir carrega a chave privada saudação do `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. Use Olá topologias de saudação do toostart de comando a seguir:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Envia Olá topologia toohello serviço Nimbus, que inicia em nós de trabalho Olá cluster hello.

4. dados de saudação conectado tooview, vá toohttps://CLUSTERNAME.azurehdinsight.net/stormui, onde __CLUSTERNAME__ é o nome de saudação do cluster HDInsight. Selecione topologias hello e fazer drill down toohello componentes. Selecione Olá __porta__ entrada para uma instância de um componente tooview informações registradas em log.

5. Use Olá topologias de saudação toostop comandos a seguir:

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>Excluir o cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Próximas etapas

* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)
