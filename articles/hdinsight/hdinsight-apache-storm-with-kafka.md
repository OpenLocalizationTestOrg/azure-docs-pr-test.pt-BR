---
title: aaaUse Kafka Apache com Storm no HDInsight - Azure | Microsoft Docs
description: "O Apache Kafka é instalado com o Apache Storm no HDInsight. Saiba como toowrite tooKafka e, em seguida, ler, usando Olá KafkaBolt e KafkaSpout componentes fornecidos com Storm. Também aprenderá como toouse Olá fluxo framework toodefine e enviar topologias Storm."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>Usar o Apache Kafka (visualização) com o Storm no HDInsight

Saiba como toouse Apache Storm tooread de e escrever tooApache Kafka. Este exemplo também demonstra como sistema usado pelo HDInsight do arquivo de dados de toosave de uma topologia de Storm toohello compatível com o HDFS.

> [!NOTE]
> etapas de saudação neste documento criam um grupo de recursos do Azure que contém tanto uma profusão de HDInsight e um Kafka no cluster HDInsight. Esses agrupamentos são ambos localizados em uma rede Virtual do Azure, que permite Olá Storm cluster toodirectly Olá cluster Kafka se comunicam.
> 
> Quando você concluir etapas Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.

## <a name="get-hello-code"></a>Obter o código de saudação

Olá código de exemplo hello usado neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).

toocompile este projeto, você precisa Olá seguinte configuração para o seu ambiente de desenvolvimento:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior. HDInsight 3.5 ou superior exige Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

