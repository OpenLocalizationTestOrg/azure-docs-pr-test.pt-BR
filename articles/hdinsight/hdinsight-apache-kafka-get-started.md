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
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="91009-104">Introdução ao Apache Kafka (versão prévia) no HDInsight</span><span class="sxs-lookup"><span data-stu-id="91009-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="91009-105">Saiba como toocreate e usar um [Kafka Apache](https://kafka.apache.org) cluster no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="91009-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="91009-106">O Kafka é uma plataforma de streaming distribuída de software livre que está disponível com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="91009-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="91009-107">Ele geralmente é usado como um agente de mensagem, pois ela fornece funcionalidade semelhante tooa publicação / assinatura fila de mensagens.</span><span class="sxs-lookup"><span data-stu-id="91009-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="91009-108">Atualmente, há duas versões do Kafka disponíveis com o HDInsight: 0.9.0 (HDInsight 3.4) e 0.10.0 (HDInsight 3.5 e 3.6).</span><span class="sxs-lookup"><span data-stu-id="91009-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="91009-109">etapas de saudação neste documento pressupõem que você esteja usando Kafka em HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="91009-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="91009-110">Criar um cluster Kafka</span><span class="sxs-lookup"><span data-stu-id="91009-110">Create a Kafka cluster</span></span>

