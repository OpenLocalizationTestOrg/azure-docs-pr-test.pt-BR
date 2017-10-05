---
title: "Introdução ao Apache Kafka - Azure HDInsight | Microsoft Docs"
description: "Saiba como criar um cluster do Apache Kafka no Azure HDInsight. Aprenda a criar tópicos, assinantes e consumidores."
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
ms.openlocfilehash: 03e6996f0f44e04978080b3bd267e924f342b7fc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="7e4e5-104">Introdução ao Apache Kafka (versão prévia) no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e4e5-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="7e4e5-105">Saiba como criar e usar um cluster do [Apache Kafka](https://kafka.apache.org) no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-105">Learn how to create and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="7e4e5-106">O Kafka é uma plataforma de streaming distribuída de software livre que está disponível com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="7e4e5-107">Ela é geralmente usada como um agente de mensagens, pois fornece funcionalidade semelhante a uma fila de mensagens para publicação e assinatura.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-107">It is often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="7e4e5-108">Atualmente, há duas versões do Kafka disponíveis com o HDInsight: 0.9.0 (HDInsight 3.4) e 0.10.0 (HDInsight 3.5 e 3.6).</span><span class="sxs-lookup"><span data-stu-id="7e4e5-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="7e4e5-109">As etapas neste documento pressupõem que você está usando o Kafka no HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-109">The steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="7e4e5-110">Criar um cluster Kafka</span><span class="sxs-lookup"><span data-stu-id="7e4e5-110">Create a Kafka cluster</span></span>

<span data-ttu-id="7e4e5-111">Use as seguintes etapas para criar um cluster Kafka no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-111">Use the following steps to create a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="7e4e5-112">No [portal do Azure](https://portal.azure.com), selecione **+ NOVO**, **Inteligência + Análises** e **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-112">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Criar um cluster HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="7e4e5-114">Em **Noções Básicas**, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-114">From **Basics**, enter the following information:</span></span>

    * <span data-ttu-id="7e4e5-115">**Nome do cluster**: o nome do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-115">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="7e4e5-116">**Assinatura**: selecione a assinatura a ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-116">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="7e4e5-117">**Nome de usuário de logon do cluster** e **Senha de logon do cluster**: logon ao acessar o cluster por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-117">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="7e4e5-118">Você pode usar essas credenciais para acessar serviços como a interface do usuário da Web do Ambari ou a API REST.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-118">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="7e4e5-119">**Nome de usuário do SSH (Secure Shell)**: o logon usado ao acessar o cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-119">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="7e4e5-120">Por padrão, a senha é a mesma do logon do cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-120">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="7e4e5-121">**Grupo de Recursos**: o grupo de recursos para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-121">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="7e4e5-122">**Local**: a região do Azure para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-122">**Location**: The Azure region to create the cluster in.</span></span>
   
 ![Escolha a assinatura](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="7e4e5-124">Selecione **Tipo de cluster** e defina os seguintes valores em **Configuração do cluster**:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-124">Select **Cluster type**, and then set the following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="7e4e5-125">**Tipo de Cluster**: Kafka</span><span class="sxs-lookup"><span data-stu-id="7e4e5-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="7e4e5-126">**Versão**: Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="7e4e5-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="7e4e5-127">**Camada de Cluster**: Padrão</span><span class="sxs-lookup"><span data-stu-id="7e4e5-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="7e4e5-128">Por fim, use o botão **Selecionar** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-128">Finally, use the **Select** button to save settings.</span></span>
     
 ![Selecione o tipo de cluster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="7e4e5-130">Depois de selecionar o tipo de cluster, use o botão __Selecionar__ para definir o tipo de cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-130">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="7e4e5-131">Em seguida, use o botão __Avançar__ para concluir a configuração básica.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-131">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="7e4e5-132">Em **Armazenamento**, selecione ou crie uma Conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="7e4e5-133">Para as etapas neste documento, deixe os outros campos com os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-133">For the steps in this document, leave the other fields at the default values.</span></span> <span data-ttu-id="7e4e5-134">Use o botão __Avançar__ para salvar a configuração de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-134">Use the __Next__ button to save storage configuration.</span></span>

    ![Definir as configurações de conta de armazenamento do HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="7e4e5-136">Em __Aplicativos (opcionais)__, selecione __Avançar__ para continuar.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-136">From __Applications (optional)__, select __Next__ to continue.</span></span> <span data-ttu-id="7e4e5-137">Nenhum aplicativo é necessário neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="7e4e5-138">Em __Tamanho do cluster__, selecione __Avançar__ para continuar.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-138">From __Cluster size__, select __Next__ to continue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="7e4e5-139">Para garantir a disponibilidade do Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Definir o tamanho do cluster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="7e4e5-141">A entrada dos **discos por nó de trabalho** controla a escalabilidade do Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-141">The **disks per worker node** entry controls the scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="7e4e5-142">Para saber mais, veja [Configurar o armazenamento e a escalabilidade do Kafka no HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="7e4e5-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="7e4e5-143">Em __Configurações avançadas__, selecione __Avançar__ para continuar.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-143">From __Advanced settings__, select __Next__ to continue.</span></span>

9. <span data-ttu-id="7e4e5-144">Em **Resumo**, examine a configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-144">From the **Summary**, review the configuration for the cluster.</span></span> <span data-ttu-id="7e4e5-145">Use os links __Editar__ para alterar as configurações que estão incorretas.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-145">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="7e4e5-146">Por fim, use o botão __Criar__ para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-146">Finally, use the__Create__ button to create the cluster.</span></span>
   
    ![Resumo da configuração do cluster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="7e4e5-148">Pode levar até 20 minutos para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-148">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="7e4e5-149">Conectar-se ao cluster</span><span class="sxs-lookup"><span data-stu-id="7e4e5-149">Connect to the cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e4e5-150">Ao executar as etapas a seguir, você deve usar um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-150">When performing the following steps, you must use an SSH client.</span></span> <span data-ttu-id="7e4e5-151">Para saber mais, consulte o documento [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7e4e5-151">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="7e4e5-152">No cliente, use o SSH para se conectar ao cluster:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-152">From your client, use SSH to connect to the cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="7e4e5-153">Substitua **SSHUSER** pelo nome de usuário SSH fornecido durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-153">Replace **SSHUSER** with the SSH username you provided during cluster creation.</span></span> <span data-ttu-id="7e4e5-154">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-154">Replace **CLUSTERNAME** with the name of the cluster.</span></span>

<span data-ttu-id="7e4e5-155">Quando solicitado, digite a senha usada para a conta SSH.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-155">When prompted, enter the password you used for the SSH account.</span></span>

<span data-ttu-id="7e4e5-156">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7e4e5-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="7e4e5-157"><a id="getkafkainfo"></a>Obter as informações de host do Zookeeper e Broker</span><span class="sxs-lookup"><span data-stu-id="7e4e5-157"><a id="getkafkainfo"></a>Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="7e4e5-158">Ao trabalhar com Kafka, você deve saber os dois valores de host; os hosts *Zookeeper* e os hosts *Broker*.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-158">When working with Kafka, you must know two host values; the *Zookeeper* hosts and the *Broker* hosts.</span></span> <span data-ttu-id="7e4e5-159">Esses hosts são usados com a API Kafka e muitos dos utilitários fornecidos com o Kafka.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-159">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="7e4e5-160">Use as etapas a seguir para criar variáveis de ambiente que contêm as informações de host.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-160">Use the following steps to create environment variables that contain the host information.</span></span> <span data-ttu-id="7e4e5-161">As variáveis de ambiente são usadas nas etapas deste documento.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-161">These environment variables are used in the steps in this document.</span></span>

1. <span data-ttu-id="7e4e5-162">Em uma conexão SSH ao cluster, use o comando a seguir para instalar o utilitário `jq`.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-162">From an SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="7e4e5-163">Esse utilitário é usado para analisar documentos JSON e é útil para recuperar as informações do host de agente:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-163">This utility is used to parse JSON documents, and is useful in retrieving the broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="7e4e5-164">Para definir as variáveis de ambiente com as informações recuperadas do Ambari, use os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-164">To set the environment variables with information retrieved from Ambari, use the following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="7e4e5-165">Defina `CLUSTERNAME=` para o nome do cluster do Kafka.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-165">Set `CLUSTERNAME=` to the name of the Kafka cluster.</span></span> <span data-ttu-id="7e4e5-166">Substitua `PASSWORD=` pela senha de logon (admin) que você usou ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-166">Set `PASSWORD=` to the login (admin) password you used when creating the cluster.</span></span>

    <span data-ttu-id="7e4e5-167">O seguinte texto é um exemplo do conteúdo de `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-167">The following text is an example of the contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="7e4e5-168">O seguinte texto é um exemplo do conteúdo de `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-168">The following text is an example of the contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="7e4e5-169">O comando `cut` é usado para cortar a lista de hosts em duas entradas de host.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-169">The `cut` command is used to trim the list of hosts to two host entries.</span></span> <span data-ttu-id="7e4e5-170">Você não precisa fornecer a lista completa de hosts ao criar um consumidor ou produtor do Kafka.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-170">You do not need to provide the full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="7e4e5-171">Não tome como certo que as informações retornadas nessa sessão sempre são precisas.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-171">Do not rely on the information returned from this session to always be accurate.</span></span> <span data-ttu-id="7e4e5-172">Se você dimensionar o cluster, novos agentes serão adicionados ou removidos.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-172">If you scale the cluster, new brokers are added or removed.</span></span> <span data-ttu-id="7e4e5-173">Se ocorrer uma falha e um nó for substituído, o nome do host para o nó poderá ser alterado.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-173">If a failure occurs and a node is replaced, the host name for the node may change.</span></span>
    >
    > <span data-ttu-id="7e4e5-174">Você deve recuperar as informações de hosts Zookeeper e de agente logo antes de usá-los para garantir que tenha informações válidas.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-174">You should retrieve the Zookeeper and broker hosts information shortly before you use it to ensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="7e4e5-175">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="7e4e5-175">Create a topic</span></span>

<span data-ttu-id="7e4e5-176">O Kafka armazena fluxos de dados em categorias chamadas *tópicos*.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="7e4e5-177">Em uma conexão SSH a um nó principal de cluster, use um script fornecido com o Kafka para criar um tópico:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-177">From An SSH connection to a cluster headnode, use a script provided with Kafka to create a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="7e4e5-178">Esse comando conecta ao Zookeeper usando as informações de host armazenadas em `$KAFKAZKHOSTS` e cria um tópico do Kafka chamado **teste**.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-178">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="7e4e5-179">Você pode verificar se o tópico foi criado usando o seguinte script para listar tópicos:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-179">You can verify that the topic was created by using the following script to list topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="7e4e5-180">A saída desse comando lista os tópicos do Kafka, que contém o tópico **teste**.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-180">The output of this command lists Kafka topics, which contains the **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="7e4e5-181">Produzir e consumir registros</span><span class="sxs-lookup"><span data-stu-id="7e4e5-181">Produce and consume records</span></span>

<span data-ttu-id="7e4e5-182">O Kafka armazena *registros* nos tópicos.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="7e4e5-183">Os registros são produzidos por *produtores* e consumidos por *consumidores*.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="7e4e5-184">Os produtores recuperam registros de *agentes* do Kafka.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="7e4e5-185">Cada nó de trabalho no cluster HDInsight é um agente do Kafka.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="7e4e5-186">Use as seguintes etapas para armazenar registros no tópico teste criado anteriormente e lê-los usando um consumidor:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-186">Use the following steps to store records into the test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="7e4e5-187">Na sessão SSH, use um script fornecido com o Kafka para gravar registros no tópico:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-187">From the SSH session, use a script provided with Kafka to write records to the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="7e4e5-188">Você não é levado ao prompt após esse comando.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-188">You are not returned to the prompt after this command.</span></span> <span data-ttu-id="7e4e5-189">Em vez disso, digite algumas mensagens de texto e use **Ctrl + C** para deixar de enviar ao tópico.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-189">Instead, type a few text messages and then use **Ctrl + C** to stop sending to the topic.</span></span> <span data-ttu-id="7e4e5-190">Cada linha é enviada como um registro separado.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="7e4e5-191">Use um script fornecido com o Kafka para ler registros do tópico:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-191">Use a script provided with Kafka to read records from the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="7e4e5-192">Esse comando recupera os registros do tópico e os exibe.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-192">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="7e4e5-193">O uso de `--from-beginning` instrui o consumidor a começar do início do fluxo, para que todos os registros sejam recuperados.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-193">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="7e4e5-194">Use __Ctrl + C__ para interromper o consumidor.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-194">Use __Ctrl + C__ to stop the consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="7e4e5-195">API de produtor e consumidor</span><span class="sxs-lookup"><span data-stu-id="7e4e5-195">Producer and consumer API</span></span>

<span data-ttu-id="7e4e5-196">Você pode também produzir e consumir registros de forma programática usando as [APIs Kafka](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="7e4e5-196">You can also programmatically produce and consume records using the [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="7e4e5-197">Para criar um produtor e consumidor do Java, use as seguintes etapas do ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-197">To build a Java producer and consumer, use the following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e4e5-198">Você deve ter os seguintes componentes instalados no ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-198">You must have the following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="7e4e5-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou equivalente, como OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="7e4e5-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="7e4e5-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="7e4e5-201">Um cliente SSH e o comando `scp`.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-201">An SSH client and the `scp` command.</span></span> <span data-ttu-id="7e4e5-202">Para saber mais, consulte o documento [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7e4e5-202">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="7e4e5-203">Baixe os exemplos de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="7e4e5-203">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="7e4e5-204">Para o exemplo de produtor/consumidor, use o projeto no diretório `Producer-Consumer`.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-204">For the producer/consumer example, use the project in the `Producer-Consumer` directory.</span></span> <span data-ttu-id="7e4e5-205">Esse exemplo contém as seguintes classes:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-205">This example contains the following classes:</span></span>
   
    * <span data-ttu-id="7e4e5-206">**Executar** - inicia o cliente ou o produtor.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-206">**Run** - starts either the consumer or producer.</span></span>

    * <span data-ttu-id="7e4e5-207">**Produtor** - armazena 1.000.000 registros para o tópico.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-207">**Producer** - stores 1,000,000 records to the topic.</span></span>

    * <span data-ttu-id="7e4e5-208">**Consumidor** - lê registros do tópico.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-208">**Consumer** - reads records from the topic.</span></span>

2. <span data-ttu-id="7e4e5-209">Para criar um pacote jar, altere os diretórios para o local do diretório `Producer-Consumer` e use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-209">To create a jar package, change directories to the location of the `Producer-Consumer` directory and use the following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="7e4e5-210">Esse comando cria um diretório chamado `target`, que contém um arquivo chamado `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="7e4e5-211">Use os seguintes comandos para copiar o arquivo `kafka-producer-consumer-1.0-SNAPSHOT.jar` para o cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-211">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="7e4e5-212">Substitua **SSHUSER** pelo usuário do SSH do cluster e substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-212">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="7e4e5-213">Quando solicitado, insira a senha do usuário do SSH.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-213">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="7e4e5-214">Após o comando `scp` terminar de copiar o arquivo, conecte-se ao cluster usando SSH.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-214">Once the `scp` command finishes copying the file, connect to the cluster using SSH.</span></span> <span data-ttu-id="7e4e5-215">Use o seguinte comando para gravar os registros para o tópico de teste:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-215">Use the following command to write records to the test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="7e4e5-216">Quando o processo for concluído, use o seguinte comando para ler do tópico:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-216">Once the process has finished, use the following command to read from the topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="7e4e5-217">São exibidos os registros lidos, juntamente com uma contagem de registros.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-217">The records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="7e4e5-218">É possível ver pouco mais de 1.000.000 registros, pois você envia vários registros ao tópico usando um script em uma etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-218">You may see a few more than 1,000,000 logged as you sent several records to the topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="7e4e5-219">Use __Ctrl + C__ para sair do consumidor.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-219">Use __Ctrl + C__ to exit the consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="7e4e5-220">Vários consumidores</span><span class="sxs-lookup"><span data-stu-id="7e4e5-220">Multiple consumers</span></span>

<span data-ttu-id="7e4e5-221">Os consumidores do Kafka usam um grupo de consumidores ao ler os registros.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="7e4e5-222">Usar o mesmo grupo com vários consumidores resulta em leituras de balanceamento de carga de um tópico.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-222">Using the same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="7e4e5-223">Cada consumidor no grupo recebe uma parte dos registros.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-223">Each consumer in the group receives a portion of the records.</span></span> <span data-ttu-id="7e4e5-224">Para ver esse processo em ação, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-224">To see this process in action, use the following steps:</span></span>

1. <span data-ttu-id="7e4e5-225">Abra uma nova sessão do SSH para o cluster, para que você tenha duas.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-225">Open a new SSH session to the cluster, so that you have two of them.</span></span> <span data-ttu-id="7e4e5-226">Em cada sessão, use o seguinte para iniciar um consumidor com a mesma ID do grupo de consumidores:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-226">In each session, use the following to start a consumer with the same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="7e4e5-227">Esse comando inicia um consumidor usando a ID do grupo `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-227">This command starts a consumer using the group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7e4e5-228">Use os comandos da seção [Obter as informações de host do Zookeeper e do Agente](#getkafkainfo) para definir `$KAFKABROKERS` para essa sessão de SSH.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-228">Use the commands in the [Get the Zookeeper and Broker host information](#getkafkainfo) section to set `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="7e4e5-229">Observe como cada sessão conta os registros que recebe do tópico.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-229">Watch as each session counts the records it receives from the topic.</span></span> <span data-ttu-id="7e4e5-230">O total de ambas as sessões deve ser o mesmo que você recebeu anteriormente de um consumidor.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-230">The total of both sessions should be the same as you received previously from one consumer.</span></span>

<span data-ttu-id="7e4e5-231">O consumo por clientes no mesmo grupo é manipulado por meio das partições do tópico.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-231">Consumption by clients within the same group is handled through the partitions for the topic.</span></span> <span data-ttu-id="7e4e5-232">O tópico `test` criado anteriormente tem oito partições.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-232">For the `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="7e4e5-233">Se você abrir oito sessões do SSH e iniciar um consumidor em todas elas, cada consumidor lerá os registros de uma única partição do tópico.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for the topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e4e5-234">Não pode haver mais instâncias de consumidores do que partições em um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="7e4e5-235">Neste exemplo, um grupo de consumidores pode conter até oito consumidores, já que esse é o número de partições no tópico.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-235">In this example, one consumer group can contain up to eight consumers since that is the number of partitions in the topic.</span></span> <span data-ttu-id="7e4e5-236">Ou você pode ter vários grupos de consumidores, cada um com no máximo oito consumidores.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="7e4e5-237">Os registros armazenados no Kafka são armazenados na ordem em que são recebidos em uma partição.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-237">Records stored in Kafka are stored in the order they are received within a partition.</span></span> <span data-ttu-id="7e4e5-238">Para garantir a entrega ordenada em registros *em uma partição*, crie um grupo de consumidores em que o número de instâncias de consumidor corresponda ao número de partições.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-238">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span></span> <span data-ttu-id="7e4e5-239">Para garantir a entrega ordenada em registros *no tópico*, crie um grupo de consumidores com apenas uma instância de consumidor.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-239">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="7e4e5-240">API de streaming</span><span class="sxs-lookup"><span data-stu-id="7e4e5-240">Streaming API</span></span>

<span data-ttu-id="7e4e5-241">A API de streaming foi adicionada ao Kafka na versão 0.10.0. Versões anteriores usam o Apache Spark ou o Storm para processamento de fluxo.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-241">The streaming API was added to Kafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="7e4e5-242">Se ainda não tiver feito isso, baixe os exemplos de [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) para seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-242">If you haven't already done so, download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) to your development environment.</span></span> <span data-ttu-id="7e4e5-243">Para o exemplo de streaming, use o projeto no diretório `streaming`.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-243">For the streaming example, use the project in the `streaming` directory.</span></span>
   
    <span data-ttu-id="7e4e5-244">Esse projeto contém apenas uma classe, `Stream`, que lê registros do tópico `test` criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-244">This project contains only one class, `Stream`, which reads records from the `test` topic created previously.</span></span> <span data-ttu-id="7e4e5-245">Ele conta as palavras lidas e emite cada palavra e contagem para um tópico chamado `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-245">It counts the words read, and emits each word and count to a topic named `wordcounts`.</span></span> <span data-ttu-id="7e4e5-246">O tópico `wordcounts` é criado em uma etapa posterior desta seção.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-246">The `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="7e4e5-247">Na linha de comando no ambiente de desenvolvimento, altere os diretórios para o local do diretório `Streaming` e use o seguinte comando para criar um pacote jar:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-247">From the command line in your development environment, change directories to the location of the `Streaming` directory, and then use the following command to create a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="7e4e5-248">Esse comando cria um diretório chamado `target`, que contém um arquivo chamado `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="7e4e5-249">Use os seguintes comandos para copiar o arquivo `kafka-streaming-1.0-SNAPSHOT.jar` para o cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-249">Use the following commands to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="7e4e5-250">Substitua **SSHUSER** pelo usuário do SSH do cluster e substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-250">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="7e4e5-251">Quando solicitado, insira a senha do usuário do SSH.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-251">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="7e4e5-252">Quando o comando `scp` terminar de copiar o arquivo, conecte-se ao cluster usando SSH e use o seguinte comando para criar o tópico `wordcounts`:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-252">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following command to create the `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="7e4e5-253">Em seguida, inicie o processo de streaming usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-253">Next, start the streaming process by using the following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="7e4e5-254">Esse comando inicia o processo de streaming em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-254">This command starts the streaming process in the background.</span></span>

6. <span data-ttu-id="7e4e5-255">Use o comando a seguir para enviar mensagens ao tópico `test`.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-255">Use the following command to send messages to the `test` topic.</span></span> <span data-ttu-id="7e4e5-256">Estas mensagens são processadas pelo exemplo de streaming:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-256">These messages are processed by the streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="7e4e5-257">Use o seguinte comando para exibir a saída é gravada para o `wordcounts` tópico pelo processo de streaming:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-257">Use the following command to view the output that is written to the `wordcounts` topic by the streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="7e4e5-258">Para exibir os dados, você deve instruir o consumidor a imprimir a chave e o desserializador a ser usado para a chave e o valor.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-258">To view the data, you must tell the consumer to print the key and the deserializer to use for the key and value.</span></span> <span data-ttu-id="7e4e5-259">O nome da chave é a palavra e o valor da chave contém a contagem.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-259">The key name is the word, and the key value contains the count.</span></span>
   
    <span data-ttu-id="7e4e5-260">A saída é semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-260">The output is similar to the following text:</span></span>
   
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
    > <span data-ttu-id="7e4e5-261">A contagem é incrementada sempre que uma palavra é encontrada.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-261">The count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="7e4e5-262">Use __Ctrl + C__ para sair do consumidor e use o comando `fg` para colocar a tarefa de streaming em segundo plano novamente em primeiro plano.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-262">Use the __Ctrl + C__ to exit the consumer, then use the `fg` command to bring the streaming background task back to the foreground.</span></span> <span data-ttu-id="7e4e5-263">Use __Ctrl + C__ para sair dela também.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-263">Use __Ctrl + C__ to exit it also.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="7e4e5-264">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="7e4e5-264">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="7e4e5-265">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="7e4e5-265">Troubleshoot</span></span>

<span data-ttu-id="7e4e5-266">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="7e4e5-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e4e5-267">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e4e5-267">Next steps</span></span>

<span data-ttu-id="7e4e5-268">Neste documento, você aprendeu os fundamentos do trabalho com o Apache Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-268">In this document, you have learned the basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="7e4e5-269">Confira o seguinte para obter mais informações sobre como trabalhar com o Kafka:</span><span class="sxs-lookup"><span data-stu-id="7e4e5-269">Use the following to learn more about working with Kafka:</span></span>

* [<span data-ttu-id="7e4e5-270">Garantir a alta disponibilidade de seus dados com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e4e5-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="7e4e5-271">Aumentar a escalabilidade, configurando discos gerenciados com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e4e5-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="7e4e5-272">[Documentação do Apache Kafka](http://kafka.apache.org/documentation.html) em kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="7e4e5-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="7e4e5-273">Usar MirrorMaker para criar uma réplica de Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e4e5-273">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="7e4e5-274">Usar Apache Storm com Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e4e5-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="7e4e5-275">Usar o Apache Spark com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e4e5-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="7e4e5-276">Conectar-se ao Kafka no HDInsight (preview) por meio de uma Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="7e4e5-276">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