* Um cliente SSH (é necessário Olá `ssh` e `scp` comandos) - para obter informações, consulte [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Um editor de texto ou IDE.

Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK em sua estação de trabalho de desenvolvimento. No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.

* `JAVA_HOME`-deve apontar toohello diretório onde hello JDK está instalado.
* `PATH`-deve conter Olá caminhos a seguir:
  
    * `JAVA_HOME`(ou caminho equivalente Olá).
    * `JAVA_HOME\bin`(ou caminho equivalente Olá).
    * diretório de saudação onde Maven está instalado.

## <a name="create-hello-clusters"></a>Criar clusters de saudação

Apache Kafka no HDInsight não fornece acesso toohello Kafka agentes sobre Olá internet pública. Qualquer coisa que fala tooKafka deve estar no hello mesma rede virtual do Azure como nós Olá Olá cluster Kafka. Neste exemplo, Olá Kafka e clusters Storm estão localizados em uma rede virtual do Azure. Olá diagrama a seguir mostra como a comunicação flui entre clusters de saudação:

![Diagrama de clusters Storm e Kafka em uma rede virtual do Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> Outros serviços em cluster hello como SSH e Ambari podem ser acessados pela Olá da internet. Para obter mais informações sobre portas públicas de saudação disponíveis com o HDInsight, consulte [portas e URIs usados por HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Embora você pode criar uma rede virtual do Azure, Kafka, e Storm clusters manualmente, é mais fácil toouse um modelo do Gerenciador de recursos do Azure. Toodeploy uma rede virtual do Azure, Kafka, as etapas a seguir do uso hello e Storm clusters tooyour assinatura do Azure.

1. Use Olá botão toosign em tooAzure e modelo Olá abrir no portal do Azure de saudação a seguir.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello Azure Resource Manager modelo está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**. Ele cria Olá recursos a seguir:
    
    * Grupo de recursos do Azure
    * Rede Virtual do Azure
    * Conta de Armazenamento do Azure
    * Kafka no HDInsight versão 3.6 (três nós de trabalho)
    * Storm no HDInsight versão 3.6 (três nós de trabalho)

  > [!WARNING]
  > disponibilidade de tooguarantee de Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho. Este modelo cria um cluster de Kafka que contém três nós de trabalho.

2. Olá usar entradas de saudação toopopulate diretrizes a seguir em hello **implantação personalizada** folha:
   
    ![Implantação personalizada do HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **Grupo de recursos**: Crie um grupo ou selecione um existente. Esse grupo contém o cluster do HDInsight hello.
   
    * **Local**: selecione um tooyou geograficamente fechar do local.

    * **Nome do Cluster base**: esse valor é usado como nome de base Olá para clusters de saudação Storm e Kafka. Por exemplo, inserir **hdi** cria um cluster Storm chamado **storm-hdi** e um cluster Kafka chamado **kafka-hdi**.
   
    * **Nome de usuário de logon de cluster**: nome de usuário de administrador Olá para clusters de saudação Storm e Kafka.
   
    * **Senha de logon de cluster**: senha do usuário administrador Olá para clusters de saudação Storm e Kafka.
    
    * **Nome de usuário SSH**: Olá toocreate de usuário SSH para clusters de saudação Storm e Kafka.
    
    * **Senha SSH**: senha Olá para usuário SSH Olá Olá Storm e Kafka clusters.

3. Saudação de leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições declaradas acima**.

4. Finalmente, verifique **Pin toodashboard** e, em seguida, selecione **compra**. Demora cerca de 20 minutos toocreate clusters hello.

Após a criação dos recursos de hello, folha Olá Olá para grupo de recursos é exibida.

![Folha de grupo de recursos para redes hello e clusters](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Observe que os nomes de saudação de clusters de HDInsight Olá ficam **profusão de nome de base** e **kafka nome de base**, onde nome base é o nome da saudação fornecido toohello modelo. Você pode usar esses nomes em etapas posteriores ao conectar-se toohello clusters.

## <a name="understanding-hello-code"></a>Entendendo o código Olá

Este projeto contém duas topologias:

* **KafkaWriter**: definidos por Olá **writer.yaml** arquivo, esta topologia grava tooKafka sentenças aleatório usando Olá KafkaBolt fornecido com o Apache Storm.

    Essa topologia usa um personalizado **SentenceSpout** sentenças aleatório do componente toogenerate.

* **KafkaReader**: definidos por Olá **reader.yaml** arquivo, esta topologia lê dados de Kafka usando Olá KafkaSpout fornecido com o Apache Storm e logs Olá toostdout de dados.

    Essa topologia usa o hello Storm HdfsBolt toowrite dados toodefault armazenamento para cluster Storm de saudação.
### <a name="flux"></a>Flux

topologias de saudação são definidas usando [fluxo](https://storm.apache.org/releases/1.1.0/flux.html). Fluxo foi introduzido no Storm 0.10.x e permite que você tooseparate configuração de topologia de saudação do código de saudação. Para topologias que usam a estrutura do fluxo de Olá, topologia Olá é definida em um arquivo YAML. arquivo YAML de saudação pode ser incluído como parte da topologia de saudação. Ele também pode ser um arquivo autônomo usado ao enviar a topologia de saudação. O Flux também dá suporte à substituição de variáveis em tempo de execução, o que é usado neste exemplo.

Olá seguintes parâmetros são definidos em tempo de execução para essas topologias:

* `${kafka.topic}`: nome de saudação do hello Kafka tópico topologias Olá leitura/gravação para.

* `${kafka.broker.hosts}`: Olá hospeda esse Olá Kafka os agentes executado em. informações de agente de Hello são usadas pelo Olá KafkaBolt ao gravar tooKafka.

* `${kafka.zookeeper.hosts}`: hosts Olá Zookeeper executado na Olá cluster Kafka.

Para obter mais informações sobre as topologias do Flux, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="download-and-compile-hello-project"></a>Baixe e compilar o projeto de saudação

1. Em seu ambiente de desenvolvimento, baixe o projeto de saudação do [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), abra uma linha de comando e altere diretórios toohello local que você baixou o projeto de saudação.

2. De saudação **hdinsight-storm java kafka** diretório a seguir Olá use projeto de saudação toocompile de comando e cria um pacote para implantação:

  ```bash
  mvn clean package
  ```

    processo de pacote de saudação cria um arquivo chamado `KafkaTopology-1.0-SNAPSHOT.jar` em Olá `target` directory.

3. Use Olá comandos toocopy Olá pacote tooyour Storm a seguir no cluster HDInsight. Substituir **nome de usuário** com nome de usuário SSH Olá para cluster hello. Substituir **nome base** com o nome de base Olá usados ao criar o cluster de saudação.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    Quando solicitado, insira a senha Olá usada durante a criação de clusters de saudação.

## <a name="configure-hello-topology"></a>Configurar a topologia de saudação

1. Use uma saudação toodiscover métodos a seguir Olá hosts de broker Kafka:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Olá Bash exemplo supõe que `$CLUSTERNAME` contém nome de saudação do cluster do HDInsight hello. Ele também pressupõe que [jq](https://stedolan.github.io/jq/) esteja instalado. Quando solicitado, insira a senha Olá Olá cluster conta de logon.

    valor de saudação retornado é semelhante toohello texto a seguir:

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > Embora possa haver mais de dois hosts de agente para o cluster, não é necessário tooprovide uma lista completa de todos os tooclients de hosts. Um ou dois são suficientes.

2. Use uma saudação hosts de Kafka Zookeeper métodos toodiscover Olá a seguir:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Olá Bash exemplo supõe que `$CLUSTERNAME` contém nome de saudação do cluster do HDInsight hello. Ele também pressupõe que [jq](https://stedolan.github.io/jq/) esteja instalado. Quando solicitado, insira a senha Olá Olá cluster conta de logon.

    valor de saudação retornado é semelhante toohello texto a seguir:

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > Embora haja mais de dois nós Zookeeper, não é necessário tooprovide uma lista completa de todos os tooclients de hosts. Um ou dois são suficientes.

    Salve esse valor, pois ele é usado mais tarde.

3. Editar saudação `dev.properties` arquivo na raiz de saudação do projeto de saudação. Adicione hello Broker e linhas correspondentes do toohello Zookeeper hosts informações neste arquivo. Olá exemplo a seguir é configurado com os valores de exemplo hello de etapas anteriores hello:

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Salvar Olá `dev.properties` arquivo e usar o hello após o comando tooupload-cluster Storm de toohello:

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    Substituir **nome de usuário** com nome de usuário SSH Olá para cluster hello. Substituir **nome base** com o nome de base Olá usados ao criar o cluster de saudação.

## <a name="start-hello-writer"></a>Iniciar o gravador de saudação

1. Use Olá seguindo o cluster de Storm toohello tooconnect usando o SSH. Substituir **nome de usuário** com nome de usuário SSH Olá usado ao criar o cluster de saudação. Substituir **nome base** com o nome de base Olá usado ao criar o cluster de saudação.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    Quando solicitado, insira a senha Olá usada durante a criação de clusters de saudação.
   
    Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. De Olá conexão SSH, use Olá Olá do comando toocreate tópico Kafka usado pelo topologia Olá a seguir:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    Substituir `$KAFKAZKHOSTS` com hello Zookeeper hospedar as informações recuperadas na seção anterior hello.

2. De cluster da saudação SSH conexão toohello Storm, use Olá topologia de gravador de saudação do comando toostart a seguir:

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    Olá parâmetros usados com este comando são:

    * `org.apache.storm.flux.Flux`: Use fluxo tooconfigure e execute esta topologia.

    * `--remote`: Envie Olá tooNimbus de topologia. topologia de saudação é distribuída entre nós de trabalho Olá cluster hello.

    * `-R /writer.yaml`: Olá usar `writer.yaml` tooconfigure topologia de saudação do arquivo. `-R`indica que esse recurso está incluído no arquivo jar de saudação. É na raiz de saudação do jar hello, portanto `/writer.yaml` é Olá tooit de caminho.

    * `--filter`: Preencher entradas no hello `writer.yaml` topologia usando valores de saudação `dev.properties` arquivo. Olá, por exemplo, o valor de saudação `kafka.topic` entrada no arquivo hello é usado tooreplace Olá `${kafka.topic}` entrada em definição de topologia de saudação.

5. Após o início de topologia Olá use Olá tooverify de comando que está gravando dados toohello tópico Kafka a seguir:

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    Substituir `$KAFKAZKHOSTS` com hello Zookeeper hospedar as informações recuperadas na seção anterior hello.

    Esse comando usa um script que acompanham o tópico de saudação do Kafka toomonitor. Após um momento, ele deve ser iniciado retornando aleatórias sentenças que foram gravadas toohello tópico. saudação de saída é similar toohello exemplo a seguir:

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Use Ctrl + c toostop script de saudação.

## <a name="start-hello-reader"></a>Leitor de saudação inicial

1. De cluster da saudação SSH sessão toohello Storm, use Olá topologia de leitor de saudação do comando toostart a seguir:

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. Depois de iniciada a topologia hello, abra Olá profusão de interface do usuário. Essa interface do usuário da Web está localizada em https://storm-BASENAME.azurehdinsight.net/stormui. Substituir __nome base__ com o nome de base Olá usado quando Olá cluster foi criado. 

    Quando solicitado, use o nome de logon do administrador de saudação (padrão, `admin`) e a senha usada durante a saudação cluster foi criado. Você verá um toohello semelhante de página da web imagem a seguir:

    ![Interface do Usuário do Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. Olá profusão de interface do usuário, selecione Olá __kafka leitor__ link no hello __Resumo da topologia__ seção toodisplay informações sobre Olá __kafka leitor__ topologia.

    ![Na seção topologia do resumida da interface da web hello Storm](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. toodisplay informações sobre as instâncias de saudação do componente de raio do agente de log hello, selecione Olá __raio de agente de log__ link no hello __parafusos (tempo de todos os)__ seção.

    ![Link de raio de agente na seção de parafusos Olá](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. Em Olá __executores__ seção, selecione um link no hello __porta__ log de toodisplay de coluna de informações sobre essa instância do componente de saudação.

    ![Link de executores](./media/hdinsight-apache-storm-with-kafka/executors.png)

    log Olá contém um log de saudação da leitura dos dados Olá tópico Kafka. informações de Olá no log de saudação são semelhante toohello texto a seguir:

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Parar topologias Olá

De um cluster Storm do SSH sessão toohello, use Olá topologias de profusão de saudação de toostop comandos a seguir:

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Excluir o cluster Olá

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Como criam etapas de saudação neste documento hello de clusters no mesmo grupo de recursos do Azure, você pode excluir o grupo de recursos Olá Olá portal do Azure. Excluindo grupo de recursos de saudação remove todos os recursos criados por este documento a seguir.

## <a name="next-steps"></a>Próximas etapas

Para obter mais topologias de exemplo que podem ser usadas com o Storm no HDInsight, confira [Topologias Storm de exemplo e componentes](hdinsight-storm-example-topology.md).

Para obter informações sobre como implantar e monitorar topologias no HDInsight baseado em Linux, confira [Implantar e gerenciar topologias Apache Storm no HDInsight baseado em Linux](hdinsight-storm-deploy-monitor-topology-linux.md)