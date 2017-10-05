---
title: "Alta disponibilidade para Hadoop – Azure HDInsight | Microsoft Docs"
description: "Saiba como clusters HDInsight melhoram a confiabilidade e a disponibilidade usando um nó principal adicional. Saiba como isso afeta os serviços do Hadoop, como o Ambari e o Hive, e também como se conectar individualmente com cada nó principal usando SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: alta disponibilidade hadoop
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: e66ba67a36fc48d1762ba302d708e060489fdc71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="5248c-105">Disponibilidade e confiabilidade dos clusters Hadoop em HDInsight</span><span class="sxs-lookup"><span data-stu-id="5248c-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="5248c-106">Os clusters HDInsight fornecem dois nós de cabeçalho para aumentar a disponibilidade e a confiabilidade dos serviços e trabalhos do Hadoop em execução.</span><span class="sxs-lookup"><span data-stu-id="5248c-106">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="5248c-107">O Hadoop atinge a alta disponibilidade e confiabilidade replicando serviços e dados em múltiplos nós em um cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="5248c-108">No entanto, em geral, as distribuições padrão do Hadoop têm apenas um único nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="5248c-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="5248c-109">Qualquer falha do único nó de cabeçalho poderá fazer com que o cluster pare de funcionar.</span><span class="sxs-lookup"><span data-stu-id="5248c-109">Any outage of the single head node can cause the cluster to stop working.</span></span> <span data-ttu-id="5248c-110">O HDInsight fornece dois nós principais para melhorar a disponibilidade e a confiabilidade do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5248c-110">HDInsight provides two headnodes to improve Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5248c-111">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="5248c-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5248c-112">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5248c-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="5248c-113">Disponibilidade e confiabilidade dos nós</span><span class="sxs-lookup"><span data-stu-id="5248c-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="5248c-114">Os nós em um cluster HDInsight são implementados com o uso de Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="5248c-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="5248c-115">As seções a seguir abordam os tipos de nós individuais usados com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5248c-115">The following sections discuss the individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="5248c-116">Nem todos os tipos de nó são usados para um tipo de cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="5248c-117">Por exemplo, um tipo de cluster Hadoop não tem nenhum nó Nimbus.</span><span class="sxs-lookup"><span data-stu-id="5248c-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="5248c-118">Para obter mais informações sobre os nós usados pelos tipos de cluster HDInsight, veja a seção “Tipos de cluster” do documento [Criar clusters Hadoop baseados em Linux no HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="5248c-118">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="5248c-119">Nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="5248c-119">Head nodes</span></span>

<span data-ttu-id="5248c-120">Para garantir a alta disponibilidade dos serviços do Hadoop, o HDInsight oferece dois nós principais.</span><span class="sxs-lookup"><span data-stu-id="5248c-120">To ensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="5248c-121">Ambos os nós de cabeçalho estão ativos e em execução no cluster HDInsight simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="5248c-121">Both head nodes are active and running within the HDInsight cluster simultaneously.</span></span> <span data-ttu-id="5248c-122">Alguns serviços, como HDFS ou YARN, só estão “ativos” em um nó de cabeçalho a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="5248c-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="5248c-123">Outros serviços, como HiveServer2 ou MetaStore Hive estão ativos em ambos os nós de cabeçalho ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="5248c-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span></span>

<span data-ttu-id="5248c-124">Os nós de cabeçalho (e outros nós no HDInsight) tem um valor numérico como parte do nome do host do nó.</span><span class="sxs-lookup"><span data-stu-id="5248c-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span></span> <span data-ttu-id="5248c-125">Por exemplo, `hn0-CLUSTERNAME` ou `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="5248c-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5248c-126">Não associa o valor numérico com a possibilidade de um nó ser primário ou secundário.</span><span class="sxs-lookup"><span data-stu-id="5248c-126">Do not associate the numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="5248c-127">O valor numérico está presente apenas para fornecer um nome exclusivo para cada nó.</span><span class="sxs-lookup"><span data-stu-id="5248c-127">The numeric value is only present to provide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="5248c-128">Nós Nimbus</span><span class="sxs-lookup"><span data-stu-id="5248c-128">Nimbus Nodes</span></span>

<span data-ttu-id="5248c-129">Nós Nimbus estão disponíveis nos clusters Storm.</span><span class="sxs-lookup"><span data-stu-id="5248c-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="5248c-130">Os nós Nimbus fornecem funcionalidade semelhante ao JobTracker do Hadoop, distribuindo e monitorando o processamento nos nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5248c-130">The Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="5248c-131">O HDInsight oferece dois nós Nimbus para clusters Storm</span><span class="sxs-lookup"><span data-stu-id="5248c-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="5248c-132">Nós do Zookeeper</span><span class="sxs-lookup"><span data-stu-id="5248c-132">Zookeeper nodes</span></span>

<span data-ttu-id="5248c-133">Os nós [ZooKeeper](http://zookeeper.apache.org/) são usados para eleição de líder de serviços mestres em nós principais.</span><span class="sxs-lookup"><span data-stu-id="5248c-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="5248c-134">Eles também são usados para garantir que os serviços, nós de dados (trabalho) e gateways saibam em qual nó principal um serviço mestre está ativo.</span><span class="sxs-lookup"><span data-stu-id="5248c-134">They are also used to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="5248c-135">Por padrão, o HDInsight fornece três nós do ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="5248c-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="5248c-136">Nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="5248c-136">Worker nodes</span></span>

<span data-ttu-id="5248c-137">Os nós de trabalho executam a análise de dados real quando um trabalho é enviado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span></span> <span data-ttu-id="5248c-138">Se um nó de trabalho falhar, a tarefa que ele estava executando será enviada para outro nó de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5248c-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span></span> <span data-ttu-id="5248c-139">Por padrão, o HDInsight cria quatro nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5248c-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="5248c-140">Você pode alterar esse número para atender às suas necessidades, durante e após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-140">You can change this number to suit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="5248c-141">Nó de borda</span><span class="sxs-lookup"><span data-stu-id="5248c-141">Edge node</span></span>

<span data-ttu-id="5248c-142">Um nó de borda não participa ativamente na análise de dados dentro do cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-142">An edge node does not actively participate in data analysis within the cluster.</span></span> <span data-ttu-id="5248c-143">Ele é usado por desenvolvedores ou cientistas de dados ao trabalhar com o Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5248c-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="5248c-144">O nó de borda reside na mesma Rede Virtual do Azure que os outros nós no cluster e pode acessar diretamente todos os outros nós.</span><span class="sxs-lookup"><span data-stu-id="5248c-144">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="5248c-145">O nó de borda pode ser usado sem retirar recursos dos serviços críticos do Hadoop ou de trabalhos de análise.</span><span class="sxs-lookup"><span data-stu-id="5248c-145">The edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="5248c-146">Atualmente, o Servidor R no HDInsight é o único tipo de cluster que fornece um nó de borda por padrão.</span><span class="sxs-lookup"><span data-stu-id="5248c-146">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="5248c-147">Para o Servidor R no HDInsight, o nó de borda é usado para testar o código R localmente no nó antes de enviá-lo ao cluster para o processamento distribuído.</span><span class="sxs-lookup"><span data-stu-id="5248c-147">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span></span>

<span data-ttu-id="5248c-148">Para saber mais sobre como usar um nó de borda com tipos de cluster diferentes do Servidor de R, consulte o documento [Usar nós de borda no HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="5248c-148">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-the-nodes"></a><span data-ttu-id="5248c-149">Acessando os nós</span><span class="sxs-lookup"><span data-stu-id="5248c-149">Accessing the nodes</span></span>

<span data-ttu-id="5248c-150">O acesso ao cluster pela internet é fornecido por meio de um gateway público.</span><span class="sxs-lookup"><span data-stu-id="5248c-150">Access to the cluster over the internet is provided through a public gateway.</span></span> <span data-ttu-id="5248c-151">O acesso é limitado à conexão com os nós principais e (se houver) do nó de borda.</span><span class="sxs-lookup"><span data-stu-id="5248c-151">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span></span> <span data-ttu-id="5248c-152">O acesso aos serviços em execução em nós principais não é afetado por ter vários nós de cabeça.</span><span class="sxs-lookup"><span data-stu-id="5248c-152">Access to services running on the head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="5248c-153">O gateway público encaminha solicitações ao nó principal que hospeda o serviço solicitado.</span><span class="sxs-lookup"><span data-stu-id="5248c-153">The public gateway routes requests to the head node that hosts the requested service.</span></span> <span data-ttu-id="5248c-154">Por exemplo, se, no momento, o Ambari estiver hospedado no nó de cabeçalho secundário, o gateway encaminhará solicitações de entrada para o Ambari nesse nó.</span><span class="sxs-lookup"><span data-stu-id="5248c-154">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span></span>

<span data-ttu-id="5248c-155">O acesso por meio do gateway público é limitado à porta 443 (HTTPS), 22 e 23.</span><span class="sxs-lookup"><span data-stu-id="5248c-155">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="5248c-156">A porta __443__ é usada para acessar a interface do usuário do Ambari ou de outras interfaces da Web ou APIs REST hospedadas em nós de cabeça.</span><span class="sxs-lookup"><span data-stu-id="5248c-156">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span></span>

* <span data-ttu-id="5248c-157">A porta __22__ é usada para acessar o nó principal primária ou o nó de borda com o SSH.</span><span class="sxs-lookup"><span data-stu-id="5248c-157">Port __22__ is used to access the primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="5248c-158">A porta __23__ é usada para acessar o nó principal secundário com SSH.</span><span class="sxs-lookup"><span data-stu-id="5248c-158">Port __23__ is used to access the secondary head node with SSH.</span></span> <span data-ttu-id="5248c-159">Por exemplo, o `ssh username@mycluster-ssh.azurehdinsight.net` se conectará ao nó principal de cabeçalho do cluster chamado **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="5248c-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span></span>

<span data-ttu-id="5248c-160">Para saber mais sobre como usar SSH, consulte o documento [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5248c-160">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="5248c-161">Nomes internos de domínio totalmente qualificado (FQDN)</span><span class="sxs-lookup"><span data-stu-id="5248c-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="5248c-162">Os nós em um cluster HDInsight possuem um endereço IP interno e o FQDN que só pode ser acessado do cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span></span> <span data-ttu-id="5248c-163">Ao acessar serviços em cluster usando o endereço IP ou FQDN interno, você deve usar Ambari para verificar o IP ou FQDN para usar quando acessar o serviço.</span><span class="sxs-lookup"><span data-stu-id="5248c-163">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span></span>

<span data-ttu-id="5248c-164">Por exemplo, o serviço de Oozie pode ser executado somente em um nó de cabeçalho e usar o comando `oozie` de uma sessão SSH requer a URL para o serviço.</span><span class="sxs-lookup"><span data-stu-id="5248c-164">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span></span> <span data-ttu-id="5248c-165">Essa URL pode ser recuperada do Ambari usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5248c-165">This URL can be retrieved from Ambari by using the following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="5248c-166">Esse comando retorna um valor semelhante ao seguinte comando, que contém a URL interna para usar com o comando `oozie`:</span><span class="sxs-lookup"><span data-stu-id="5248c-166">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="5248c-167">Para saber mais sobre como trabalhar com a API REST do Ambari, consulte [Monitorar e gerenciar o HDInsight usando a API REST do Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="5248c-167">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="5248c-168">Acessando outros tipos de nó</span><span class="sxs-lookup"><span data-stu-id="5248c-168">Accessing other node types</span></span>

<span data-ttu-id="5248c-169">Você pode se conectar a nós que não estão diretamente acessíveis pela Internet usando os métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5248c-169">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span></span>

* <span data-ttu-id="5248c-170">**SSH**: assim que estiver conectado a um nó de cabeçalho usando o SSH, você poderá usar o SSH por meio do nó de cabeçalho para se conectar aos outros nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-170">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span></span> <span data-ttu-id="5248c-171">Para saber mais, consulte o documento [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5248c-171">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="5248c-172">**Túnel SSH**: caso precise acessar um serviço Web hospedado em um dos nós que não esteja exposto à Internet, será necessário usar um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="5248c-172">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="5248c-173">Para saber mais, consulte o documento [Usar túnel SSH com HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="5248c-173">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="5248c-174">**Rede Virtual do Azure**: caso o cluster HDInsight faça parte de uma Rede Virtual do Azure, qualquer recurso contido na mesma Rede Virtual poderá acessar diretamente todos os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span></span> <span data-ttu-id="5248c-175">Para saber mais, confira o documento [Estender o HDInsight usando a Rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="5248c-175">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-to-check-on-a-service-status"></a><span data-ttu-id="5248c-176">Como verificar o status do serviço</span><span class="sxs-lookup"><span data-stu-id="5248c-176">How to check on a service status</span></span>

<span data-ttu-id="5248c-177">A interface do usuário da Web do Ambari ou a API REST do Ambari pode ser usada para verificar o status dos serviços executados nos nós de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="5248c-177">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="5248c-178">Interface do usuário da Ambari Web</span><span class="sxs-lookup"><span data-stu-id="5248c-178">Ambari Web UI</span></span>

<span data-ttu-id="5248c-179">Abra a interface do usuário da Web do Ambari em https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="5248c-179">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="5248c-180">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-180">Replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="5248c-181">Se solicitado, insira as credenciais do usuário HTTP para o cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-181">If prompted, enter the HTTP user credentials for your cluster.</span></span> <span data-ttu-id="5248c-182">O nome de usuário padrão HTTP é **admin** e a senha é a senha que você digitou ao criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-182">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span></span>

<span data-ttu-id="5248c-183">Ao chegar na página Ambari, os serviços instalados serão listados à esquerda da página.</span><span class="sxs-lookup"><span data-stu-id="5248c-183">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span></span>

![Serviços instalados](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="5248c-185">Há uma série de ícones que podem aparecer ao lado de um serviço para indicar o status.</span><span class="sxs-lookup"><span data-stu-id="5248c-185">There are a series of icons that may appear next to a service to indicate status.</span></span> <span data-ttu-id="5248c-186">Todos os alertas relacionados a um serviço podem ser visualizados usando o link **Alertas** na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="5248c-186">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span></span> <span data-ttu-id="5248c-187">Você pode selecionar cada serviço para exibir mais informações sobre ele.</span><span class="sxs-lookup"><span data-stu-id="5248c-187">You can select each service to view more information on it.</span></span>

<span data-ttu-id="5248c-188">A página de serviço fornece informações sobre o status e a configuração de cada serviço, mas não fornece informações sobre o nó de cabeçalho no qual o serviço está em execução.</span><span class="sxs-lookup"><span data-stu-id="5248c-188">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span></span> <span data-ttu-id="5248c-189">Para exibir essas informações, use o link **Hosts** na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="5248c-189">To view this information, use the **Hosts** link at the top of the page.</span></span> <span data-ttu-id="5248c-190">Isso exibe os hosts do cluster, incluindo os nós de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="5248c-190">This page displays hosts within the cluster, including the head nodes.</span></span>

![lista de hosts](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="5248c-192">Selecionar o link para um dos nós de cabeçalho exibirá os serviços e componentes em execução nesse nó.</span><span class="sxs-lookup"><span data-stu-id="5248c-192">Selecting the link for one of the head nodes displays the services and components running on that node.</span></span>

![Status do componente](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="5248c-194">Para saber mais sobre como usar o Ambari, confira [Monitorar e gerenciar o HDInsight usando a interface de usuário da Web do Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="5248c-194">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="5248c-195">API REST do Ambari</span><span class="sxs-lookup"><span data-stu-id="5248c-195">Ambari REST API</span></span>

<span data-ttu-id="5248c-196">A API REST do Ambari está disponível pela internet.</span><span class="sxs-lookup"><span data-stu-id="5248c-196">The Ambari REST API is available over the internet.</span></span> <span data-ttu-id="5248c-197">O gateway público HDInsight manipula as solicitações de roteamento para o nó de cabeçalho que hospeda a API REST.</span><span class="sxs-lookup"><span data-stu-id="5248c-197">The HDInsight public gateway handles routing requests to the head node that is currently hosting the REST API.</span></span>

<span data-ttu-id="5248c-198">Você pode usar o seguinte comando para verificar o estado de um serviço por meio da API de REST do Ambari:</span><span class="sxs-lookup"><span data-stu-id="5248c-198">You can use the following command to check the state of a service through the Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="5248c-199">Substitua a **SENHA** pela senha da conta do usuário HTTP (administrador).</span><span class="sxs-lookup"><span data-stu-id="5248c-199">Replace **PASSWORD** with the HTTP user (admin) account password.</span></span>
* <span data-ttu-id="5248c-200">Substitua **CLUSTERNAME** pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-200">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
* <span data-ttu-id="5248c-201">Substitua o **SERVICENAME** pelo nome do serviço desejado para verificar o status.</span><span class="sxs-lookup"><span data-stu-id="5248c-201">Replace **SERVICENAME** with the name of the service you want to check the status of.</span></span>

<span data-ttu-id="5248c-202">Por exemplo, para verificar o status do serviço **HDFS** em um cluster chamado **mycluster**, por uma senha de **senha**, você usaria o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="5248c-202">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="5248c-203">A resposta é semelhante ao JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="5248c-203">The response is similar to the following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="5248c-204">A URL indica que o serviço está sendo executado no **hn0-CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="5248c-204">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="5248c-205">O estado indica que o serviço está sendo executado ou **INICIADO**.</span><span class="sxs-lookup"><span data-stu-id="5248c-205">The state tells us that the service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="5248c-206">Se você não souber quais serviços estão instalados no cluster, use o seguinte comando para recuperar uma lista:</span><span class="sxs-lookup"><span data-stu-id="5248c-206">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="5248c-207">Para saber mais sobre como trabalhar com a API REST do Ambari, consulte [Monitorar e gerenciar o HDInsight usando a API REST do Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="5248c-207">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="5248c-208">Componentes do serviço</span><span class="sxs-lookup"><span data-stu-id="5248c-208">Service components</span></span>

<span data-ttu-id="5248c-209">Serviços podem conter componentes os quais você deseja verificar o status de individualmente.</span><span class="sxs-lookup"><span data-stu-id="5248c-209">Services may contain components that you wish to check the status of individually.</span></span> <span data-ttu-id="5248c-210">Por exemplo, o HDFS contém o componente NameNode.</span><span class="sxs-lookup"><span data-stu-id="5248c-210">For example, HDFS contains the NameNode component.</span></span> <span data-ttu-id="5248c-211">Para exibir informações sobre um componente, o comando seria:</span><span class="sxs-lookup"><span data-stu-id="5248c-211">To view information on a component, the command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="5248c-212">Se você não souber quais componentes estão instalados no cluster, você pode usar o seguinte comando para recuperar uma lista:</span><span class="sxs-lookup"><span data-stu-id="5248c-212">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-to-access-log-files-on-the-head-nodes"></a><span data-ttu-id="5248c-213">Como acessar arquivos de log nos nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="5248c-213">How to access log files on the head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="5248c-214">SSH</span><span class="sxs-lookup"><span data-stu-id="5248c-214">SSH</span></span>

<span data-ttu-id="5248c-215">Enquanto estiver conectado a um nó de cabeçalho por meio do SSH, os arquivos de log podem ser encontrados em **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="5248c-215">While connected to a head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="5248c-216">Por exemplo, **/var/log/hadoop-yarn/yarn** contêm logs para YARN.</span><span class="sxs-lookup"><span data-stu-id="5248c-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="5248c-217">Cada nó de cabeçalho pode ter entradas de log exclusivo, portanto você deve verificar os logs em ambos.</span><span class="sxs-lookup"><span data-stu-id="5248c-217">Each head node can have unique log entries, so you should check the logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="5248c-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="5248c-218">SFTP</span></span>

<span data-ttu-id="5248c-219">Também é possível se conectar ao nó de cabeçalho usando o Protocolo FTP do SSH ou SFTP e baixar os arquivos de log diretamente.</span><span class="sxs-lookup"><span data-stu-id="5248c-219">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span></span>

<span data-ttu-id="5248c-220">Semelhante ao uso de um cliente SSH, ao se conectar com o cluster, é necessário fornecer o nome de conta de usuário SSH e o endereço SSH do cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-220">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span></span> <span data-ttu-id="5248c-221">Por exemplo: `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="5248c-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="5248c-222">Forneça a senha da conta quando solicitado ou uma chave pública usando o parâmetro `-i`.</span><span class="sxs-lookup"><span data-stu-id="5248c-222">Provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span></span>

<span data-ttu-id="5248c-223">Depois de conectado, você verá um prompt `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="5248c-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="5248c-224">Neste prompt, é possível alterar os diretórios, além de carregar e baixar arquivos.</span><span class="sxs-lookup"><span data-stu-id="5248c-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="5248c-225">Por exemplo, os seguintes comandos alteram os diretórios para o diretório **/var/log/hadoop/hdfs** e baixam todos os arquivos no diretório em seguida.</span><span class="sxs-lookup"><span data-stu-id="5248c-225">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="5248c-226">Para obter uma lista dos comandos disponíveis, insira `help` no prompt `sftp>`.</span><span class="sxs-lookup"><span data-stu-id="5248c-226">For a list of available commands, enter `help` at the `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="5248c-227">Há também interfaces gráficas que permitem visualizar o sistema de arquivos quando você estiver conectado usando SFTP.</span><span class="sxs-lookup"><span data-stu-id="5248c-227">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span></span> <span data-ttu-id="5248c-228">Por exemplo, [MobaXTerm](http://mobaxterm.mobatek.net/) permite que você procure o sistema de arquivos usando uma interface semelhante à do Windows Explorer.</span><span class="sxs-lookup"><span data-stu-id="5248c-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="5248c-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="5248c-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="5248c-230">Para acessar os arquivos de log usando o Ambari, use um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="5248c-230">To access log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="5248c-231">As interfaces da web para os serviços individuais não são expostas publicamente na Internet.</span><span class="sxs-lookup"><span data-stu-id="5248c-231">The web interfaces for the individual services are not exposed publicly on the Internet.</span></span> <span data-ttu-id="5248c-232">Para saber mais sobre como usar um túnel SSH, veja o documento [Usar túnel SSH](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="5248c-232">For information on using an SSH tunnel, see the [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="5248c-233">Na interface de usuário da Web do Ambari, selecione o serviço do qual você deseja exibir os logs (por exemplo, YARN).</span><span class="sxs-lookup"><span data-stu-id="5248c-233">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span></span> <span data-ttu-id="5248c-234">Em seguida, use os **Links Rápidos** a fim de selecionar para qual nó de cabeçalho exibir os logs.</span><span class="sxs-lookup"><span data-stu-id="5248c-234">Then use **Quick Links** to select which head node to view the logs for.</span></span>

![Usando links rápidos para exibir logs](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-to-configure-the-node-size"></a><span data-ttu-id="5248c-236">Como configurar o tamanho do nó</span><span class="sxs-lookup"><span data-stu-id="5248c-236">How to configure the node size</span></span>

<span data-ttu-id="5248c-237">O tamanho de um nó só pode ser selecionado durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="5248c-237">The size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="5248c-238">Você pode encontrar uma lista de diferentes tamanhos de VM disponíveis para o HDInsight na [página de preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5248c-238">You can find a list of the different VM sizes available for HDInsight on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="5248c-239">Ao criar um cluster, você pode especificar o tamanho dos nós.</span><span class="sxs-lookup"><span data-stu-id="5248c-239">When creating a cluster, you can specify the size of the nodes.</span></span> <span data-ttu-id="5248c-240">As informações a seguir fornecem orientação sobre como especificar o tamanho usando o [portal do Azure][preview-portal], o [Azure PowerShell][azure-powershell] e a [CLI do Azure][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="5248c-240">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="5248c-241">**Portal do Azure**: ao criar um cluster, você pode definir o tamanho dos nós usados pelo cluster:</span><span class="sxs-lookup"><span data-stu-id="5248c-241">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span></span>

    ![Imagem do Assistente de criação de cluster com a seleção de tamanho do nó](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="5248c-243">**CLI do Azure**: ao usar o comando `azure hdinsight cluster create`, é possível definir o tamanho dos nós de cabeçalho, de trabalho e do ZooKeeper usando os parâmetros `--headNodeSize`, `--workerNodeSize` e `--zookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="5248c-243">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="5248c-244">**Azure PowerShell**: ao usar o `New-AzureRmHDInsightCluster` cmdlet , é possível definir o tamanho dos nós de cabeçalho, de trabalho e do ZooKeeper usando os parâmetros `-HeadNodeVMSize`, `-WorkerNodeSize` e `-ZookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="5248c-244">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5248c-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5248c-245">Next steps</span></span>

<span data-ttu-id="5248c-246">Use os links a seguir para saber mais sobre os tópicos mencionados neste documento.</span><span class="sxs-lookup"><span data-stu-id="5248c-246">Use the following links to learn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="5248c-247">Referência REST do Ambari</span><span class="sxs-lookup"><span data-stu-id="5248c-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="5248c-248">Instalar e configurar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="5248c-248">Install and configure the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="5248c-249">Instalar e configurar o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="5248c-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="5248c-250">Gerenciar clusters HDInsight usando o Ambari</span><span class="sxs-lookup"><span data-stu-id="5248c-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="5248c-251">Provisionar os clusters HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="5248c-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
