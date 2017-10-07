---
title: aaaStart com Kafka Apache - HDInsight do Azure | Microsoft Docs
description: "Saiba como toocreate uma Kafka Apache cluster no Azure HDInsight. Saiba como toocreate tópicos, assinantes e consumidores."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>Introdução ao Apache Kafka (versão prévia) no HDInsight

Saiba como toocreate e usar um [Kafka Apache](https://kafka.apache.org) cluster no Azure HDInsight. O Kafka é uma plataforma de streaming distribuída de software livre que está disponível com o HDInsight. Ele geralmente é usado como um agente de mensagem, pois ela fornece funcionalidade semelhante tooa publicação / assinatura fila de mensagens.

> [!NOTE]
> Atualmente, há duas versões do Kafka disponíveis com o HDInsight: 0.9.0 (HDInsight 3.4) e 0.10.0 (HDInsight 3.5 e 3.6). etapas de saudação neste documento pressupõem que você esteja usando Kafka em HDInsight 3.6.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>Criar um cluster Kafka

Use Olá seguindo as etapas toocreate um Kafka no cluster HDInsight:

1. De saudação [portal do Azure](https://portal.azure.com), selecione **+ novo**, **Intelligence + análise**e, em seguida, selecione **HDInsight**.
   
    ![Criar um cluster HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. De **Noções básicas de**, digite Olá informações a seguir:

    * **Nome do cluster**: nome de saudação do cluster do HDInsight de saudação.
    * **Assinatura**: selecione Olá toouse de assinatura.
    * **Nome de usuário de logon de cluster** e **senha de logon de Cluster**: logon Olá ao acessar o cluster Olá via HTTPS. Você usa esses serviços de tooaccess de credenciais como saudação da interface do usuário do Ambari Web ou a API REST.
    * **Secure Shell (SSH) username**: logon Olá usado ao acessar o cluster Olá via SSH. Por padrão senha Olá é Olá igual à senha de logon de cluster hello.
    * **Grupo de recursos**: Olá recurso grupo toocreate Olá cluster.
    * **Local**: Olá região do Azure toocreate Olá cluster.
   
 ![Escolha a assinatura](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. Selecione **tipo de Cluster**, e, em seguida, Olá conjunto seguindo os valores de **configuração de Cluster**:
   
    * **Tipo de Cluster**: Kafka

    * **Versão**: Kafka 0.10.0 (HDI 3.6)

    * **Camada de Cluster**: Padrão
     
 Por fim, use Olá **selecione** toosave configurações de botão.
     
 ![Selecione o tipo de cluster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. Depois de selecionar o tipo de cluster hello, use Olá __selecione__ tooset Olá cluster tipo de botão. Em seguida, use Olá __próximo__ configuração básica do botão toofinish.

5. Em **Armazenamento**, selecione ou crie uma Conta de armazenamento. Para obter etapas Olá neste documento, deixe Olá outros campos com valores padrão de saudação. Saudação de uso __próximo__ configuração de armazenamento de toosave do botão.

    ![Definir configurações de conta de armazenamento Olá para HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. De __aplicativos (opcionais)__, selecione __próximo__ toocontinue. Nenhum aplicativo é necessário neste exemplo.

7. De __tamanho do Cluster__, selecione __próximo__ toocontinue.

    > [!WARNING]
    > disponibilidade de tooguarantee de Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho.

    ![Saudação de conjunto de tamanho do cluster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > Olá **discos por nó de trabalho** controles de entrada hello escalabilidade de Kafka no HDInsight. Para saber mais, veja [Configurar o armazenamento e a escalabilidade do Kafka no HDInsight](hdinsight-apache-kafka-scalability.md).

8. De __configurações avançadas__, selecione __próximo__ toocontinue.

9. De saudação **resumo**, examine a configuração Olá para cluster hello. Saudação de uso __editar__ links toochange todas as configurações que estão incorretas. Por fim, use o cluster de saudação do the__Create__ botão toocreate.
   
    ![Resumo da configuração do cluster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > Pode demorar até o cluster de saudação de toocreate too20 minutos.

## <a name="connect-toohello-cluster"></a>Conecte-se o cluster toohello

> [!IMPORTANT]
> Ao executar Olá etapas a seguir, você deve usar um cliente SSH. Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

De seu cliente, use SSH tooconnect toohello cluster:

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

Substituir **SSHUSER** com nome de usuário SSH Olá fornecido durante a criação do cluster. Substituir **CLUSTERNAME** com o nome de saudação do cluster hello.

Quando solicitado, insira a senha Olá usada Olá conta SSH.

Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="getkafkainfo"></a>Obter informações de saudação Zookeeper e agente de host

Ao trabalhar com Kafka, você deve saber os dois valores de host; Olá *Zookeeper* hosts e hello *Broker* hosts. Esses hosts são usados com hello Kafka API e muitos utilitários Olá que vêm com Kafka.

As etapas a seguir de saudação de uso toocreate variáveis de ambiente que contêm informações de host de saudação. Essas variáveis de ambiente são usadas nas etapas Olá neste documento.

1. De um cluster de toohello de conexão SSH, Olá tooinstall de comando de uso a seguir de Olá `jq` utilitário. Esse utilitário é usado tooparse documentos JSON e é útil para recuperar informações do host de agente Olá:
   
    ```bash
    sudo apt -y install jq
    ```

2. variáveis de ambiente Olá tooset com informações recuperada do Ambari, Olá use comandos a seguir:

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > Definir `CLUSTERNAME=` toohello nome da saudação cluster Kafka. Definir `PASSWORD=` toohello senha de logon (admin) usado durante a criação de cluster de saudação.

    Olá, texto a seguir é um exemplo do conteúdo de saudação do `$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    Olá, texto a seguir é um exemplo do conteúdo de saudação do `$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > Olá `cut` comando é a lista de saudação de tootrim usadas de entradas de host tootwo hosts. Lista completa de saudação de tooprovide de hosts não é necessário durante a criação de um consumidor de Kafka ou o produtor.
   
    > [!WARNING]
    > Não se baseiam nas informações de saudação retornadas desta sessão tooalways sejam precisas. Se você expandir o cluster hello, os novos agentes são adicionados ou removidos. Se ocorrer uma falha e um nó for substituído, nome do host Olá para o nó de saudação pode mudar.
    >
    > Deve recuperar informações de hosts de Zookeeper e agente Olá logo antes de usá-lo tooensure tem informações válidas.

## <a name="create-a-topic"></a>Criar um tópico

O Kafka armazena fluxos de dados em categorias chamadas *tópicos*. De um SSH conexão tooa cluster um nó principal, use um script fornecido com Kafka toocreate um tópico:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

Esse comando conecta tooZookeeper usando Olá host informações armazenadas em `$KAFKAZKHOSTS`e, em seguida, criar tópico Kafka chamado **teste**. Você pode verificar que esse tópico Olá foi criado usando Olá tópicos toolist de script a seguir:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

Olá saída desse comando lista Kafka tópicos, que contém a saudação **teste** tópico.

## <a name="produce-and-consume-records"></a>Produzir e consumir registros

O Kafka armazena *registros* nos tópicos. Os registros são produzidos por *produtores* e consumidos por *consumidores*. Os produtores recuperam registros de *agentes* do Kafka. Cada nó de trabalho no cluster HDInsight é um agente do Kafka.

Use Olá registros de toostore as etapas a seguir no tópico de teste Olá você criou anteriormente e, em seguida, lê-los usando um consumidor:

1. Da sessão SSH Olá, use um script fornecido com o tópico de toohello Kafka toowrite registros:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    Você não retornará toohello prompt após esse comando. Em vez disso, digite algumas mensagens de texto e, em seguida, use **Ctrl + C** toostop enviar toohello tópico. Cada linha é enviada como um registro separado.

2. Use um script fornecido com registros de tooread Kafka tópico hello:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    Esse comando recupera os registros de saudação do tópico hello e os exibe. Usando `--from-beginning` informa Olá consumidor toostart desde o início de saudação do fluxo de Olá para todos os registros são recuperados.

3. Use __Ctrl + C__ toostop consumidor de saudação.

## <a name="producer-and-consumer-api"></a>API de produtor e consumidor

Também por meio de programação, você pode produzir e consumir registros usando Olá [Kafka APIs](http://kafka.apache.org/documentation#api). toobuild um produtor de Java e consumidor, use Olá seguindo as etapas do seu ambiente de desenvolvimento.

> [!IMPORTANT]
> Você deve ter Olá instalados em seu ambiente de desenvolvimento de componentes a seguir:
>
> * [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou equivalente, como OpenJDK.
>
> * [Apache Maven](http://maven.apache.org/)
>
> * Um cliente SSH e hello `scp` comando. Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.

1. Baixe os exemplos de saudação do [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started). Para exemplo de produtor/consumidor hello, use projeto Olá no hello `Producer-Consumer` directory. Este exemplo contém Olá classes a seguir:
   
    * **Executar** -inicia o consumidor hello ou o produtor.

    * **Produtor** -repositórios 1.000.000 registros toohello tópico.

    * **Consumidor** -lê os registros de tópico hello.

2. toocreate um pacote jar, alterar o local de toohello de diretórios da saudação `Producer-Consumer` saudação de diretório e usar comandos a seguir:

    ```
    mvn clean package
    ```

    Esse comando cria um diretório chamado `target`, que contém um arquivo chamado `kafka-producer-consumer-1.0-SNAPSHOT.jar`.

3. A seguir Olá use comandos Olá toocopy `kafka-producer-consumer-1.0-SNAPSHOT.jar` cluster do HDInsight tooyour arquivo:
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    Substituir **SSHUSER** com usuário SSH Olá para o cluster e substituir **CLUSTERNAME** com nome de saudação do cluster. Quando solicitado que digite a senha de saudação do usuário SSH hello.

4. Uma vez Olá `scp` comando concluído a cópia do arquivo hello, conecte-se o cluster toohello usando o SSH. Saudação de uso toowrite de comando a seguir registra toohello testar tópico:

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. Quando tiver terminado de processo Olá, use Olá após o comando tooread tópico hello:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    Olá ler, juntamente com uma contagem de registros, é exibido. Você pode ver alguns mais de 1.000.000 registrados como enviados tópico de toohello vários registros usando um script em uma etapa anterior.

6. Use __Ctrl + C__ tooexit consumidor de saudação.

### <a name="multiple-consumers"></a>Vários consumidores

Os consumidores do Kafka usam um grupo de consumidores ao ler os registros. Usando o mesmo grupo de saudação com vários consumidores resulta em carga equilibrada leituras de um tópico. Cada consumidor no grupo Olá recebe uma parte dos registros de saudação. toosee esse processo em ação, use Olá seguindo as etapas:

1. Abra um novo cluster de toohello de sessão SSH, para que você tenha duas delas. Em cada sessão, use Olá seguintes toostart um consumidor com Olá a mesma ID de grupo de consumidor:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    Esse comando inicia um consumidor usando uma ID de grupo Olá `mygroup`.

    > [!NOTE]
    > Usar os comandos de Olá Olá [obter informações de host Zookeeper e Broker Olá](#getkafkainfo) tooset seção `$KAFKABROKERS` para esta sessão SSH.

2. Observe como cada sessão contagens Olá registra recebe do tópico hello. total de saudação de ambas as sessões deve ser Olá mesmo que você recebeu anteriormente de um consumidor.

Consumo por clientes em Olá mesmo grupo é tratado por meio das partições Olá tópico hello. Para Olá `test` tópico criado anteriormente, ele tem oito partições. Se você abre oito sessões SSH e iniciar um consumidor em todas as sessões, cada consumidor lê os registros de uma única partição para o tópico de saudação.

> [!IMPORTANT]
> Não pode haver mais instâncias de consumidores do que partições em um grupo de consumidores. Neste exemplo, um grupo de consumidor pode conter a consumidores tooeight já que é o número de saudação de partições no tópico hello. Ou você pode ter vários grupos de consumidores, cada um com no máximo oito consumidores.

Registros armazenados em Kafka são armazenados em ordem de saudação que são recebidos em uma partição. tooachieve ordenados na entrega para registros *dentro de uma partição*, crie um grupo de consumidores, onde o número de Olá de instâncias de consumidor corresponde o número de saudação de partições. tooachieve ordenados na entrega para registros *tópico Olá*, criar um grupo de consumidores com a instância de apenas um consumidor.

## <a name="streaming-api"></a>API de streaming

Olá streaming API foi adicionado tooKafka na versão 0.10.0; versões anteriores dependem Apache Spark ou Storm para processamento de fluxo.

1. Se você ainda não fez isso, baixe os exemplos de saudação do [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour ambiente de desenvolvimento. Para Olá exemplo de transmissão, use o projeto Olá no Olá `streaming` directory.
   
    Este projeto contém apenas uma classe, `Stream`, que lê os registros de saudação `test` tópico criado anteriormente. Ele conta palavras Olá ler e emite cada tópico de tooa word e contagem chamado `wordcounts`. Olá `wordcounts` tópico é criado em uma etapa mais adiante nesta seção.

2. Na linha de comando de saudação em seu ambiente de desenvolvimento, alterar o local de toohello de diretórios da saudação `Streaming` diretório e, em seguida, use Olá comando toocreate um pacote jar a seguir:

    ```bash
    mvn clean package
    ```

    Esse comando cria um diretório chamado `target`, que contém um arquivo chamado `kafka-streaming-1.0-SNAPSHOT.jar`.

3. A seguir Olá use comandos Olá toocopy `kafka-streaming-1.0-SNAPSHOT.jar` cluster do HDInsight tooyour arquivo:
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    Substituir **SSHUSER** com usuário SSH Olá para o cluster e substituir **CLUSTERNAME** com nome de saudação do cluster. Quando solicitado que digite a senha de saudação do usuário SSH hello.

4. Uma vez Olá `scp` comando concluído a cópia do arquivo hello, conectar toohello cluster usando o SSH e, em seguida, usar Olá Olá de toocreate de comando a seguir `wordcounts` tópico:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. Em seguida, inicie Olá streaming processo usando o comando a seguir de saudação:
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    Esse comando inicia Olá processo em segundo plano da saudação de streaming.

6. Comando a seguir de saudação do uso toosend mensagens toohello `test` tópico. Essas mensagens são processadas pelo Olá streaming de exemplo:
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. Saudação de uso após a saída de saudação do comando tooview escrito toohello `wordcounts` tópico por Olá streaming processo:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > dados de saudação tooview, você deve informar o chave de Olá Olá consumidor tooprint e Olá desserializador toouse para Olá chave e valor. nome da chave Olá é palavra hello e valor de chave Olá contém a contagem de saudação.
   
    saudação de saída é similar toohello texto a seguir:
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > Contagem de saudação incrementado sempre que uma palavra é encontrada.

7. Use Olá __Ctrl + C__ tooexit Olá consumidor, em seguida, usar Olá `fg` comando toobring Olá primeiro plano streaming toohello voltar de tarefa em segundo plano. Use __Ctrl + C__ tooexit-lo também.

## <a name="delete-hello-cluster"></a>Excluir o cluster Olá

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Próximas etapas

Neste documento, você aprendeu os fundamentos de saudação do trabalho com o Apache Kafka no HDInsight. Use Olá toolearn mais sobre como trabalhar com Kafka a seguir:

* [Garantir a alta disponibilidade de seus dados com o Kafka no HDInsight](hdinsight-apache-kafka-high-availability.md)
* [Aumentar a escalabilidade, configurando discos gerenciados com o Kafka no HDInsight](hdinsight-apache-kafka-scalability.md)
* [Documentação do Apache Kafka](http://kafka.apache.org/documentation.html) em kafka.apache.org.
* [Use MirrorMaker toocreate uma réplica de Kafka no HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Usar Apache Storm com Kafka no HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Usar o Apache Spark com o Kafka no HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Conecte-se tooKafka por meio de uma rede Virtual do Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
