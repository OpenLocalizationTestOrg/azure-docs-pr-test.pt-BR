---
title: aaaTroubleshoot Storm usando o Azure HDInsight | Microsoft Docs
description: Obter respostas a perguntas toocommon sobre o uso do Apache Storm com HDInsight do Azure.
keywords: "Azure HDInsight, Storm, perguntas frequentes, guia de solução de problemas, problemas comuns"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Solucionar problemas do Storm usando o Azure HDInsight

Saiba mais sobre questões hello e suas resoluções para trabalhar com cargas do Apache Storm no Apache Ambari.

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>Como acessar o hello profusão de interface do usuário em um cluster
Você tem duas opções para acessar Olá profusão de interface do usuário em um navegador:

### <a name="ambari-ui"></a>Interface do usuário do Ambari
1. Vá toohello Ambari painel.
2. Na lista de saudação de serviços, selecione **Storm**.
3. Em Olá **Links rápidos** menu, selecione **profusão de interface do usuário**.

### <a name="direct-link"></a>Link direto
Você pode acessar Olá profusão de interface do usuário em Olá URL a seguir:

https://\<nome DNS do cluster\>/stormui

Exemplo:

 https://stormcluster.azurehdinsight.net/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>Como posso transferir informações de ponto de verificação spout do hub de evento profusão de uma topologia tooanother

Quando você desenvolve topologias que leem dos Hubs de eventos do Azure usando Olá arquivo. jar do HDInsight Storm evento hub spout, você deve implantar uma topologia que tem o mesmo nome em um novo cluster de saudação. No entanto, você deve reter dados de ponto de verificação de saudação que foi confirmada tooApache ZooKeeper no cluster antigo hello.

### <a name="where-checkpoint-data-is-stored"></a>O local em que os dados de ponto de verificação são armazenados
Dados de ponto de verificação de deslocamentos são armazenados por spout de hub de evento Olá no ZooKeeper em dois caminhos de raiz:
- Pontos de verificação de spout não transacionais são armazenados em /eventhubspout.
- Dados de pontos de verificação de spout transacionais são armazenados em /transactional.

