---
title: disponibilidade de aaaHigh para Hadoop - HDInsight do Azure | Microsoft Docs
description: "Saiba como clusters HDInsight melhoram a confiabilidade e a disponibilidade usando um nó principal adicional. Saiba como isso afeta os serviços Hadoop, como Ambari e Hive, bem como tooindividually conectar tooeach nó principal usando o SSH."
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
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="e3184-105">Disponibilidade e confiabilidade dos clusters Hadoop em HDInsight</span><span class="sxs-lookup"><span data-stu-id="e3184-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="e3184-106">Clusters HDInsight fornecem duas disponibilidade de saudação tooincrease nós de cabeçalho e a confiabilidade dos serviços Hadoop e trabalhos em execução.</span><span class="sxs-lookup"><span data-stu-id="e3184-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="e3184-107">O Hadoop atinge a alta disponibilidade e confiabilidade replicando serviços e dados em múltiplos nós em um cluster.</span><span class="sxs-lookup"><span data-stu-id="e3184-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="e3184-108">No entanto, em geral, as distribuições padrão do Hadoop têm apenas um único nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="e3184-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="e3184-109">Qualquer interrupção do nó de cabeçalho único Olá pode fazer com que o trabalho de toostop cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e3184-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="e3184-110">HDInsight fornece disponibilidade e a confiabilidade do duas headnodes tooimprove Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e3184-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3184-111">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e3184-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e3184-112">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e3184-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="e3184-113">Disponibilidade e confiabilidade dos nós</span><span class="sxs-lookup"><span data-stu-id="e3184-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="e3184-114">Os nós em um cluster HDInsight são implementados com o uso de Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3184-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="e3184-115">Olá seções a seguir discutem os tipos de nós individuais Olá usados com HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e3184-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="e3184-116">Nem todos os tipos de nó são usados para um tipo de cluster.</span><span class="sxs-lookup"><span data-stu-id="e3184-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="e3184-117">Por exemplo, um tipo de cluster Hadoop não tem nenhum nó Nimbus.</span><span class="sxs-lookup"><span data-stu-id="e3184-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="e3184-118">Para obter mais informações sobre nós usado pelos tipos de cluster HDInsight, consulte a seção de tipos de Cluster de saudação do hello [Hadoop baseado em Linux criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) documento.</span><span class="sxs-lookup"><span data-stu-id="e3184-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="e3184-119">Nós de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="e3184-119">Head nodes</span></span>

<span data-ttu-id="e3184-120">a alta disponibilidade de serviços Hadoop tooensure, HDInsight fornece dois nós de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="e3184-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="e3184-121">Ambos os nós de cabeçalho estão ativo e em execução no cluster do HDInsight Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="e3184-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="e3184-122">Alguns serviços, como HDFS ou YARN, só estão “ativos” em um nó de cabeçalho a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e3184-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="e3184-123">Outros serviços, como HiveServer2 ou MetaStore Hive estão ativos em ambos os nós principal no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="e3184-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="e3184-124">Nós de cabeçalho (e outros nós no HDInsight) tem um valor numérico como parte do nome de host de saudação do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3184-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="e3184-125">Por exemplo, `hn0-CLUSTERNAME` ou `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="e3184-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3184-126">Não associe valor numérico Olá se um nó é primário ou secundário.</span><span class="sxs-lookup"><span data-stu-id="e3184-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="e3184-127">valor numérico de saudação é tooprovide presente apenas um nome exclusivo para cada nó.</span><span class="sxs-lookup"><span data-stu-id="e3184-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="e3184-128">Nós Nimbus</span><span class="sxs-lookup"><span data-stu-id="e3184-128">Nimbus Nodes</span></span>

<span data-ttu-id="e3184-129">Nós Nimbus estão disponíveis nos clusters Storm.</span><span class="sxs-lookup"><span data-stu-id="e3184-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="e3184-130">nós de Nimbus Olá fornecem semelhante funcionalidade toohello Hadoop JobTracker por distribuição e monitoramento de processamento entre nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e3184-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="e3184-131">O HDInsight oferece dois nós Nimbus para clusters Storm</span><span class="sxs-lookup"><span data-stu-id="e3184-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="e3184-132">Nós do Zookeeper</span><span class="sxs-lookup"><span data-stu-id="e3184-132">Zookeeper nodes</span></span>

