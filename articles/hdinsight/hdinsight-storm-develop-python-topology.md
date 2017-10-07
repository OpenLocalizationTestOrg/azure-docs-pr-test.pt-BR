---
title: aaaApache Storm com componentes de Python - HDInsight do Azure | Microsoft Docs
description: Saiba como toocreate uma topologia do Apache Storm que usa componentes de Python.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>Desenvolver topologias do Apache Storm usando o Python no HDInsight

Saiba como toocreate uma topologia do Apache Storm que usa componentes de Python. Apache Storm dá suporte a vários idiomas, permitindo até que você toocombine componentes de diversos idiomas em uma topologia. Olá fluxo estrutura (introduzida com Storm 0.10.0) permite que você tooeasily criar soluções que usam componentes do Python.

> [!IMPORTANT]
> informações de saudação neste documento foi testadas usando o Storm no HDInsight 3.6. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

saudação de código para este projeto está disponível em [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).

## <a name="prerequisites"></a>Pré-requisitos

* Python 2.7 ou posterior

* Java JDK 1.8 ou superior

* Maven 3

* (Opcional) Um ambiente de desenvolvimento local do Storm. Um ambiente Storm local só é necessário se você quiser toorun topologia de saudação localmente. Para obter mais informações, consulte [Configurar um ambiente de desenvolvimento](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).

## <a name="storm-multi-language-support"></a>Suporte a várias linguagens no Storm

Apache Storm foi projetado toowork com componentes escritos usando qualquer linguagem de programação. componentes de saudação devem entender como toowork com hello [definição Thrift Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift). Para Python, um módulo é fornecido como parte do projeto do Apache Storm Olá que permite que você tooeasily interface com Storm. Você pode encontrar esse módulo em [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).

Tempestade é um processo de Java que é executado em Olá Máquina Virtual Java (JVM). Componentes escritos em outras linguagens são executados como subprocessos. Olá Storm se comunica com esses subprocessos usando JSON mensagens enviadas pela stdin/stdout. Mais detalhes sobre a comunicação entre os componentes podem ser encontrados no hello [Multi-lang protocolo](https://storm.apache.org/documentation/Multilang-protocol.html) documentação.

## <a name="python-with-hello-flux-framework"></a>Python com estrutura de fluxo de saudação

estrutura de fluxo de saudação permite que você toodefine topologias de Storm separadamente de componentes de saudação. estrutura do fluxo de Olá usa topologia de Storm YAML toodefine hello. Olá, texto a seguir é um exemplo de como tooreference um componente de Python no documento YAML hello:

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

Olá classe `FluxShellSpout` é usado toostart hello `sentencespout.py` script que implementa spout hello.

Fluxo espera Olá Python scripts toobe no hello `/resources` diretório dentro do arquivo jar Olá que contém a topologia de saudação. Para este exemplo armazena scripts de Python Olá em Olá `/multilang/resources` directory. Olá `pom.xml` inclui esse arquivo usando Olá XML a seguir:

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

Como mencionado anteriormente, há um `storm.py` arquivo que implementa a definição de Thrift Olá para Storm. Olá fluxo framework inclui `storm.py` automaticamente quando Olá projeto é compilado, para que você não tenha tooworry sobre incluí-lo.

## <a name="build-hello-project"></a>Compilar o projeto de saudação

De raiz de saudação do projeto hello, use Olá comando a seguir:

```bash
mvn clean compile package
```

Este comando cria um `target/WordCount-1.0-SNAPSHOT.jar` arquivo que contém a saudação compilado topologia.

## <a name="run-hello-topology-locally"></a>Executar topologia Olá localmente

topologia de saudação do toorun localmente, use Olá comando a seguir:

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> Esse comando requer um ambiente de desenvolvimento local do Storm. Para obter mais informações, consulte [Configurar um ambiente de desenvolvimento](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)

Uma vez Olá topologia inicia, ele emite informações toohello console local semelhante toohello texto a seguir:


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


topologia de saudação toostop, use __Ctrl + C__.

## <a name="run-hello-storm-topology-on-hdinsight"></a>Execute a topologia de profusão de saudação no HDInsight

1. Olá toocopy do comando de uso a seguir de saudação `WordCount-1.0-SNAPSHOT.jar` tooyour Storm no cluster HDInsight do arquivo:

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    Substituir `sshuser` com usuário SSH Olá para seu cluster. Substituir `mycluster` com o nome do cluster hello. Você pode ser solicitados tooenter senha Olá usuário SSH de saudação.

    Para obter mais informações sobre como usar o SSH e o SCP, confira [Usar o SSH com o HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Depois que o arquivo hello foi carregado, conecte-se toohello cluster usando o SSH:

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. Da sessão SSH hello, use Olá topologia de saudação do comando toostart a seguir no cluster hello:

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. Você pode usar a topologia de Olá Olá Storm da interface do usuário tooview em cluster hello. Olá profusão de interface do usuário está localizado em https://mycluster.azurehdinsight.net/stormui. Substitua `mycluster` pelo nome do cluster.

> [!NOTE]
> Após ser iniciada, uma topologia do Storm é executada até ser interrompida. toostop Olá topologia, use um dos métodos a seguir de saudação:
>
> * Olá `storm kill TOPOLOGYNAME` comando da linha de comando Olá
> * Olá **Kill** botão Olá profusão de interface do usuário.


## <a name="next-steps"></a>Próximas etapas

Consulte Olá documentos para outra maneiras de toouse Python com HDInsight a seguir:

* [Como toouse Python para streaming trabalhos MapReduce](hdinsight-hadoop-streaming-python.md)
* [Como toouse Python definida pelo usuário funções (UDF) na Pig e Hive](hdinsight-python.md)
