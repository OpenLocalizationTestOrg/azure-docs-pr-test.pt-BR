---
title: "tópicos do Apache Kafka aaaMirror - HDInsight do Azure | Microsoft Docs"
description: "Saiba como espelhamento do toouse Apache Kafka recurso toomaintain uma réplica de um Kafka no cluster HDInsight pelo espelhamento de cluster secundário de tooa de tópicos."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>Use tópicos de Apache Kafka tooreplicate MirrorMaker com Kafka no HDInsight (visualização)

Saiba como toouse Kafka Apache do espelhamento de cluster secundário do recurso tooreplicate tópicos tooa. O espelhamento pode ser executado como um processo contínuo ou intermitentemente usado como um método de migração de dados de um cluster tooanother.

Neste exemplo, o espelhamento é usado tooreplicate tópicos entre dois clusters de HDInsight. Ambos os clusters estão em uma rede Virtual do Azure no hello mesma região.

> [!WARNING]
> O espelhamento não deve ser considerado como uma meio tooachieve tolerância a falhas. Olá tooitems de deslocamento dentro de um tópico são diferentes entre clusters de origem e destino hello, para que clientes não poderão usar o hello dois alternadamente.
>
> Se você estiver preocupado com a tolerância a falhas, você deve definir a replicação para tópicos de saudação no cluster. Para obter mais informações, confira [Introdução ao Kafka no HDInsight](hdinsight-apache-kafka-get-started.md).

## <a name="how-kafka-mirroring-works"></a>Como funciona o espelhamento do Kafka

Espelhamento funciona usando Olá MirrorMaker ferramenta (parte do Apache Kafka) tooconsume registros de tópicos no cluster de origem hello e, em seguida, crie uma cópia local no cluster de destino hello. MirrorMaker usa uma (ou mais) *consumidores* que ler do cluster de origem Olá e um *produtor* que grava o cluster do toohello local (destino).

Olá diagrama a seguir ilustra o processo de espelhamento de saudação:

