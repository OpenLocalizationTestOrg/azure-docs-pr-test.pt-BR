---
title: aaaApache Spark Streaming estruturado com Kafka - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Apache Spark streaming (DStream) tooget dados entrando ou saindo Kafka do Apache. Neste exemplo, você deve transmitir dados usando um bloco de anotações do Jupyter do Spark no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Use o Streaming Estruturado do Spark com o Kafka (versão prévia) no HDInsight

Saiba como toouse Spark estruturado fluxo de dados de tooread do Apache Kafka no Azure HDInsight.

O streaming estruturado do Spark é um mecanismo de processamento de fluxo baseado no Spark SQL. Ele permite que você tooexpress cálculos de streaming Olá igual a computação de lote em dados estáticos. Para obter mais informações sobre fluxo estruturado, consulte Olá [estruturado Streaming guia de programação [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) em Apache.org.

> [!IMPORTANT]
> Este exemplo usou o Spark 2.1 no HDInsight 3.6. O Streaming Estruturado é considerado __versão alfa__ no Spark 2.1.
>
> etapas de saudação neste documento criam um grupo de recursos do Azure que contém um Spark no HDInsight tanto um Kafka no cluster HDInsight. Esses agrupamentos são ambos localizados em uma rede Virtual do Azure, que permite Olá toodirectly de cluster do Spark Olá cluster Kafka se comunicam.
>
> Quando você concluir etapas Olá neste documento, lembre-se toodelete Olá clusters tooavoid em excesso encargos.

## <a name="create-hello-clusters"></a>Criar clusters de saudação

Apache Kafka no HDInsight não fornece acesso toohello Kafka agentes sobre Olá internet pública. Qualquer coisa que fala tooKafka deve estar no hello mesma rede virtual do Azure como nós Olá Olá cluster Kafka. Neste exemplo, Olá Kafka e clusters do Spark estão localizados em uma rede virtual do Azure. Olá diagrama a seguir mostra como a comunicação flui entre clusters de saudação:

![Diagrama de clusters Spark e Kafka em uma rede virtual do Azure](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Olá serviço Kafka é toocommunication limitado na rede virtual hello. Outros serviços em cluster hello, como SSH e Ambari, podem ser acessados pela Olá da internet. Para obter mais informações sobre portas públicas de saudação disponíveis com o HDInsight, consulte [portas e URIs usados por HDInsight](hdinsight-hadoop-port-settings-for-services.md).

Embora você possa criar uma rede virtual do Azure, Kafka e Spark clusters manualmente, é mais fácil toouse um modelo do Gerenciador de recursos do Azure. Toodeploy uma rede virtual do Azure, Kafka, as etapas a seguir do uso hello e Spark clusters tooyour assinatura do Azure.

1. Use Olá botão toosign em tooAzure e modelo Olá abrir no portal do Azure de saudação a seguir.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello Azure Resource Manager modelo está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Este modelo cria Olá recursos a seguir:

    * Um cluster Kafka no HDInsight 3.5.
    * Um cluster Spark no HDInsight 3.6.
    * Uma rede Virtual do Azure, que contém os clusters de HDInsight hello.

    > [!IMPORTANT]
    > notebook streaming estruturado Olá usado neste exemplo requer Spark no HDInsight 3.6. Se você usar uma versão anterior do Spark no HDInsight, você recebe erros ao usar o bloco de anotações de saudação.

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

Após a criação dos recursos Olá, você é redirecionado toohello folha de grupo de recursos.

![Folha de grupo de recursos para redes hello e clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Observe que os nomes de saudação de clusters de HDInsight Olá ficam **nome base do spark** e **kafka nome de base**, onde nome base é o nome da saudação fornecido toohello modelo. Você pode usar esses nomes em etapas posteriores ao conectar-se toohello clusters.

## <a name="get-hello-kafka-brokers"></a>Obter Olá Kafka agentes

o código neste exemplo Hello conecta toohello Kafka hosts no cluster Kafka de saudação do agente. toofind Olá hosts de broker Kafka, use Olá PowerShell ou Bash exemplo a seguir:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> Este exemplo espera `$PASSWORD` toocontain senha de saudação para logon de cluster Olá, e `$CLUSTERNAME` toocontain nome de saudação do hello cluster Kafka.
>
> Este exemplo usa Olá [jq](https://stedolan.github.io/jq/) dados do utilitário tooparse fora do documento JSON hello.

saudação de saída é similar toohello texto a seguir:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Salve essas informações, como ele é usado no hello seguintes seções deste documento.

## <a name="get-hello-notebooks"></a>Obter blocos de anotações de saudação

Olá código de exemplo hello descrito neste documento está disponível em [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-hello-notebooks"></a>Carregar os blocos de anotações de saudação

Use Olá seguir etapas tooupload Olá blocos de anotações de saudação projeto tooyour Spark no cluster HDInsight:

1. No navegador da web, conecte-se de anotações do Jupyter toohello em seu cluster Spark. Olá seguindo a URL, substitua `CLUSTERNAME` com nome de saudação do cluster Kafka:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    Quando solicitado, insira o logon de cluster da saudação (admin) e a senha usada ao criar cluster hello.

2. Olá superior direita da página Olá, use Olá __carregar__ saudação do botão tooupload __fluxo Tweets To_Kafka.ipynb__ cluster toohello de arquivos. Selecione __abrir__ toostart carregamento de saudação.

    ![Use Olá tooselect de botão de carregamento e carregar um bloco de anotações](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Selecione o arquivo de KafkaStreaming.ipynb Olá](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Localize Olá __fluxo Tweets To_Kafka.ipynb__ entrada na lista de saudação do blocos de anotações e selecione __carregar__ botão ao lado dela.

    ![Carregamento de saudação do uso botão ao lado de tooupload de entrada KafkaStreaming.ipynb Olá-servidor de notebook toohello](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. Repita as etapas de saudação do tooload de 1 a 3 __Spark-estruturado-Streaming-de-Kafka.ipynb__ notebook.

## <a name="load-tweets-into-kafka"></a>Carregar tweets no Kafka

Depois de carregar arquivos hello, selecionar Olá __fluxo Tweets To_Kafka.ipynb__ notebook de saudação do tooopen de entrada. Siga as etapas de Olá Olá notebook tooload tweets em Kafka.

## <a name="process-tweets-using-spark-structured-streaming"></a>Processar tweets usando o streaming estruturado do Spark

Olá home page do Jupyter Notebook, selecione Olá __Spark-estruturado-Streaming-de-Kafka.ipynb__ entrada. Siga as etapas de Olá Olá notebook tooload tweets de Kafka usando fluxo estruturado do Spark.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como toouse Spark estruturado Streaming, consulte Olá documentos toolearn mais sobre como trabalhar com Spark e Kafka a seguir:

* [Como toouse despertar streaming (DStream) com Kafka](hdinsight-apache-spark-with-kafka.md).
* [Iniciar com o bloco de anotações do Jupyter e Spark no HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md)