### <a name="how-toorestore"></a>Como toorestore
scripts de saudação tooget e bibliotecas que você use dados tooexport ZooKeeper e, em seguida, importa Olá dados back tooZooKeeper com um novo nome, consulte [exemplos profusão de HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

pasta lib de saudação tem arquivos. jar que contêm a implementação de saudação para operação de importação/exportação de saudação. Olá bash pasta tiver um script de exemplo que demonstra como dados tooexport Olá server ZooKeeper no cluster antigo hello e importe-o servidor de ZooKeeper toohello Voltar no novo cluster de saudação.

Executar Olá [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) Olá ZooKeeper nós tooexport de script e, em seguida, importar dados. Atualização Olá script toohello plataforma HDP (Hortonworks Data) versão correta. (Estamos trabalhando para tornar esses scripts genéricos no HDInsight. Scripts genéricos podem executar de qualquer nó no cluster Olá sem modificações pelo usuário hello.)

o comando de exportação Olá grava Olá tooan sistema de arquivos distribuído (HDFS) do Apache Hadoop caminho de metadados (em um repositório de armazenamento de BLOBs do Azure ou do repositório Azure Data Lake) em um local que você definir.

### <a name="examples"></a>Exemplos

#### <a name="export-offset-metadata"></a>Exportar metadados de deslocamento
1. Use o cluster do SSH toogo toohello ZooKeeper no cluster de saudação do ponto de verificação que Olá deslocamento precisa toobe exportado.
2. Olá executar comando a seguir (após a atualização Olá cadeia de caracteres de versão HDP) tooexport ZooKeeper deslocamento dados toohello /stormmetadta/zkdata HDFS caminho:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Importar metadados de deslocamento
1. Use o cluster do SSH toogo toohello ZooKeeper no cluster de saudação do ponto de verificação que Olá deslocamento precisa toobe exportado.
2. Execução hello seguinte comando (depois de atualizar a cadeia de caracteres de versão do hello HDP) tooimport ZooKeeper deslocamento dados de saudação caminho/stormmetadata/zkdata toohello ZooKeeper do servidor HDFS no cluster de destino hello:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>Excluir metadados deslocamento topologias podem iniciar o processamento de dados desde o início de hello, ou de um carimbo de hora que o usuário Olá escolhe
1. Use o cluster do SSH toogo toohello ZooKeeper no cluster de saudação do ponto de verificação que Olá deslocamento precisa toobe exportado.
2. Execução hello seguinte comando (depois de atualizar a cadeia de caracteres de versão do hello HDP) toodelete todos os ZooKeeper deslocamento dados no cluster de saudação atual:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Como fazer para localizar binários do Storm em um cluster
Binários de profusão de pilha atual de HDP Olá estão em /usr/hdp/current/storm-client. local de saudação é Olá mesmo para nós de cabeçalho e nós de trabalho.
 
Pode haver vários binários para versões específicas do HDP em /usr/hdp (por exemplo, /usr/hdp/2.5.0.1233/storm). pasta de /usr/hdp/current/storm-client Olá é symlinked toohello versão mais recente que está em execução no cluster de saudação.

Para obter mais informações, consulte [cluster do HDInsight tooan conectar usando o SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>Como determinar a topologia de implantação de saudação de um cluster Storm
Primeiro, identifique todos os componentes instalados com o HDInsight Storm. Um cluster do Storm consiste em quatro categorias de nó:

* Nós de gateway
* Nós de cabeçalho
* Nós do ZooKeeper
* Nós de trabalho
 
### <a name="gateway-nodes"></a>Nós de gateway
Um nó do gateway é um gateway e o serviço de proxy reverso que permite acesso público tooan active Ambari management service. Ele também lida com a seleção de líder do Ambari.
 
### <a name="head-nodes"></a>Nós de cabeçalho
Nós de cabeçalho Storm execute Olá serviços a seguir:
* Nimbus
* Servidor Ambari
* Servidor de Métricas do Ambari
* Coletor de Métricas do Ambari
 
### <a name="zookeeper-nodes"></a>Nós do ZooKeeper
O HDInsight tem um quorum do ZooKeeper de três nós. tamanho de quorum Olá é fixo e não pode ser reconfigurado.
 
Serviços de storm em cluster Olá são quorum de ZooKeeper tooautomatically configurado use hello.
 
### <a name="worker-nodes"></a>Nós de trabalho
Nós de trabalho Storm executam Olá serviços a seguir:
* Supervisor
* JVMs (máquinas virtuais Java) de trabalho, para executar topologias
* Agente do Ambari
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Como fazer para localizar binários de spout do hub de eventos Storm para desenvolvimento
 
Para obter mais informações sobre como usar arquivos. jar do Storm evento hub spout com sua topologia, consulte Olá recursos a seguir.
 
### <a name="java-based-topology"></a>Topologia baseada em Java
[Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (Java)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>Topologia baseada em C# (Mono em clusters Storm Linux no HDInsight 3.4+)
[Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Binários de spout do hub de eventos Storm mais recentes para clusters Storm Linux no HDInsight 3.5+
toolearn como toouse hello mais recente Storm evento hub spout que funciona com o HDInsight 3.5 + Linux Storm clusters, consulte Olá mvn-repo [arquivo Leiame](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Exemplos de código-fonte
Consulte [exemplos](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) como tooread e gravação de Hub de eventos do Azure usando uma topologia do Apache Storm (escrita em Java) em um cluster HDInsight do Azure.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>Como fazer para localizar arquivos de configuração do Storm Log4J nos clusters
 
arquivos de configuração tooidentify Log4J Apache para serviços Storm.
 
### <a name="on-head-nodes"></a>Em nós de cabeçalho
Olá Nimbus Log4J configuração é lida em /usr. hdp/\<versão HDP\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>Em nós de trabalho
configuração de supervisor Log4J Olá é lido de em /usr. hdp/\<versão HDP\>/storm/log4j2/cluster.xml.
 
arquivo de configuração de trabalho Log4J Olá é lido em /usr. hdp/\<versão HDP\>/storm/log4j2/worker.xml.
 
Exemplos: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