![Diagrama do processo de espelhamento de saudação](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

Apache Kafka no HDInsight não fornece acesso toohello serviço Kafka sobre Olá internet pública. Produtores Kafka ou os consumidores devem estar na Olá mesma rede virtual do Azure como nós Olá Olá cluster Kafka. Neste exemplo, Olá fonte Kafka e clusters de destino estão localizados em uma rede virtual do Azure. Olá diagrama a seguir mostra como a comunicação flui entre clusters de saudação:

![Diagrama de clusters Kafka de origem e destino em uma rede virtual do Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

clusters de origem e destino Olá podem ser diferentes em número de saudação de nós e partições e deslocamentos nos tópicos da saudação também são diferentes. Espelhamento mantém o valor de chave de saudação que é usado para particionamento, para que registro ordem é preservada em uma base por chave.

### <a name="mirroring-across-network-boundaries"></a>Espelhamento entre limites de rede

Se você precisar toomirror entre clusters de Kafka em redes diferentes, existem Olá considerações adicionais a seguir:

* **Gateways**: redes de saudação devem ser capaz de toocommunicate em Olá nível TCPIP.

* **A resolução de nome**: Olá Kafka clusters em cada rede deve ser capaz de tooconnect tooeach outros usando nomes de host. Isso pode exigir um servidor de sistema de nome de domínio (DNS) em cada rede que é configurado tooforward solicitações toohello outras redes.

    Ao criar uma rede Virtual do Azure, em vez de usar o hello que DNS automático fornecido com a rede hello, você deve especificar um DNS server e hello endereço IP personalizado para o servidor de saudação. Após Olá que rede Virtual tiver sido criada, você deve criar uma máquina Virtual do Azure que usa o endereço IP, em seguida, instale e configure software DNS nele.

    > [!WARNING]
    > Criar e configurar um servidor DNS personalizado Olá antes de instalar HDInsight Olá rede Virtual. Não há nenhuma configuração adicional necessária para o servidor DNS do HDInsight toouse Olá configurado para Olá rede Virtual.

Para obter mais informações sobre como conectar duas Redes Virtuais do Azure, confira [Configurar uma conexão de VNet para VNet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

## <a name="create-kafka-clusters"></a>Criar clusters Kafka

Embora você pode criar uma rede virtual do Azure e Kafka clusters manualmente, é mais fácil toouse um modelo do Gerenciador de recursos do Azure. Use Olá toodeploy as etapas a seguir, uma rede virtual do Azure e tooyour clusters de dois Kafka assinatura do Azure.

1. Use Olá botão toosign em tooAzure e modelo Olá abrir no portal do Azure de saudação a seguir.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello Azure Resource Manager modelo está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > disponibilidade de tooguarantee de Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho. Este modelo cria um cluster de Kafka que contém três nós de trabalho.

2. Olá usar entradas de saudação toopopulate informações a seguir no hello **implantação personalizada** folha:
    
    ![Implantação personalizada do HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **Grupo de recursos**: Crie um grupo ou selecione um existente. Esse grupo contém o cluster do HDInsight hello.

    * **Local**: selecione um tooyou geograficamente fechar do local.
     
    * **Nome do Cluster base**: esse valor é usado como nome base Olá Olá Kafka clusters. Por exemplo, inserir **hdi** cria clusters chamados **source-hdi** e **dest-hdi**.

    * **Nome de usuário de logon de cluster**: nome de usuário de administrador Olá para Olá origem e destino Kafka clusters.

    * **Senha de logon de cluster**: clusters de Kafka com a senha do usuário administrador Olá para Olá origem e destino.

    * **Nome de usuário SSH**: clusters de Kafka toocreate de usuário SSH Olá para Olá origem e destino.

    * **Senha SSH**: senha Olá para usuário SSH Olá Olá origem e destino Kafka clusters.

3. Saudação de leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições declaradas acima**.

4. Finalmente, verifique **Pin toodashboard** e, em seguida, selecione **compra**. Demora cerca de 20 minutos toocreate clusters hello.

Após a criação dos recursos Olá, será redirecionado tooa folha Olá grupo de recursos que contém hello e clusters do painel da web.

![Folha de grupo de recursos para redes hello e clusters](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> Observe que os nomes de saudação de clusters de HDInsight Olá ficam **nome base do código-fonte** e **dest-nome de base**, onde nome base é o nome da saudação fornecido toohello modelo. Você pode usar esses nomes em etapas posteriores ao conectar-se toohello clusters.

## <a name="create-topics"></a>Criar tópicos

1. Conecte-se toohello **fonte** cluster usando o SSH:

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    Substituir **sshuser** com nome de usuário SSH Olá usado ao criar o cluster de saudação. Substituir **nome base** com o nome de base Olá usado ao criar o cluster de saudação.

    Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. A seguir Olá use comandos hosts de Zookeeper toofind Olá para o cluster de origem hello:

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. Saudação de uso tooverify de comando que Olá tópico a seguir foi criada:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    Olá resposta contém `testtopic`.

4. Olá usar informações do host Zookeeper tooview Olá para este a seguir (Olá **origem**) cluster:

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    Isso retorna informações toohello semelhante texto a seguir:

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    Salve essas informações. Ele é usado na próxima seção, Olá.

## <a name="configure-mirroring"></a>Configurar o espelhamento

1. Conecte-se toohello **destino** usando uma sessão SSH diferente do cluster:

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    Substituir **sshuser** com nome de usuário SSH Olá usado ao criar o cluster de saudação. Substituir **nome base** com o nome de base Olá usado ao criar o cluster de saudação.

    Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Comando a seguir de saudação do uso toocreate um `consumer.properties` arquivo que descreve como toocommunicate com hello **fonte** cluster:

    ```bash
    nano consumer.properties
    ```

    Saudação de uso após o texto como conteúdo de saudação do hello `consumer.properties` arquivo:

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    Substituir **SOURCE_ZKHOSTS** com hello Zookeeper hospeda informações de saudação **fonte** cluster.

    Esse arquivo descreve Olá consumidor informações toouse durante a leitura da origem Olá cluster Kafka. Para obter mais informações de configuração do consumidor, confira [Configurações de Consumidor](https://kafka.apache.org/documentation#consumerconfigs) em kafka.apache.org.

    arquivo de saudação toosave, use **Ctrl + X**, **Y**e, em seguida, **Enter**.

3. Antes de configurar o produtor Olá que se comunica com o cluster de destino hello, você deve localizar broker Olá hosts Olá **destino** cluster. Use essas informações de saudação tooretrieve comandos a seguir:

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    Substituir `$PASSWORD` com senha de conta (admin) de logon Olá para cluster Olá.

    Substituir `$CLUSTERNAME` com o nome de saudação do cluster de destino hello.

    Estes comandos retornam a seguir toohello semelhante informações:

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. Saudação de uso a seguir toocreate uma `producer.properties` arquivo que descreve como toocommunicate com hello **destino** cluster:

    ```bash
    nano producer.properties
    ```

    Saudação de uso após o texto como conteúdo de saudação do hello `producer.properties` arquivo:

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    Substituir **DEST_BROKERS** com informações de agente de saudação da etapa anterior Olá.

    Para obter mais informações de configuração produtor, confira [Configurações de Produtor](https://kafka.apache.org/documentation#producerconfigs) em kafka.apache.org.

## <a name="start-mirrormaker"></a>Iniciar MirrorMaker

1. De saudação SSH conexão toohello **destino** de cluster, use Olá após comando toostart Olá MirrorMaker processo:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    Olá parâmetros usados neste exemplo são:

    * **– consumer.config**: Especifica o arquivo hello que contém propriedades de consumidor. Essas propriedades são usada toocreate um consumidor que lê da saudação *fonte* cluster Kafka.

    * **– producer.config**: Especifica o arquivo hello que contém propriedades de produtor. Essas propriedades são usada toocreate um produtor que grava toohello *destino* cluster Kafka.

    * **– lista branca**: uma lista de tópicos MirrorMaker replica de saudação origem cluster toohello destino.

    * **– num.streams**: Olá inúmeros toocreate de threads de consumidor.

 Na inicialização, MirrorMaker retorna informações toohello semelhante texto a seguir:

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. De saudação SSH conexão toohello **fonte** de cluster, use Olá após o comando toostart um produtor e enviar o tópico de toohello de mensagens:

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    Substituir `$PASSWORD` com a senha de logon (admin) Olá para o cluster de origem hello.

    Substituir `$CLUSTERNAME` com o nome de saudação do cluster de origem hello.

     Quando você chega a uma linha em branco com um cursor, digite algumas mensagens de texto. Esses são enviadas toohello tópico em Olá **fonte** cluster. Quando terminar, use **Ctrl + C** tooend processo de produtor de saudação.

3. De saudação SSH conexão toohello **destino** de cluster, use **Ctrl + C** Olá tooend MirrorMaker processo. Em seguida, a seguir Olá use comandos tooverify que Olá `testtopic` tópico foi criado, e esses dados no tópico Olá foram replicada toothis espelho:

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    Substituir `$PASSWORD` com a senha de logon (admin) Olá para o cluster de destino hello.

    Substituir `$CLUSTERNAME` com o nome de saudação do cluster de destino hello.

    Olá lista de tópicos agora inclui `testtopic`, que é criado quando MirrorMaster reflete o tópico de saudação do hello fonte cluster toohello de destino. mensagens de saudação recuperadas do tópico Olá são Olá mesmo inserido no cluster de origem hello.

## <a name="delete-hello-cluster"></a>Excluir o cluster Olá

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Como criam etapas de saudação neste documento hello de clusters no mesmo grupo de recursos do Azure, você pode excluir o grupo de recursos Olá Olá portal do Azure. Excluindo grupo de recursos de saudação remove todos os recursos criados seguindo este documento, Olá rede Virtual do Azure e conta de armazenamento usados pelo clusters hello.

## <a name="next-steps"></a>Próximas etapas

Neste documento, você aprendeu como toouse MirrorMaker toocreate de uma réplica de um Kafka cluster. Use Olá toodiscover links a seguir outra maneiras toowork Kafka:

* [Documentação do Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) em cwiki.apache.org.
* [Introdução ao Apache Kafka no HDInsight](hdinsight-apache-kafka-get-started.md)
* [Usar o Apache Spark com o Kafka no HDInsight](hdinsight-apache-spark-with-kafka.md)
* [Usar Apache Storm com Kafka no HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Conecte-se tooKafka por meio de uma rede Virtual do Azure](hdinsight-apache-kafka-connect-vpn-gateway.md)
