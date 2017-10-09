---
title: "aaaPorts usado pelos serviços de Hadoop no HDInsight - Azure | Microsoft Docs"
description: "Uma lista de portas usadas pelos serviços do Hadoop em execução no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd14aed9-ec25-4bb3-a20c-e29562735a7d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 0abc5c1c678aa79816e3e82a74538d2fb6db40ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-used-by-hadoop-services-on-hdinsight"></a>Portas usadas pelos serviços do Hadoop em execução no HDInsight

Este documento fornece uma lista de portas Olá usado pelos serviços de Hadoop executados em clusters HDInsight baseados em Linux. Ele também fornece informações sobre portas usadas tooconnect toohello cluster usando o SSH.

## <a name="public-ports-vs-non-public-ports"></a>Portas públicas versus portas não públicas

Olá de HDInsight baseados em Linux clusters expõem apenas três portas publicamente na internet; 22, 23 e 443. Essas portas são usadas toosecurely cluster de Olá de acesso usando SSH e serviços expostos através do protocolo HTTPS seguro de saudação.

Internamente, o HDInsight é implementado por várias máquinas virtuais do Azure (nós Olá em cluster Olá) em execução em uma rede Virtual do Azure. Rede virtual do hello, você pode acessar portas não expostas em Olá internet. Por exemplo, se você conectar tooone de nós de cabeçalho hello usando SSH, do nó principal Olá você pode, em seguida, acessar diretamente os serviços em execução em nós de cluster de saudação.

> [!IMPORTANT]
> Se você não especificar uma Rede Virtual do Azure como uma opção de configuração para o HDInsight, uma será criada automaticamente. No entanto, você não pode associar outra rede virtual de toothis máquinas (como outras máquinas virtuais do Azure ou seu computador de desenvolvimento de cliente).


máquinas adicionais toojoin toohello a rede virtual, você deve primeiro criar rede virtual hello e, em seguida, especifique-ao criar seu cluster HDInsight. Para saber mais, confira [Estender os recursos do HDInsight usando a Rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md)

## <a name="public-ports"></a>Portas públicas

Saudação de todos os nós em um cluster do HDInsight estão localizados em uma rede Virtual do Azure e não podem ser acessados diretamente de Olá da internet. Um gateway público fornece toohello de acesso de internet portas, que são comuns a todos os tipos de cluster do HDInsight a seguir.

| O Barramento de | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| sshd |22 |SSH |Conecta-se toosshd de clientes em um nó principal do hello primário. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |22 |SSH |Conecta-se toosshd de clientes no nó de borda hello. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| sshd |23 |SSH |Conecta-se toosshd de clientes em um nó principal do hello secundário. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md). |
| Ambari |443 |HTTPS |Interface de usuário da Web do Ambari. Consulte [gerenciar HDInsight usando Olá Ambari Web UI](hdinsight-hadoop-manage-ambari.md) |
| Ambari |443 |HTTPS |API REST do Ambari. Consulte [gerenciar HDInsight usando Olá Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md) |
| WebHCat |443 |HTTPS |API REST do HCatalog. Confira [Usar Hive com Curl](hdinsight-hadoop-use-pig-curl.md), [Usar Pig com Curl](hdinsight-hadoop-use-pig-curl.md), [Usar MapReduce com Curl](hdinsight-hadoop-use-mapreduce-curl.md) |
| HiveServer2 |443 |ODBC |Conecta-se tooHive usando ODBC. Consulte [tooHDInsight Excel conectar-se com o driver de ODBC do Microsoft hello](hdinsight-connect-excel-hive-odbc-driver.md). |
| HiveServer2 |443 |JDBC |Conecta-se tooHive usando o JDBC. Consulte [conectar tooHive no HDInsight usando Olá Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md) |

a seguir Olá está disponível para tipos específicos de cluster:

| O Barramento de | Port | Protocolo | Tipo de cluster | Descrição |
| --- | --- | --- | --- | --- |
| Stargate |443 |HTTPS |HBase |API REST do HBase. Confira [Introdução ao HBase](hdinsight-hbase-tutorial-get-started-linux.md) |
| Livy |443 |HTTPS |Spark |API REST do Spark. Confira [Enviar trabalhos do Spark remotamente usando o Livy](hdinsight-apache-spark-livy-rest-interface.md) |
| Storm |443 |HTTPS |Storm |Interface de usuário do Storm para Web. Confira [Implantar e gerenciar topologias Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md) |

### <a name="authentication"></a>Autenticação

Todos os serviços expostos publicamente Olá que Internet deve ser autenticada:

| Porta | Credenciais |
| --- | --- |
| 22 ou 23 |credenciais de usuário SSH Olá especificadas durante a criação do cluster |
| 443 |nome de logon da saudação (padrão: administrador) e a senha que foram definidos durante a criação do cluster |

## <a name="non-public-ports"></a>Portas não públicas

> [!NOTE]
> Alguns serviços só estão disponíveis em tipos de cluster específicos. Por exemplo, HBase só está disponível em tipos de cluster HBase.

> [!IMPORTANT]
> Alguns serviços são executados somente em um nó de cabeçalho por vez. Se você tenta tooconnect toohello serviço em um nó principal do hello primário e recebe uma mensagem de erro 404, tente novamente usando um nó principal do hello secundário.

### <a name="ambari"></a>Ambari

| O Barramento de | Nós | Porta | Caminho da URL | Protocolo | 
| --- | --- | --- | --- | --- |
| Interface do usuário da Web do Ambari | Nós de cabeçalho | 8080 | / | HTTP |
| API REST do Ambari | Nós de cabeçalho | 8080 | /api/v1 | HTTP |

Exemplos:

* API REST do Ambari: `curl -u admin "http://10.0.0.11:8080/api/v1/clusters"`