<span data-ttu-id="91009-111">Use Olá seguindo as etapas toocreate um Kafka no cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="91009-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="91009-112">De saudação [portal do Azure](https://portal.azure.com), selecione **+ novo**, **Intelligence + análise**e, em seguida, selecione **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="91009-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Criar um cluster HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="91009-114">De **Noções básicas de**, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="91009-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="91009-115">**Nome do cluster**: nome de saudação do cluster do HDInsight de saudação.</span><span class="sxs-lookup"><span data-stu-id="91009-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="91009-116">**Assinatura**: selecione Olá toouse de assinatura.</span><span class="sxs-lookup"><span data-stu-id="91009-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="91009-117">**Nome de usuário de logon de cluster** e **senha de logon de Cluster**: logon Olá ao acessar o cluster Olá via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="91009-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="91009-118">Você usa esses serviços de tooaccess de credenciais como saudação da interface do usuário do Ambari Web ou a API REST.</span><span class="sxs-lookup"><span data-stu-id="91009-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="91009-119">**Secure Shell (SSH) username**: logon Olá usado ao acessar o cluster Olá via SSH.</span><span class="sxs-lookup"><span data-stu-id="91009-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="91009-120">Por padrão senha Olá é Olá igual à senha de logon de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="91009-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="91009-121">**Grupo de recursos**: Olá recurso grupo toocreate Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="91009-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="91009-122">**Local**: Olá região do Azure toocreate Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="91009-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![Escolha a assinatura](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="91009-124">Selecione **tipo de Cluster**, e, em seguida, Olá conjunto seguindo os valores de **configuração de Cluster**:</span><span class="sxs-lookup"><span data-stu-id="91009-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="91009-125">**Tipo de Cluster**: Kafka</span><span class="sxs-lookup"><span data-stu-id="91009-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="91009-126">**Versão**: Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="91009-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="91009-127">**Camada de Cluster**: Padrão</span><span class="sxs-lookup"><span data-stu-id="91009-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="91009-128">Por fim, use Olá **selecione** toosave configurações de botão.</span><span class="sxs-lookup"><span data-stu-id="91009-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![Selecione o tipo de cluster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="91009-130">Depois de selecionar o tipo de cluster hello, use Olá __selecione__ tooset Olá cluster tipo de botão.</span><span class="sxs-lookup"><span data-stu-id="91009-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="91009-131">Em seguida, use Olá __próximo__ configuração básica do botão toofinish.</span><span class="sxs-lookup"><span data-stu-id="91009-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="91009-132">Em **Armazenamento**, selecione ou crie uma Conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="91009-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="91009-133">Para obter etapas Olá neste documento, deixe Olá outros campos com valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="91009-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="91009-134">Saudação de uso __próximo__ configuração de armazenamento de toosave do botão.</span><span class="sxs-lookup"><span data-stu-id="91009-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Definir configurações de conta de armazenamento Olá para HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="91009-136">De __aplicativos (opcionais)__, selecione __próximo__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="91009-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="91009-137">Nenhum aplicativo é necessário neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="91009-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="91009-138">De __tamanho do Cluster__, selecione __próximo__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="91009-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="91009-139">disponibilidade de tooguarantee de Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="91009-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Saudação de conjunto de tamanho do cluster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="91009-141">Olá **discos por nó de trabalho** controles de entrada hello escalabilidade de Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="91009-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="91009-142">Para saber mais, veja [Configurar o armazenamento e a escalabilidade do Kafka no HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="91009-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="91009-143">De __configurações avançadas__, selecione __próximo__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="91009-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="91009-144">De saudação **resumo**, examine a configuração Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="91009-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="91009-145">Saudação de uso __editar__ links toochange todas as configurações que estão incorretas.</span><span class="sxs-lookup"><span data-stu-id="91009-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="91009-146">Por fim, use o cluster de saudação do the__Create__ botão toocreate.</span><span class="sxs-lookup"><span data-stu-id="91009-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![Resumo da configuração do cluster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="91009-148">Pode demorar até o cluster de saudação de toocreate too20 minutos.</span><span class="sxs-lookup"><span data-stu-id="91009-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="91009-149">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="91009-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91009-150">Ao executar Olá etapas a seguir, você deve usar um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="91009-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="91009-151">Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="91009-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="91009-152">De seu cliente, use SSH tooconnect toohello cluster:</span><span class="sxs-lookup"><span data-stu-id="91009-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="91009-153">Substituir **SSHUSER** com nome de usuário SSH Olá fornecido durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="91009-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="91009-154">Substituir **CLUSTERNAME** com o nome de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="91009-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="91009-155">Quando solicitado, insira a senha Olá usada Olá conta SSH.</span><span class="sxs-lookup"><span data-stu-id="91009-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="91009-156">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="91009-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="91009-157"><a id="getkafkainfo"></a>Obter informações de saudação Zookeeper e agente de host</span><span class="sxs-lookup"><span data-stu-id="91009-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="91009-158">Ao trabalhar com Kafka, você deve saber os dois valores de host; Olá *Zookeeper* hosts e hello *Broker* hosts.</span><span class="sxs-lookup"><span data-stu-id="91009-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="91009-159">Esses hosts são usados com hello Kafka API e muitos utilitários Olá que vêm com Kafka.</span><span class="sxs-lookup"><span data-stu-id="91009-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="91009-160">As etapas a seguir de saudação de uso toocreate variáveis de ambiente que contêm informações de host de saudação.</span><span class="sxs-lookup"><span data-stu-id="91009-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="91009-161">Essas variáveis de ambiente são usadas nas etapas Olá neste documento.</span><span class="sxs-lookup"><span data-stu-id="91009-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="91009-162">De um cluster de toohello de conexão SSH, Olá tooinstall de comando de uso a seguir de Olá `jq` utilitário.</span><span class="sxs-lookup"><span data-stu-id="91009-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="91009-163">Esse utilitário é usado tooparse documentos JSON e é útil para recuperar informações do host de agente Olá:</span><span class="sxs-lookup"><span data-stu-id="91009-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="91009-164">variáveis de ambiente Olá tooset com informações recuperada do Ambari, Olá use comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="91009-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="91009-165">Definir `CLUSTERNAME=` toohello nome da saudação cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="91009-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="91009-166">Definir `PASSWORD=` toohello senha de logon (admin) usado durante a criação de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="91009-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="91009-167">Olá, texto a seguir é um exemplo do conteúdo de saudação do `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="91009-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="91009-168">Olá, texto a seguir é um exemplo do conteúdo de saudação do `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="91009-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="91009-169">Olá `cut` comando é a lista de saudação de tootrim usadas de entradas de host tootwo hosts.</span><span class="sxs-lookup"><span data-stu-id="91009-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="91009-170">Lista completa de saudação de tooprovide de hosts não é necessário durante a criação de um consumidor de Kafka ou o produtor.</span><span class="sxs-lookup"><span data-stu-id="91009-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="91009-171">Não se baseiam nas informações de saudação retornadas desta sessão tooalways sejam precisas.</span><span class="sxs-lookup"><span data-stu-id="91009-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="91009-172">Se você expandir o cluster hello, os novos agentes são adicionados ou removidos.</span><span class="sxs-lookup"><span data-stu-id="91009-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="91009-173">Se ocorrer uma falha e um nó for substituído, nome do host Olá para o nó de saudação pode mudar.</span><span class="sxs-lookup"><span data-stu-id="91009-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="91009-174">Deve recuperar informações de hosts de Zookeeper e agente Olá logo antes de usá-lo tooensure tem informações válidas.</span><span class="sxs-lookup"><span data-stu-id="91009-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="91009-175">Criar um tópico</span><span class="sxs-lookup"><span data-stu-id="91009-175">Create a topic</span></span>

<span data-ttu-id="91009-176">O Kafka armazena fluxos de dados em categorias chamadas *tópicos*.</span><span class="sxs-lookup"><span data-stu-id="91009-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="91009-177">De um SSH conexão tooa cluster um nó principal, use um script fornecido com Kafka toocreate um tópico:</span><span class="sxs-lookup"><span data-stu-id="91009-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="91009-178">Esse comando conecta tooZookeeper usando Olá host informações armazenadas em `$KAFKAZKHOSTS`e, em seguida, criar tópico Kafka chamado **teste**.</span><span class="sxs-lookup"><span data-stu-id="91009-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="91009-179">Você pode verificar que esse tópico Olá foi criado usando Olá tópicos toolist de script a seguir:</span><span class="sxs-lookup"><span data-stu-id="91009-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="91009-180">Olá saída desse comando lista Kafka tópicos, que contém a saudação **teste** tópico.</span><span class="sxs-lookup"><span data-stu-id="91009-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="91009-181">Produzir e consumir registros</span><span class="sxs-lookup"><span data-stu-id="91009-181">Produce and consume records</span></span>

<span data-ttu-id="91009-182">O Kafka armazena *registros* nos tópicos.</span><span class="sxs-lookup"><span data-stu-id="91009-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="91009-183">Os registros são produzidos por *produtores* e consumidos por *consumidores*.</span><span class="sxs-lookup"><span data-stu-id="91009-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="91009-184">Os produtores recuperam registros de *agentes* do Kafka.</span><span class="sxs-lookup"><span data-stu-id="91009-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="91009-185">Cada nó de trabalho no cluster HDInsight é um agente do Kafka.</span><span class="sxs-lookup"><span data-stu-id="91009-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="91009-186">Use Olá registros de toostore as etapas a seguir no tópico de teste Olá você criou anteriormente e, em seguida, lê-los usando um consumidor:</span><span class="sxs-lookup"><span data-stu-id="91009-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="91009-187">Da sessão SSH Olá, use um script fornecido com o tópico de toohello Kafka toowrite registros:</span><span class="sxs-lookup"><span data-stu-id="91009-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="91009-188">Você não retornará toohello prompt após esse comando.</span><span class="sxs-lookup"><span data-stu-id="91009-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="91009-189">Em vez disso, digite algumas mensagens de texto e, em seguida, use **Ctrl + C** toostop enviar toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="91009-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="91009-190">Cada linha é enviada como um registro separado.</span><span class="sxs-lookup"><span data-stu-id="91009-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="91009-191">Use um script fornecido com registros de tooread Kafka tópico hello:</span><span class="sxs-lookup"><span data-stu-id="91009-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="91009-192">Esse comando recupera os registros de saudação do tópico hello e os exibe.</span><span class="sxs-lookup"><span data-stu-id="91009-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="91009-193">Usando `--from-beginning` informa Olá consumidor toostart desde o início de saudação do fluxo de Olá para todos os registros são recuperados.</span><span class="sxs-lookup"><span data-stu-id="91009-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="91009-194">Use __Ctrl + C__ toostop consumidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="91009-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="91009-195">API de produtor e consumidor</span><span class="sxs-lookup"><span data-stu-id="91009-195">Producer and consumer API</span></span>

<span data-ttu-id="91009-196">Também por meio de programação, você pode produzir e consumir registros usando Olá [Kafka APIs](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="91009-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="91009-197">toobuild um produtor de Java e consumidor, use Olá seguindo as etapas do seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="91009-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91009-198">Você deve ter Olá instalados em seu ambiente de desenvolvimento de componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="91009-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="91009-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou equivalente, como OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="91009-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="91009-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="91009-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="91009-201">Um cliente SSH e hello `scp` comando.</span><span class="sxs-lookup"><span data-stu-id="91009-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="91009-202">Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="91009-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="91009-203">Baixe os exemplos de saudação do [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="91009-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="91009-204">Para exemplo de produtor/consumidor hello, use projeto Olá no hello `Producer-Consumer` directory.</span><span class="sxs-lookup"><span data-stu-id="91009-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="91009-205">Este exemplo contém Olá classes a seguir:</span><span class="sxs-lookup"><span data-stu-id="91009-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="91009-206">**Executar** -inicia o consumidor hello ou o produtor.</span><span class="sxs-lookup"><span data-stu-id="91009-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="91009-207">**Produtor** -repositórios 1.000.000 registros toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="91009-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="91009-208">**Consumidor** -lê os registros de tópico hello.</span><span class="sxs-lookup"><span data-stu-id="91009-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="91009-209">toocreate um pacote jar, alterar o local de toohello de diretórios da saudação `Producer-Consumer` saudação de diretório e usar comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="91009-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="91009-210">Esse comando cria um diretório chamado `target`, que contém um arquivo chamado `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="91009-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="91009-211">A seguir Olá use comandos Olá toocopy `kafka-producer-consumer-1.0-SNAPSHOT.jar` cluster do HDInsight tooyour arquivo:</span><span class="sxs-lookup"><span data-stu-id="91009-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="91009-212">Substituir **SSHUSER** com usuário SSH Olá para o cluster e substituir **CLUSTERNAME** com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="91009-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="91009-213">Quando solicitado que digite a senha de saudação do usuário SSH hello.</span><span class="sxs-lookup"><span data-stu-id="91009-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="91009-214">Uma vez Olá `scp` comando concluído a cópia do arquivo hello, conecte-se o cluster toohello usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="91009-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="91009-215">Saudação de uso toowrite de comando a seguir registra toohello testar tópico:</span><span class="sxs-lookup"><span data-stu-id="91009-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="91009-216">Quando tiver terminado de processo Olá, use Olá após o comando tooread tópico hello:</span><span class="sxs-lookup"><span data-stu-id="91009-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="91009-217">Olá ler, juntamente com uma contagem de registros, é exibido.</span><span class="sxs-lookup"><span data-stu-id="91009-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="91009-218">Você pode ver alguns mais de 1.000.000 registrados como enviados tópico de toohello vários registros usando um script em uma etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="91009-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="91009-219">Use __Ctrl + C__ tooexit consumidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="91009-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="91009-220">Vários consumidores</span><span class="sxs-lookup"><span data-stu-id="91009-220">Multiple consumers</span></span>

<span data-ttu-id="91009-221">Os consumidores do Kafka usam um grupo de consumidores ao ler os registros.</span><span class="sxs-lookup"><span data-stu-id="91009-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="91009-222">Usando o mesmo grupo de saudação com vários consumidores resulta em carga equilibrada leituras de um tópico.</span><span class="sxs-lookup"><span data-stu-id="91009-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="91009-223">Cada consumidor no grupo Olá recebe uma parte dos registros de saudação.</span><span class="sxs-lookup"><span data-stu-id="91009-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="91009-224">toosee esse processo em ação, use Olá seguindo as etapas:</span><span class="sxs-lookup"><span data-stu-id="91009-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="91009-225">Abra um novo cluster de toohello de sessão SSH, para que você tenha duas delas.</span><span class="sxs-lookup"><span data-stu-id="91009-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="91009-226">Em cada sessão, use Olá seguintes toostart um consumidor com Olá a mesma ID de grupo de consumidor:</span><span class="sxs-lookup"><span data-stu-id="91009-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="91009-227">Esse comando inicia um consumidor usando uma ID de grupo Olá `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="91009-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="91009-228">Usar os comandos de Olá Olá [obter informações de host Zookeeper e Broker Olá](#getkafkainfo) tooset seção `$KAFKABROKERS` para esta sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="91009-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="91009-229">Observe como cada sessão contagens Olá registra recebe do tópico hello.</span><span class="sxs-lookup"><span data-stu-id="91009-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="91009-230">total de saudação de ambas as sessões deve ser Olá mesmo que você recebeu anteriormente de um consumidor.</span><span class="sxs-lookup"><span data-stu-id="91009-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="91009-231">Consumo por clientes em Olá mesmo grupo é tratado por meio das partições Olá tópico hello.</span><span class="sxs-lookup"><span data-stu-id="91009-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="91009-232">Para Olá `test` tópico criado anteriormente, ele tem oito partições.</span><span class="sxs-lookup"><span data-stu-id="91009-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="91009-233">Se você abre oito sessões SSH e iniciar um consumidor em todas as sessões, cada consumidor lê os registros de uma única partição para o tópico de saudação.</span><span class="sxs-lookup"><span data-stu-id="91009-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91009-234">Não pode haver mais instâncias de consumidores do que partições em um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="91009-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="91009-235">Neste exemplo, um grupo de consumidor pode conter a consumidores tooeight já que é o número de saudação de partições no tópico hello.</span><span class="sxs-lookup"><span data-stu-id="91009-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="91009-236">Ou você pode ter vários grupos de consumidores, cada um com no máximo oito consumidores.</span><span class="sxs-lookup"><span data-stu-id="91009-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="91009-237">Registros armazenados em Kafka são armazenados em ordem de saudação que são recebidos em uma partição.</span><span class="sxs-lookup"><span data-stu-id="91009-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="91009-238">tooachieve ordenados na entrega para registros *dentro de uma partição*, crie um grupo de consumidores, onde o número de Olá de instâncias de consumidor corresponde o número de saudação de partições.</span><span class="sxs-lookup"><span data-stu-id="91009-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="91009-239">tooachieve ordenados na entrega para registros *tópico Olá*, criar um grupo de consumidores com a instância de apenas um consumidor.</span><span class="sxs-lookup"><span data-stu-id="91009-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="91009-240">API de streaming</span><span class="sxs-lookup"><span data-stu-id="91009-240">Streaming API</span></span>

<span data-ttu-id="91009-241">Olá streaming API foi adicionado tooKafka na versão 0.10.0; versões anteriores dependem Apache Spark ou Storm para processamento de fluxo.</span><span class="sxs-lookup"><span data-stu-id="91009-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="91009-242">Se você ainda não fez isso, baixe os exemplos de saudação do [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="91009-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="91009-243">Para Olá exemplo de transmissão, use o projeto Olá no Olá `streaming` directory.</span><span class="sxs-lookup"><span data-stu-id="91009-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="91009-244">Este projeto contém apenas uma classe, `Stream`, que lê os registros de saudação `test` tópico criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="91009-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="91009-245">Ele conta palavras Olá ler e emite cada tópico de tooa word e contagem chamado `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="91009-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="91009-246">Olá `wordcounts` tópico é criado em uma etapa mais adiante nesta seção.</span><span class="sxs-lookup"><span data-stu-id="91009-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="91009-247">Na linha de comando de saudação em seu ambiente de desenvolvimento, alterar o local de toohello de diretórios da saudação `Streaming` diretório e, em seguida, use Olá comando toocreate um pacote jar a seguir:</span><span class="sxs-lookup"><span data-stu-id="91009-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="91009-248">Esse comando cria um diretório chamado `target`, que contém um arquivo chamado `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="91009-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="91009-249">A seguir Olá use comandos Olá toocopy `kafka-streaming-1.0-SNAPSHOT.jar` cluster do HDInsight tooyour arquivo:</span><span class="sxs-lookup"><span data-stu-id="91009-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="91009-250">Substituir **SSHUSER** com usuário SSH Olá para o cluster e substituir **CLUSTERNAME** com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="91009-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="91009-251">Quando solicitado que digite a senha de saudação do usuário SSH hello.</span><span class="sxs-lookup"><span data-stu-id="91009-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="91009-252">Uma vez Olá `scp` comando concluído a cópia do arquivo hello, conectar toohello cluster usando o SSH e, em seguida, usar Olá Olá de toocreate de comando a seguir `wordcounts` tópico:</span><span class="sxs-lookup"><span data-stu-id="91009-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="91009-253">Em seguida, inicie Olá streaming processo usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="91009-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="91009-254">Esse comando inicia Olá processo em segundo plano da saudação de streaming.</span><span class="sxs-lookup"><span data-stu-id="91009-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="91009-255">Comando a seguir de saudação do uso toosend mensagens toohello `test` tópico.</span><span class="sxs-lookup"><span data-stu-id="91009-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="91009-256">Essas mensagens são processadas pelo Olá streaming de exemplo:</span><span class="sxs-lookup"><span data-stu-id="91009-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="91009-257">Saudação de uso após a saída de saudação do comando tooview escrito toohello `wordcounts` tópico por Olá streaming processo:</span><span class="sxs-lookup"><span data-stu-id="91009-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="91009-258">dados de saudação tooview, você deve informar o chave de Olá Olá consumidor tooprint e Olá desserializador toouse para Olá chave e valor.</span><span class="sxs-lookup"><span data-stu-id="91009-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="91009-259">nome da chave Olá é palavra hello e valor de chave Olá contém a contagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="91009-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="91009-260">saudação de saída é similar toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="91009-260">hello output is similar toohello following text:</span></span>
   
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
    > <span data-ttu-id="91009-261">Contagem de saudação incrementado sempre que uma palavra é encontrada.</span><span class="sxs-lookup"><span data-stu-id="91009-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="91009-262">Use Olá __Ctrl + C__ tooexit Olá consumidor, em seguida, usar Olá `fg` comando toobring Olá primeiro plano streaming toohello voltar de tarefa em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="91009-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="91009-263">Use __Ctrl + C__ tooexit-lo também.</span><span class="sxs-lookup"><span data-stu-id="91009-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="91009-264">Excluir o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="91009-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="91009-265">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="91009-265">Troubleshoot</span></span>

<span data-ttu-id="91009-266">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="91009-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="91009-267">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91009-267">Next steps</span></span>

<span data-ttu-id="91009-268">Neste documento, você aprendeu os fundamentos de saudação do trabalho com o Apache Kafka no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="91009-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="91009-269">Use Olá toolearn mais sobre como trabalhar com Kafka a seguir:</span><span class="sxs-lookup"><span data-stu-id="91009-269">Use hello following toolearn more about working with Kafka:</span></span>

* [<span data-ttu-id="91009-270">Garantir a alta disponibilidade de seus dados com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="91009-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="91009-271">Aumentar a escalabilidade, configurando discos gerenciados com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="91009-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="91009-272">[Documentação do Apache Kafka](http://kafka.apache.org/documentation.html) em kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="91009-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="91009-273">Use MirrorMaker toocreate uma réplica de Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="91009-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="91009-274">Usar Apache Storm com Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="91009-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="91009-275">Usar o Apache Spark com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="91009-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="91009-276">Conecte-se tooKafka por meio de uma rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="91009-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
