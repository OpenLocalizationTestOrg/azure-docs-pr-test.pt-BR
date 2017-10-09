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
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="55ee9-103">Use tópicos de Apache Kafka tooreplicate MirrorMaker com Kafka no HDInsight (visualização)</span><span class="sxs-lookup"><span data-stu-id="55ee9-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="55ee9-104">Saiba como toouse Kafka Apache do espelhamento de cluster secundário do recurso tooreplicate tópicos tooa.</span><span class="sxs-lookup"><span data-stu-id="55ee9-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="55ee9-105">O espelhamento pode ser executado como um processo contínuo ou intermitentemente usado como um método de migração de dados de um cluster tooanother.</span><span class="sxs-lookup"><span data-stu-id="55ee9-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="55ee9-106">Neste exemplo, o espelhamento é usado tooreplicate tópicos entre dois clusters de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="55ee9-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="55ee9-107">Ambos os clusters estão em uma rede Virtual do Azure no hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="55ee9-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="55ee9-108">O espelhamento não deve ser considerado como uma meio tooachieve tolerância a falhas.</span><span class="sxs-lookup"><span data-stu-id="55ee9-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="55ee9-109">Olá tooitems de deslocamento dentro de um tópico são diferentes entre clusters de origem e destino hello, para que clientes não poderão usar o hello dois alternadamente.</span><span class="sxs-lookup"><span data-stu-id="55ee9-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="55ee9-110">Se você estiver preocupado com a tolerância a falhas, você deve definir a replicação para tópicos de saudação no cluster.</span><span class="sxs-lookup"><span data-stu-id="55ee9-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="55ee9-111">Para obter mais informações, confira [Introdução ao Kafka no HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="55ee9-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="55ee9-112">Como funciona o espelhamento do Kafka</span><span class="sxs-lookup"><span data-stu-id="55ee9-112">How Kafka mirroring works</span></span>

<span data-ttu-id="55ee9-113">Espelhamento funciona usando Olá MirrorMaker ferramenta (parte do Apache Kafka) tooconsume registros de tópicos no cluster de origem hello e, em seguida, crie uma cópia local no cluster de destino hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="55ee9-114">MirrorMaker usa uma (ou mais) *consumidores* que ler do cluster de origem Olá e um *produtor* que grava o cluster do toohello local (destino).</span><span class="sxs-lookup"><span data-stu-id="55ee9-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="55ee9-115">Olá diagrama a seguir ilustra o processo de espelhamento de saudação:</span><span class="sxs-lookup"><span data-stu-id="55ee9-115">hello following diagram illustrates hello Mirroring process:</span></span>

![Diagrama do processo de espelhamento de saudação](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="55ee9-117">Apache Kafka no HDInsight não fornece acesso toohello serviço Kafka sobre Olá internet pública.</span><span class="sxs-lookup"><span data-stu-id="55ee9-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="55ee9-118">Produtores Kafka ou os consumidores devem estar na Olá mesma rede virtual do Azure como nós Olá Olá cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="55ee9-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="55ee9-119">Neste exemplo, Olá fonte Kafka e clusters de destino estão localizados em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="55ee9-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="55ee9-120">Olá diagrama a seguir mostra como a comunicação flui entre clusters de saudação:</span><span class="sxs-lookup"><span data-stu-id="55ee9-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagrama de clusters Kafka de origem e destino em uma rede virtual do Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="55ee9-122">clusters de origem e destino Olá podem ser diferentes em número de saudação de nós e partições e deslocamentos nos tópicos da saudação também são diferentes.</span><span class="sxs-lookup"><span data-stu-id="55ee9-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="55ee9-123">Espelhamento mantém o valor de chave de saudação que é usado para particionamento, para que registro ordem é preservada em uma base por chave.</span><span class="sxs-lookup"><span data-stu-id="55ee9-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="55ee9-124">Espelhamento entre limites de rede</span><span class="sxs-lookup"><span data-stu-id="55ee9-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="55ee9-125">Se você precisar toomirror entre clusters de Kafka em redes diferentes, existem Olá considerações adicionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="55ee9-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="55ee9-126">**Gateways**: redes de saudação devem ser capaz de toocommunicate em Olá nível TCPIP.</span><span class="sxs-lookup"><span data-stu-id="55ee9-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="55ee9-127">**A resolução de nome**: Olá Kafka clusters em cada rede deve ser capaz de tooconnect tooeach outros usando nomes de host.</span><span class="sxs-lookup"><span data-stu-id="55ee9-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="55ee9-128">Isso pode exigir um servidor de sistema de nome de domínio (DNS) em cada rede que é configurado tooforward solicitações toohello outras redes.</span><span class="sxs-lookup"><span data-stu-id="55ee9-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="55ee9-129">Ao criar uma rede Virtual do Azure, em vez de usar o hello que DNS automático fornecido com a rede hello, você deve especificar um DNS server e hello endereço IP personalizado para o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="55ee9-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="55ee9-130">Após Olá que rede Virtual tiver sido criada, você deve criar uma máquina Virtual do Azure que usa o endereço IP, em seguida, instale e configure software DNS nele.</span><span class="sxs-lookup"><span data-stu-id="55ee9-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="55ee9-131">Criar e configurar um servidor DNS personalizado Olá antes de instalar HDInsight Olá rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="55ee9-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="55ee9-132">Não há nenhuma configuração adicional necessária para o servidor DNS do HDInsight toouse Olá configurado para Olá rede Virtual.</span><span class="sxs-lookup"><span data-stu-id="55ee9-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="55ee9-133">Para obter mais informações sobre como conectar duas Redes Virtuais do Azure, confira [Configurar uma conexão de VNet para VNet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="55ee9-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="55ee9-134">Criar clusters Kafka</span><span class="sxs-lookup"><span data-stu-id="55ee9-134">Create Kafka clusters</span></span>

<span data-ttu-id="55ee9-135">Embora você pode criar uma rede virtual do Azure e Kafka clusters manualmente, é mais fácil toouse um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="55ee9-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="55ee9-136">Use Olá toodeploy as etapas a seguir, uma rede virtual do Azure e tooyour clusters de dois Kafka assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="55ee9-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="55ee9-137">Use Olá botão toosign em tooAzure e modelo Olá abrir no portal do Azure de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="55ee9-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="55ee9-138">Hello Azure Resource Manager modelo está localizado em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="55ee9-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="55ee9-139">disponibilidade de tooguarantee de Kafka no HDInsight, o cluster deve conter pelo menos três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="55ee9-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="55ee9-140">Este modelo cria um cluster de Kafka que contém três nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="55ee9-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="55ee9-141">Olá usar entradas de saudação toopopulate informações a seguir no hello **implantação personalizada** folha:</span><span class="sxs-lookup"><span data-stu-id="55ee9-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![Implantação personalizada do HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="55ee9-143">**Grupo de recursos**: Crie um grupo ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="55ee9-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="55ee9-144">Esse grupo contém o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="55ee9-145">**Local**: selecione um tooyou geograficamente fechar do local.</span><span class="sxs-lookup"><span data-stu-id="55ee9-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="55ee9-146">**Nome do Cluster base**: esse valor é usado como nome base Olá Olá Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="55ee9-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="55ee9-147">Por exemplo, inserir **hdi** cria clusters chamados **source-hdi** e **dest-hdi**.</span><span class="sxs-lookup"><span data-stu-id="55ee9-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="55ee9-148">**Nome de usuário de logon de cluster**: nome de usuário de administrador Olá para Olá origem e destino Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="55ee9-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="55ee9-149">**Senha de logon de cluster**: clusters de Kafka com a senha do usuário administrador Olá para Olá origem e destino.</span><span class="sxs-lookup"><span data-stu-id="55ee9-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="55ee9-150">**Nome de usuário SSH**: clusters de Kafka toocreate de usuário SSH Olá para Olá origem e destino.</span><span class="sxs-lookup"><span data-stu-id="55ee9-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="55ee9-151">**Senha SSH**: senha Olá para usuário SSH Olá Olá origem e destino Kafka clusters.</span><span class="sxs-lookup"><span data-stu-id="55ee9-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="55ee9-152">Saudação de leitura **termos e condições**e, em seguida, selecione **concordo toohello termos e condições declaradas acima**.</span><span class="sxs-lookup"><span data-stu-id="55ee9-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="55ee9-153">Finalmente, verifique **Pin toodashboard** e, em seguida, selecione **compra**.</span><span class="sxs-lookup"><span data-stu-id="55ee9-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="55ee9-154">Demora cerca de 20 minutos toocreate clusters hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="55ee9-155">Após a criação dos recursos Olá, será redirecionado tooa folha Olá grupo de recursos que contém hello e clusters do painel da web.</span><span class="sxs-lookup"><span data-stu-id="55ee9-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Folha de grupo de recursos para redes hello e clusters](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="55ee9-157">Observe que os nomes de saudação de clusters de HDInsight Olá ficam **nome base do código-fonte** e **dest-nome de base**, onde nome base é o nome da saudação fornecido toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="55ee9-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="55ee9-158">Você pode usar esses nomes em etapas posteriores ao conectar-se toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="55ee9-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="55ee9-159">Criar tópicos</span><span class="sxs-lookup"><span data-stu-id="55ee9-159">Create topics</span></span>

1. <span data-ttu-id="55ee9-160">Conecte-se toohello **fonte** cluster usando o SSH:</span><span class="sxs-lookup"><span data-stu-id="55ee9-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="55ee9-161">Substituir **sshuser** com nome de usuário SSH Olá usado ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="55ee9-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="55ee9-162">Substituir **nome base** com o nome de base Olá usado ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="55ee9-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="55ee9-163">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="55ee9-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="55ee9-164">A seguir Olá use comandos hosts de Zookeeper toofind Olá para o cluster de origem hello:</span><span class="sxs-lookup"><span data-stu-id="55ee9-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

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

3. <span data-ttu-id="55ee9-165">Saudação de uso tooverify de comando que Olá tópico a seguir foi criada:</span><span class="sxs-lookup"><span data-stu-id="55ee9-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="55ee9-166">Olá resposta contém `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="55ee9-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="55ee9-167">Olá usar informações do host Zookeeper tooview Olá para este a seguir (Olá **origem**) cluster:</span><span class="sxs-lookup"><span data-stu-id="55ee9-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="55ee9-168">Isso retorna informações toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="55ee9-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="55ee9-169">Salve essas informações.</span><span class="sxs-lookup"><span data-stu-id="55ee9-169">Save this information.</span></span> <span data-ttu-id="55ee9-170">Ele é usado na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="55ee9-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="55ee9-171">Configurar o espelhamento</span><span class="sxs-lookup"><span data-stu-id="55ee9-171">Configure mirroring</span></span>

1. <span data-ttu-id="55ee9-172">Conecte-se toohello **destino** usando uma sessão SSH diferente do cluster:</span><span class="sxs-lookup"><span data-stu-id="55ee9-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="55ee9-173">Substituir **sshuser** com nome de usuário SSH Olá usado ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="55ee9-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="55ee9-174">Substituir **nome base** com o nome de base Olá usado ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="55ee9-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="55ee9-175">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="55ee9-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="55ee9-176">Comando a seguir de saudação do uso toocreate um `consumer.properties` arquivo que descreve como toocommunicate com hello **fonte** cluster:</span><span class="sxs-lookup"><span data-stu-id="55ee9-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="55ee9-177">Saudação de uso após o texto como conteúdo de saudação do hello `consumer.properties` arquivo:</span><span class="sxs-lookup"><span data-stu-id="55ee9-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="55ee9-178">Substituir **SOURCE_ZKHOSTS** com hello Zookeeper hospeda informações de saudação **fonte** cluster.</span><span class="sxs-lookup"><span data-stu-id="55ee9-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="55ee9-179">Esse arquivo descreve Olá consumidor informações toouse durante a leitura da origem Olá cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="55ee9-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="55ee9-180">Para obter mais informações de configuração do consumidor, confira [Configurações de Consumidor](https://kafka.apache.org/documentation#consumerconfigs) em kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="55ee9-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="55ee9-181">arquivo de saudação toosave, use **Ctrl + X**, **Y**e, em seguida, **Enter**.</span><span class="sxs-lookup"><span data-stu-id="55ee9-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="55ee9-182">Antes de configurar o produtor Olá que se comunica com o cluster de destino hello, você deve localizar broker Olá hosts Olá **destino** cluster.</span><span class="sxs-lookup"><span data-stu-id="55ee9-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="55ee9-183">Use essas informações de saudação tooretrieve comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="55ee9-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="55ee9-184">Substituir `$PASSWORD` com senha de conta (admin) de logon Olá para cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="55ee9-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="55ee9-185">Substituir `$CLUSTERNAME` com o nome de saudação do cluster de destino hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="55ee9-186">Estes comandos retornam a seguir toohello semelhante informações:</span><span class="sxs-lookup"><span data-stu-id="55ee9-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="55ee9-187">Saudação de uso a seguir toocreate uma `producer.properties` arquivo que descreve como toocommunicate com hello **destino** cluster:</span><span class="sxs-lookup"><span data-stu-id="55ee9-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="55ee9-188">Saudação de uso após o texto como conteúdo de saudação do hello `producer.properties` arquivo:</span><span class="sxs-lookup"><span data-stu-id="55ee9-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="55ee9-189">Substituir **DEST_BROKERS** com informações de agente de saudação da etapa anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="55ee9-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="55ee9-190">Para obter mais informações de configuração produtor, confira [Configurações de Produtor](https://kafka.apache.org/documentation#producerconfigs) em kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="55ee9-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="55ee9-191">Iniciar MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="55ee9-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="55ee9-192">De saudação SSH conexão toohello **destino** de cluster, use Olá após comando toostart Olá MirrorMaker processo:</span><span class="sxs-lookup"><span data-stu-id="55ee9-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="55ee9-193">Olá parâmetros usados neste exemplo são:</span><span class="sxs-lookup"><span data-stu-id="55ee9-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="55ee9-194">**– consumer.config**: Especifica o arquivo hello que contém propriedades de consumidor.</span><span class="sxs-lookup"><span data-stu-id="55ee9-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="55ee9-195">Essas propriedades são usada toocreate um consumidor que lê da saudação *fonte* cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="55ee9-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="55ee9-196">**– producer.config**: Especifica o arquivo hello que contém propriedades de produtor.</span><span class="sxs-lookup"><span data-stu-id="55ee9-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="55ee9-197">Essas propriedades são usada toocreate um produtor que grava toohello *destino* cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="55ee9-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="55ee9-198">**– lista branca**: uma lista de tópicos MirrorMaker replica de saudação origem cluster toohello destino.</span><span class="sxs-lookup"><span data-stu-id="55ee9-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="55ee9-199">**– num.streams**: Olá inúmeros toocreate de threads de consumidor.</span><span class="sxs-lookup"><span data-stu-id="55ee9-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="55ee9-200">Na inicialização, MirrorMaker retorna informações toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="55ee9-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="55ee9-201">De saudação SSH conexão toohello **fonte** de cluster, use Olá após o comando toostart um produtor e enviar o tópico de toohello de mensagens:</span><span class="sxs-lookup"><span data-stu-id="55ee9-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="55ee9-202">Substituir `$PASSWORD` com a senha de logon (admin) Olá para o cluster de origem hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="55ee9-203">Substituir `$CLUSTERNAME` com o nome de saudação do cluster de origem hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="55ee9-204">Quando você chega a uma linha em branco com um cursor, digite algumas mensagens de texto.</span><span class="sxs-lookup"><span data-stu-id="55ee9-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="55ee9-205">Esses são enviadas toohello tópico em Olá **fonte** cluster.</span><span class="sxs-lookup"><span data-stu-id="55ee9-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="55ee9-206">Quando terminar, use **Ctrl + C** tooend processo de produtor de saudação.</span><span class="sxs-lookup"><span data-stu-id="55ee9-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="55ee9-207">De saudação SSH conexão toohello **destino** de cluster, use **Ctrl + C** Olá tooend MirrorMaker processo.</span><span class="sxs-lookup"><span data-stu-id="55ee9-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="55ee9-208">Em seguida, a seguir Olá use comandos tooverify que Olá `testtopic` tópico foi criado, e esses dados no tópico Olá foram replicada toothis espelho:</span><span class="sxs-lookup"><span data-stu-id="55ee9-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="55ee9-209">Substituir `$PASSWORD` com a senha de logon (admin) Olá para o cluster de destino hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="55ee9-210">Substituir `$CLUSTERNAME` com o nome de saudação do cluster de destino hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="55ee9-211">Olá lista de tópicos agora inclui `testtopic`, que é criado quando MirrorMaster reflete o tópico de saudação do hello fonte cluster toohello de destino.</span><span class="sxs-lookup"><span data-stu-id="55ee9-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="55ee9-212">mensagens de saudação recuperadas do tópico Olá são Olá mesmo inserido no cluster de origem hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="55ee9-213">Excluir o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="55ee9-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="55ee9-214">Como criam etapas de saudação neste documento hello de clusters no mesmo grupo de recursos do Azure, você pode excluir o grupo de recursos Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="55ee9-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="55ee9-215">Excluindo grupo de recursos de saudação remove todos os recursos criados seguindo este documento, Olá rede Virtual do Azure e conta de armazenamento usados pelo clusters hello.</span><span class="sxs-lookup"><span data-stu-id="55ee9-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="55ee9-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="55ee9-216">Next Steps</span></span>

<span data-ttu-id="55ee9-217">Neste documento, você aprendeu como toouse MirrorMaker toocreate de uma réplica de um Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="55ee9-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="55ee9-218">Use Olá toodiscover links a seguir outra maneiras toowork Kafka:</span><span class="sxs-lookup"><span data-stu-id="55ee9-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="55ee9-219">[Documentação do Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) em cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="55ee9-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="55ee9-220">Introdução ao Apache Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="55ee9-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="55ee9-221">Usar o Apache Spark com o Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="55ee9-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="55ee9-222">Usar Apache Storm com Kafka no HDInsight</span><span class="sxs-lookup"><span data-stu-id="55ee9-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="55ee9-223">Conecte-se tooKafka por meio de uma rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="55ee9-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