### <a name="hdfs-ports"></a>Portas HDFS

| O Barramento de | Nós | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| Interface de usuário do NameNode na Web |Nós de cabeçalho |30070 |HTTPS |Status de tooview de interface do usuário da Web |
| Serviço de metadados NameNode |Nós de cabeçalho |8020 |IPC |Metadados do sistema de arquivos |
| DataNode |Todos os nós de trabalho |30075 |HTTPS |Status de tooview de interface do usuário da Web, logs, etc. |
| DataNode |Todos os nós de trabalho |30010 |&nbsp; |Transferência de dados |
| DataNode |Todos os nós de trabalho |30020 |IPC |Operações de metadados |
| NameNode secundário |Nós de cabeçalho |50090 |HTTP |Ponto de verificação para metadados do NameNode |

### <a name="yarn-ports"></a>Portas YARN

| O Barramento de | Nós | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| Interface de usuário na Web do Resource Manager |Nós de cabeçalho |8088 |HTTP |Interface de usuário na Web do Resource Manager |
| Interface de usuário na Web do Resource Manager |Nós de cabeçalho |8090 |HTTPS |Interface de usuário na Web do Resource Manager |
| Interface administrativa do Resource Manager |Nós de cabeçalho |8141 |IPC |Para envios de aplicativo (Hive, servidor Hive, Pig, etc.) |
| Agendador do Resource Manager |Nós de cabeçalho |8030 |HTTP |Interface administrativa |
| Interface de aplicativo do Resource Manager |Nós de cabeçalho |8050 |HTTP |Endereço da interface do Gerenciador de aplicativos Olá |
| NodeManager |Todos os nós de trabalho |30050 |&nbsp; |endereço de saudação do Gerenciador de contêiner de saudação |
| Interface de usuário na Web do NodeManager |Todos os nós de trabalho |30060 |HTTP |Interface do Resource Manager |
| Endereço do Timeline |Nós de cabeçalho |10200 |RPC |saudação do serviço RPC de serviço da linha do tempo. |
| Interface de usuário na Web do Timeline |Nós de cabeçalho |8181 |HTTP |a IU da web do serviço Olá da linha do tempo |

### <a name="hive-ports"></a>Portas Hive

| O Barramento de | Nós | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| HiveServer2 |Nós de cabeçalho |10001 |Thrift |Serviço de conexão tooHive (Thrift/JDBC) |
| Metastore do Hive |Nós de cabeçalho |9083 |Thrift |Serviço de conexão tooHive metadados (Thrift/JDBC) |

### <a name="webhcat-ports"></a>Portas WebHCat

| O Barramento de | Nós | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| Servidor WebHCat |Nós de cabeçalho |30111 |HTTP |API Web sobre o HCatalog e outros serviços do Hadoop |

### <a name="mapreduce-ports"></a>Portas MapReduce

| O Barramento de | Nós | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| JobHistory |Nós de cabeçalho |19888 |HTTP |Interface de usuário na Web JobHistory do MapReduce |
| JobHistory |Nós de cabeçalho |10020 |&nbsp; |Servidor JobHistory do MapReduce |
| ShuffleHandler |&nbsp; |13562 |&nbsp; |Mapa de transferências intermediário gera toorequesting Reducers |

### <a name="oozie"></a>Oozie

| O Barramento de | Nós | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| Servidor Oozie |Nós de cabeçalho |11000 |HTTP |URL para o serviço do Oozie |
| Servidor Oozie |Nós de cabeçalho |11001 |HTTP |Porta para administração do Oozie |

### <a name="ambari-metrics"></a>Métricas do Ambari

| O Barramento de | Nós | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| TimeLine (histórico do aplicativo) |Nós de cabeçalho |6188 |HTTP |a IU da web do serviço Olá da linha do tempo |
| TimeLine (histórico do aplicativo) |Nós de cabeçalho |30200 |RPC |a IU da web do serviço Olá da linha do tempo |

### <a name="hbase-ports"></a>Portas HBase

| O Barramento de | Nós | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| HMaster |Nós de cabeçalho |16000 |&nbsp; |&nbsp; |
| Interface de usuário na Web para informações do HMaster |Nós de cabeçalho |16010 |HTTP |porta Olá Olá HBase mestre web da interface do usuário |
| Servidor de região |Todos os nós de trabalho |16020 |&nbsp; |&nbsp; |
| &nbsp; |&nbsp; |2181 |&nbsp; |porta de saudação que os clientes usam tooconnect tooZooKeeper |

### <a name="kafka-ports"></a>Portas Kafka

| O Barramento de | Nós | Port | Protocolo | Descrição |
| --- | --- | --- | --- | --- |
| Agente |Nós de trabalho |9092 |[Protocolo Kafka Wire](http://kafka.apache.org/protocol.html) |Usado para comunicação do cliente |
| &nbsp; |Nós do Zookeeper |2181 |&nbsp; |porta de saudação que os clientes usam tooconnect tooZookeeper |

### <a name="spark-ports"></a>Portas do Spark

| O Barramento de | Nós | Port | Protocolo | Caminho da URL | Descrição |
| --- | --- | --- | --- | --- | --- |
| Servidores Thrift Spark |Nós de cabeçalho |10002 |Thrift | &nbsp; | Serviço de conexão tooSpark SQL (Thrift/JDBC) |
| Servidor Livy | Nós de cabeçalho | 8998 | HTTP | /batches | Serviço para executar instruções, trabalhos e aplicativos |

Exemplos:

* Livy: `curl "http://10.0.0.11:8998/batches"`. Neste exemplo, `10.0.0.11` é endereço IP de saudação do hello um nó principal que hospeda o serviço Livy de saudação.
