---
title: aaaApache Spark streaming com Kafka - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse dados de toostream Spark Apache Spark entrando ou saindo Apache Kafka usando DStreams. Neste exemplo, você deve transmitir dados usando um bloco de anotações do Jupyter do Spark no HDInsight."
keywords: exemplo de kafka, zookeeper kafka, streaming do kafka para Spark, exemplo de streaming do spark com o kafka
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>Exemplo de streaming do Apache Spark (DStream) com o Kafka (versão prévia) no HDInsight

Saiba como toouse dados de toostream Spark Apache Spark entrando ou saindo Kafka do Apache no HDInsight usando DStreams. Este exemplo usa um bloco de anotações do Jupyter que é executado no cluster do Spark hello.
> [!NOTE]
> etapas de saudação neste documento criam um grupo de recursos do Azure que contém um Spark no HDInsight tanto um Kafka no cluster HDInsight. Esses agrupamentos são ambos localizados em uma rede Virtual do Azure, que permite Olá toodirectly de cluster do Spark Olá cluster Kafka se comunicam.
>
> Quando você concluir etapas Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.

## <a name="create-hello-clusters"></a>Criar clusters de saudação

Apache Kafka no HDInsight não fornece acesso toohello Kafka agentes sobre Olá internet pública. Qualquer coisa que fala tooKafka deve estar no hello mesma rede virtual do Azure como nós Olá Olá cluster Kafka. Neste exemplo, Olá Kafka e clusters do Spark estão localizados em uma rede virtual do Azure. Olá diagrama a seguir mostra como a comunicação flui entre clusters de saudação:

![Diagrama de clusters Spark e Kafka em uma rede virtual do Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Embora Kafka em si é toocommunication limitado na rede virtual hello, outros serviços em cluster hello como SSH e Ambari podem ser acessados pela Olá da internet. Para obter mais informações sobre portas públicas de saudação disponíveis com o HDInsight, consulte [portas e URIs usados por HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Embora você possa criar uma rede virtual do Azure, Kafka e Spark clusters manualmente, é mais fácil toouse um modelo do Gerenciador de recursos do Azure. Toodeploy uma rede virtual do Azure, Kafka, as etapas a seguir do uso hello e Spark clusters tooyour assinatura do Azure.

1. Use Olá botão toosign em tooAzure e modelo Olá abrir no portal do Azure de saudação a seguir.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello Azure Resource Manager modelo está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > disponibilidade de tooguarantee de Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho. Este modelo cria um cluster de Kafka que contém três nós de trabalho.

    Este modelo cria um cluster HDInsight 3.6 para Kafka e Spark.

2. Olá usar entradas de saudação toopopulate informações a seguir no hello **implantação personalizada** folha:
   
    ![Implantação personalizada do HDInsight](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Grupo de recursos**: Crie um grupo ou selecione um existente. Esse grupo contém o cluster do HDInsight hello.

    * **Local**: selecione um tooyou geograficamente fechar do local.

    * **Nome do Cluster base**: esse valor é usado como nome de base Olá para clusters de saudação Spark e Kafka. Por exemplo, inserir **hdi** cria um cluster Spark chamado hdi__ spark e um cluster Kafka chamado **kafka hdi**.

    * **Nome de usuário de logon de cluster**: nome de usuário de administrador Olá para clusters de saudação Spark e Kafka.

    * **Senha de logon de cluster**: senha do usuário administrador Olá para clusters de saudação Spark e Kafka.

    * **Nome de usuário SSH**: Olá toocreate de usuário SSH para clusters de saudação Spark e Kafka.

    * **Senha SSH**: senha Olá para usuário SSH Olá Olá Spark e Kafka clusters.

3. Saudação de leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições declaradas acima**.

4. Finalmente, verifique **Pin toodashboard** e, em seguida, selecione **compra**. Demora cerca de 20 minutos toocreate clusters hello.

Após a criação dos recursos Olá, será redirecionado tooa folha Olá grupo de recursos que contém hello e clusters do painel da web.

![Folha de grupo de recursos para redes hello e clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Observe que os nomes de saudação de clusters de HDInsight Olá ficam **nome base do spark** e **kafka nome de base**, onde nome base é o nome da saudação fornecido toohello modelo. Você pode usar esses nomes em etapas posteriores ao conectar-se toohello clusters.

## <a name="use-hello-notebooks"></a>Usar blocos de anotações de saudação

Olá código de exemplo hello descrito neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).

Siga as etapas de Olá Olá `README.md` arquivo toocomplete neste exemplo.

## <a name="delete-hello-cluster"></a>Excluir o cluster Olá

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Como criam etapas de saudação neste documento hello de clusters no mesmo grupo de recursos do Azure, você pode excluir o grupo de recursos Olá Olá portal do Azure. Excluir grupo de saudação remove todos os recursos criados seguindo este documento, Olá rede Virtual do Azure e conta de armazenamento usados pelo clusters hello.

## <a name="next-steps"></a>Próximas etapas

Neste exemplo, você aprendeu como toouse despertar tooread e gravar tooKafka. Use Olá toodiscover links a seguir outra maneiras toowork Kafka:

* [Introdução ao Apache Kafka no HDInsight](hdinsight-apache-kafka-get-started.md)
* [Use MirrorMaker toocreate uma réplica de Kafka no HDInsight](hdinsight-apache-kafka-mirroring.md)
* [Usar Apache Storm com Kafka no HDInsight](hdinsight-apache-storm-with-kafka.md)