<span data-ttu-id="e3184-133">Os nós [ZooKeeper](http://zookeeper.apache.org/) são usados para eleição de líder de serviços mestres em nós principais.</span><span class="sxs-lookup"><span data-stu-id="e3184-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="e3184-134">Eles também são usada tooinsure que serviços, nós de dados (trabalho) e gateways sabem qual nó principal mestra do serviço está ativa no.</span><span class="sxs-lookup"><span data-stu-id="e3184-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="e3184-135">Por padrão, o HDInsight fornece três nós do ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="e3184-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="e3184-136">Nós de trabalho</span><span class="sxs-lookup"><span data-stu-id="e3184-136">Worker nodes</span></span>

<span data-ttu-id="e3184-137">Nós de trabalho executam análise de dados reais de saudação quando um trabalho é enviado toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="e3184-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="e3184-138">Se um nó de trabalho falhar, a tarefa de saudação que estava executando é nó de trabalho tooanother enviados.</span><span class="sxs-lookup"><span data-stu-id="e3184-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="e3184-139">Por padrão, o HDInsight cria quatro nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e3184-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="e3184-140">Você pode alterar esse número toosuit suas necessidades durante e após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="e3184-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="e3184-141">Nó de borda</span><span class="sxs-lookup"><span data-stu-id="e3184-141">Edge node</span></span>

<span data-ttu-id="e3184-142">Um nó de borda não participará na análise de dados em cluster Olá ativamente.</span><span class="sxs-lookup"><span data-stu-id="e3184-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="e3184-143">Ele é usado por desenvolvedores ou cientistas de dados ao trabalhar com o Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e3184-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="e3184-144">Olá borda nó vidas em Olá mesma rede Virtual do Azure Olá outros nós no cluster hello e podem acessar diretamente a todos os outros nós.</span><span class="sxs-lookup"><span data-stu-id="e3184-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="e3184-145">nó de borda Olá pode ser usado sem colocar recursos longe serviços críticos do Hadoop ou trabalhos de análise.</span><span class="sxs-lookup"><span data-stu-id="e3184-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="e3184-146">No momento, o servidor de R no HDInsight é Olá somente tipo de cluster que fornece um nó de borda padrão.</span><span class="sxs-lookup"><span data-stu-id="e3184-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="e3184-147">Para o servidor do R no HDInsight, o nó de borda de saudação é usado o código de teste R localmente no nó de saudação antes do envio cluster toohello para processamento distribuído.</span><span class="sxs-lookup"><span data-stu-id="e3184-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="e3184-148">Para obter informações sobre o uso de um nó de borda com tipos de cluster que não seja o servidor de R, consulte Olá [usar nós de borda em HDInsight](hdinsight-apps-use-edge-node.md) documento.</span><span class="sxs-lookup"><span data-stu-id="e3184-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="e3184-149">Acessar nós Olá</span><span class="sxs-lookup"><span data-stu-id="e3184-149">Accessing hello nodes</span></span>

<span data-ttu-id="e3184-150">Cluster de toohello de acesso sobre Olá internet é fornecido por meio de um gateway público.</span><span class="sxs-lookup"><span data-stu-id="e3184-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="e3184-151">O acesso é limitado tooconnecting toohello nós de cabeçalho e (se houver) Olá nó de borda.</span><span class="sxs-lookup"><span data-stu-id="e3184-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="e3184-152">Acesso tooservices em execução em nós de cabeça Olá não é afetado por ter vários nós de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="e3184-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="e3184-153">Olá gateway pública rotas solicitações toohello nó principal que hospeda Olá serviço solicitado.</span><span class="sxs-lookup"><span data-stu-id="e3184-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="e3184-154">Por exemplo, se Ambari está hospedado no momento no nó de cabeçalho secundário hello, gateway Olá roteia solicitações de entrada para o nó de toothat Ambari.</span><span class="sxs-lookup"><span data-stu-id="e3184-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="e3184-155">O acesso por gateway pública Olá é limitado tooport 443 (HTTPS), 22 e 23.</span><span class="sxs-lookup"><span data-stu-id="e3184-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="e3184-156">Porta __443__ é usado tooaccess Ambari e outros web interface do usuário ou APIs REST hospedadas em nós de cabeça hello.</span><span class="sxs-lookup"><span data-stu-id="e3184-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="e3184-157">Porta __22__ é nó de cabeçalho principal usado tooaccess hello ou nó de borda com o SSH.</span><span class="sxs-lookup"><span data-stu-id="e3184-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="e3184-158">Porta __23__ é usado tooaccess Olá secundário nó principal com SSH.</span><span class="sxs-lookup"><span data-stu-id="e3184-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="e3184-159">Por exemplo, `ssh username@mycluster-ssh.azurehdinsight.net` conecta toohello nó primário de principal do cluster Olá denominado **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="e3184-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="e3184-160">Para obter mais informações sobre como usar SSH, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="e3184-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="e3184-161">Nomes internos de domínio totalmente qualificado (FQDN)</span><span class="sxs-lookup"><span data-stu-id="e3184-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="e3184-162">Nós em um cluster HDInsight tem um endereço IP e o FQDN que só pode ser acessado do cluster Olá interno.</span><span class="sxs-lookup"><span data-stu-id="e3184-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="e3184-163">Ao acessar serviços em cluster hello usando o endereço IP ou FQDN interno do hello, você deve usar o Ambari tooverify Olá IP ou FQDN toouse ao acessar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3184-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="e3184-164">Por exemplo, Olá Oozie serviço só pode ser executado em um nó principal e usando Olá `oozie` comando de uma sessão SSH requer o serviço de toohello Olá URL.</span><span class="sxs-lookup"><span data-stu-id="e3184-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="e3184-165">Essa URL pode ser recuperado do Ambari usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3184-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="e3184-166">Esse comando retorna um toohello semelhante de valor a seguir de comando, que contém a saudação toouse interno de URL com hello `oozie` comando:</span><span class="sxs-lookup"><span data-stu-id="e3184-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="e3184-167">Para obter mais informações sobre como trabalhar com hello Ambari REST API, consulte [monitorar e gerenciar o HDInsight usando Olá API REST do Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="e3184-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="e3184-168">Acessando outros tipos de nó</span><span class="sxs-lookup"><span data-stu-id="e3184-168">Accessing other node types</span></span>

<span data-ttu-id="e3184-169">Você pode conectar toonodes que são não diretamente acessível via Olá internet usando Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3184-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="e3184-170">**SSH**: uma vez conectado tooa nó principal usando SSH, em seguida, você pode usar SSH de saudação nó principal tooconnect tooother nós Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="e3184-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="e3184-171">Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="e3184-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="e3184-172">**Túnel SSH**: se você precisar tooaccess um serviço web hospedado em um de nós de saudação que não seja exposto toohello internet, você deve usar um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="e3184-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="e3184-173">Para obter mais informações, consulte Olá [usar um túnel SSH com HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="e3184-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="e3184-174">**Rede Virtual do Azure**: se o HDInsight cluster faz parte de uma rede Virtual do Azure, qualquer recurso em Olá mesmo rede Virtual pode acessar todos os nós no cluster de saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="e3184-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="e3184-175">Para obter mais informações, consulte Olá [HDInsight estender usando a rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="e3184-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="e3184-176">Como toocheck em um status de serviço</span><span class="sxs-lookup"><span data-stu-id="e3184-176">How toocheck on a service status</span></span>

<span data-ttu-id="e3184-177">status de saudação toocheck de serviços que são executados em nós de cabeçalho Olá, use Olá Ambari Web UI ou Olá Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="e3184-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="e3184-178">Interface do usuário da Ambari Web</span><span class="sxs-lookup"><span data-stu-id="e3184-178">Ambari Web UI</span></span>

<span data-ttu-id="e3184-179">Olá Ambari Web UI é visível em https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="e3184-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="e3184-180">Substituir **CLUSTERNAME** com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="e3184-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="e3184-181">Quando solicitado, insira as credenciais do usuário Olá HTTP para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e3184-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="e3184-182">nome de usuário saudação padrão HTTP é **admin** e a senha de saudação é Olá senha ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3184-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="e3184-183">Ao chegar na página de Ambari hello, serviços Olá instalado estão listados Olá esquerda da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3184-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![Serviços instalados](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="e3184-185">Há uma série de ícones que podem aparecer próximo status de tooindicate do serviço tooa.</span><span class="sxs-lookup"><span data-stu-id="e3184-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="e3184-186">Todos os alertas relacionados ao serviço tooa pode ser exibido usando Olá **alertas** link na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3184-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="e3184-187">Você pode selecionar cada tooview de serviço para obter mais informações sobre ele.</span><span class="sxs-lookup"><span data-stu-id="e3184-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="e3184-188">Enquanto a página de serviço Olá fornece informações sobre o status de saudação e a configuração de cada serviço, ele não fornece informações em que está sendo executado no serviço de saudação do nó principal.</span><span class="sxs-lookup"><span data-stu-id="e3184-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="e3184-189">tooview essa informações, use Olá **Hosts** link na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3184-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="e3184-190">Esta página exibe os hosts no cluster hello, incluindo nós de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="e3184-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![lista de hosts](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="e3184-192">Link de Olá selecionando para um de nós de cabeçalho de saudação exibe serviços hello e componentes em execução nesse nó.</span><span class="sxs-lookup"><span data-stu-id="e3184-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![Status do componente](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="e3184-194">Para obter mais informações sobre como usar o Ambari, consulte [monitorar e gerenciar o HDInsight usando Olá da interface do usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="e3184-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="e3184-195">API REST do Ambari</span><span class="sxs-lookup"><span data-stu-id="e3184-195">Ambari REST API</span></span>

<span data-ttu-id="e3184-196">Olá Ambari REST API está disponível por Olá internet.</span><span class="sxs-lookup"><span data-stu-id="e3184-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="e3184-197">gateway público do HDInsight Olá manipula roteamento solicitações toohello nó principal que está hospedando Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="e3184-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="e3184-198">Você pode usar o hello estado de saudação do comando toocheck de um serviço por meio de saudação Ambari API de REST a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3184-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="e3184-199">Substituir **senha** com a senha da conta de usuário (admin) Olá HTTP.</span><span class="sxs-lookup"><span data-stu-id="e3184-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="e3184-200">Substituir **CLUSTERNAME** com o nome de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e3184-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="e3184-201">Substituir **SERVICENAME** com o nome de saudação do serviço de saudação você deseja toocheck status de saudação do.</span><span class="sxs-lookup"><span data-stu-id="e3184-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="e3184-202">Por exemplo, o status de saudação toocheck de saudação **HDFS** serviço em um cluster denominado **mycluster**, com uma senha de **senha**, você usaria Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3184-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="e3184-203">resposta de saudação é semelhante toohello JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3184-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="e3184-204">Olá URL informa que o serviço hello está sendo executado em um nó de cabeçalho chamado **hn0 CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="e3184-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="e3184-205">Olá estado informa que o serviço hello está sendo executado, ou **iniciado**.</span><span class="sxs-lookup"><span data-stu-id="e3184-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="e3184-206">Se você não souber quais serviços estão instalados no cluster hello, você pode usar o hello tooretrieve comando uma lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3184-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="e3184-207">Para obter mais informações sobre como trabalhar com hello Ambari REST API, consulte [monitorar e gerenciar o HDInsight usando Olá API REST do Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="e3184-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="e3184-208">Componentes do serviço</span><span class="sxs-lookup"><span data-stu-id="e3184-208">Service components</span></span>

<span data-ttu-id="e3184-209">Serviços podem conter componentes que você deseja status Olá toocheck individualmente.</span><span class="sxs-lookup"><span data-stu-id="e3184-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="e3184-210">Por exemplo, HDFS contém componente de NameNode de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3184-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="e3184-211">tooview informações em um componente, comando Olá seria:</span><span class="sxs-lookup"><span data-stu-id="e3184-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="e3184-212">Se você não souber quais componentes são fornecidos por um serviço, você pode usar o hello tooretrieve comando uma lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="e3184-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="e3184-213">Como tooaccess arquivos de log em nós de cabeçalho Olá</span><span class="sxs-lookup"><span data-stu-id="e3184-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="e3184-214">SSH</span><span class="sxs-lookup"><span data-stu-id="e3184-214">SSH</span></span>

<span data-ttu-id="e3184-215">Ao nó de cabeçalho tooa conectados por meio do SSH, os arquivos de log podem ser encontrados em **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="e3184-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="e3184-216">Por exemplo, **/var/log/hadoop-yarn/yarn** contêm logs para YARN.</span><span class="sxs-lookup"><span data-stu-id="e3184-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="e3184-217">Cada nó de cabeçalho pode ter entradas de log exclusivo, por isso, você deve verificar Olá logs em ambos os.</span><span class="sxs-lookup"><span data-stu-id="e3184-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="e3184-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="e3184-218">SFTP</span></span>

<span data-ttu-id="e3184-219">Você também pode conectar toohello nó principal usando Olá SSH File Transfer Protocol ou proteger arquivos Transfer Protocol (SFTP) e baixar os arquivos de log Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="e3184-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="e3184-220">Toousing semelhante um cliente SSH, ao se conectar a cluster toohello forneça Olá SSH usuário conta nome e Olá SSH o endereço de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e3184-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="e3184-221">Por exemplo: `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="e3184-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="e3184-222">Fornecer a senha de saudação conta hello quando solicitado, ou forneça uma chave pública usando Olá `-i` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e3184-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="e3184-223">Depois de conectado, você verá um prompt `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="e3184-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="e3184-224">Neste prompt, é possível alterar os diretórios, além de carregar e baixar arquivos.</span><span class="sxs-lookup"><span data-stu-id="e3184-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="e3184-225">Por exemplo, a saudação comandos a seguir alterar diretórios toohello **/var/log/hadoop/hdfs** diretório e, em seguida, baixar todos os arquivos no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3184-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="e3184-226">Para obter uma lista de comandos disponíveis, digite `help` em Olá `sftp>` prompt.</span><span class="sxs-lookup"><span data-stu-id="e3184-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="e3184-227">Também há interfaces gráficas que permitem que você toovisualize sistema de arquivos hello quando conectado usando SFTP.</span><span class="sxs-lookup"><span data-stu-id="e3184-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="e3184-228">Por exemplo, [MobaXTerm](http://mobaxterm.mobatek.net/) permite sistema de arquivos de saudação toobrowse usando um tooWindows semelhantes da interface Explorer.</span><span class="sxs-lookup"><span data-stu-id="e3184-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="e3184-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="e3184-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="e3184-230">usando o Ambari de arquivos de log de tooaccess, você deve usar um túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="e3184-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="e3184-231">interfaces de web Olá para serviços individuais Olá não são expostas publicamente Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="e3184-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="e3184-232">Para obter informações sobre o uso de um túnel SSH, consulte Olá [Use SSH túnel](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="e3184-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="e3184-233">De saudação da interface do usuário do Ambari Web, selecione Serviço de saudação que deseja tooview logs (por exemplo, YARN).</span><span class="sxs-lookup"><span data-stu-id="e3184-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="e3184-234">Em seguida, use **Links rápidos** tooselect registra quais Olá tooview de nó principal para.</span><span class="sxs-lookup"><span data-stu-id="e3184-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![Usar rápida links tooview logs](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="e3184-236">Como tooconfigure Olá tamanho de nó</span><span class="sxs-lookup"><span data-stu-id="e3184-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="e3184-237">tamanho de saudação de um nó só pode ser selecionado durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="e3184-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="e3184-238">Você pode encontrar uma lista de saudação diferentes tamanhos VM disponíveis para HDInsight no hello [página de preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e3184-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="e3184-239">Ao criar um cluster, você pode especificar o tamanho de saudação de nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3184-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="e3184-240">Olá informações a seguir fornecem orientação sobre como toospecify Olá tamanho usando Olá [portal do Azure][preview-portal], [Azure PowerShell][azure-powershell], e hello [CLI do Azure][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="e3184-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="e3184-241">**Portal do Azure**: ao criar um cluster, você pode definir o tamanho de saudação de nós Olá usados pelo cluster hello:</span><span class="sxs-lookup"><span data-stu-id="e3184-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![Imagem do Assistente de criação de cluster com a seleção de tamanho do nó](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="e3184-243">**CLI do Azure**: ao usar o hello `azure hdinsight cluster create` de comando, você pode definir o tamanho de saudação do cabeçalho hello, trabalho e nós ZooKeeper usando Olá `--headNodeSize`, `--workerNodeSize`, e `--zookeeperNodeSize` parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e3184-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="e3184-244">**O Azure PowerShell**: ao usar o hello `New-AzureRmHDInsightCluster` cmdlet, você pode definir o tamanho de saudação do cabeçalho hello, trabalho e nós ZooKeeper usando Olá `-HeadNodeVMSize`, `-WorkerNodeSize`, e `-ZookeeperNodeSize` parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e3184-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3184-245">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3184-245">Next steps</span></span>

<span data-ttu-id="e3184-246">Use Olá seguindo os links toolearn mais coisas mencionados neste documento.</span><span class="sxs-lookup"><span data-stu-id="e3184-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="e3184-247">Referência REST do Ambari</span><span class="sxs-lookup"><span data-stu-id="e3184-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="e3184-248">Instalar e configurar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e3184-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="e3184-249">Instalar e configurar o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="e3184-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="e3184-250">Gerenciar clusters HDInsight usando o Ambari</span><span class="sxs-lookup"><span data-stu-id="e3184-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="e3184-251">Provisionar os clusters HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="e3184-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
