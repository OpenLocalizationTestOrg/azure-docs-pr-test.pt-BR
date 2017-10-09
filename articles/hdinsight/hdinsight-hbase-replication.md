---
title: "replicação de cluster HBase aaaConfigure dentro das redes virtuais - Azure | Microsoft Docs"
description: "Saiba como tooconfigure HBase replicação para balanceamento de carga e alta disponibilidade, sem tempo de inatividade migração/atualização de um tooanother de versão do HDInsight e recuperação de desastres."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="4465d-103">Configurar a replicação de cluster HBase dentro das redes virtuais</span><span class="sxs-lookup"><span data-stu-id="4465d-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="4465d-104">Saiba como tooconfigure HBase replicação em uma rede virtual (VNet) ou entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="4465d-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="4465d-105">A replicação de cluster usa uma metodologia de envio de origem.</span><span class="sxs-lookup"><span data-stu-id="4465d-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="4465d-106">Um cluster HBase pode ser uma fonte, um destino ou pode atender a ambas as funções de uma vez.</span><span class="sxs-lookup"><span data-stu-id="4465d-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="4465d-107">A replicação é assíncrona e objetivo de saudação de replicação é consistência eventual.</span><span class="sxs-lookup"><span data-stu-id="4465d-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="4465d-108">Quando origem Olá recebe uma família de coluna Editar tooa com replicação habilitada, essa edição é propagado tooall clusters de destino.</span><span class="sxs-lookup"><span data-stu-id="4465d-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="4465d-109">Quando dados são replicados de um tooanother de cluster, cluster de origem hello e todos os clusters que já consumiram dados saudação são controladas tooprevent loops de replicação.</span><span class="sxs-lookup"><span data-stu-id="4465d-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="4465d-110">Neste tutorial, você configurará uma replicação de origem/destino.</span><span class="sxs-lookup"><span data-stu-id="4465d-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="4465d-111">Para obter outras topologias de cluster, consulte o [Guia de referência do Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="4465d-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="4465d-112">Casos de uso de replicação de HBase para uma única rede virtual:</span><span class="sxs-lookup"><span data-stu-id="4465d-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="4465d-113">O balanceamento de carga – por exemplo, executando verificações ou trabalhos MapReduce no cluster de destino hello e ingestão de dados no cluster de origem Olá</span><span class="sxs-lookup"><span data-stu-id="4465d-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="4465d-114">Alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="4465d-114">High availability</span></span>
* <span data-ttu-id="4465d-115">Migração de dados de um tooanother de cluster HBase</span><span class="sxs-lookup"><span data-stu-id="4465d-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="4465d-116">Atualizando um cluster Azure HDInsight de um tooanother de versão</span><span class="sxs-lookup"><span data-stu-id="4465d-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="4465d-117">Casos de uso de replicação de HBase para duas redes virtuais:</span><span class="sxs-lookup"><span data-stu-id="4465d-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="4465d-118">Recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="4465d-118">Disaster recovery</span></span>
* <span data-ttu-id="4465d-119">Balanceamento de carga e particionamento aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="4465d-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="4465d-120">Alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="4465d-120">High availability</span></span>

<span data-ttu-id="4465d-121">Replicar clusters usando scripts [ação de script](hdinsight-hadoop-customize-cluster-linux.md) localizados no [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="4465d-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4465d-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4465d-122">Prerequisites</span></span>
<span data-ttu-id="4465d-123">Antes de começar este tutorial, você deverá ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4465d-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="4465d-124">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="4465d-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="4465d-125">Configurar ambientes de saudação</span><span class="sxs-lookup"><span data-stu-id="4465d-125">Configure hello environments</span></span>

<span data-ttu-id="4465d-126">Há três opções de configuração possíveis:</span><span class="sxs-lookup"><span data-stu-id="4465d-126">There are three possible configurations:</span></span>

- <span data-ttu-id="4465d-127">Dois clusters de HBase em uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="4465d-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="4465d-128">Dois clusters HBase em duas redes virtuais diferentes no hello mesma região</span><span class="sxs-lookup"><span data-stu-id="4465d-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="4465d-129">Dois clusters de HBase em duas redes virtuais diferentes em duas regiões diferentes (replicação geográfica)</span><span class="sxs-lookup"><span data-stu-id="4465d-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="4465d-130">toomake-ambientes de saudação tooconfigure mais fácil, criamos alguns [modelos do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4465d-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="4465d-131">Se você preferir ambientes de saudação tooconfigure usando outros métodos, consulte:</span><span class="sxs-lookup"><span data-stu-id="4465d-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="4465d-132">Criar clusters Hadoop baseados em Linux em HDInsight</span><span class="sxs-lookup"><span data-stu-id="4465d-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="4465d-133">Criar clusters HBase na rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="4465d-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="4465d-134">Configurar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="4465d-134">Configure one virtual network</span></span>

<span data-ttu-id="4465d-135">Clique em Olá imagem toocreate dois clusters HBase em Olá a seguir mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4465d-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="4465d-136">Olá está armazenado na [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="4465d-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="4465d-137">Configurar duas redes virtuais no hello mesma região</span><span class="sxs-lookup"><span data-stu-id="4465d-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="4465d-138">Clique em Olá imagem toocreate duas redes virtuais com o emparelhamento de rede virtual e dois clusters HBase em Olá a seguir mesma região.</span><span class="sxs-lookup"><span data-stu-id="4465d-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="4465d-139">Olá está armazenado na [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="4465d-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="4465d-140">Esse cenário requer o [emparelhamento VNet](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4465d-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="4465d-141">modelo de saudação permite o emparelhamento de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4465d-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="4465d-142">A replicação do HBase usa endereços IP de saudação ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="4465d-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="4465d-143">Você deve configurar endereços IP estáticos para nós de HBase ZooKeeper de destino hello.</span><span class="sxs-lookup"><span data-stu-id="4465d-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="4465d-144">**endereços IP estáticos tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="4465d-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="4465d-145">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4465d-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4465d-146">No menu à esquerda do hello, clique em **grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="4465d-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="4465d-147">Clique em seu grupo de recursos que contém Olá destino HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="4465d-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="4465d-148">Este é o grupo de recursos de saudação que você especificou quando você usou o ambiente de saudação toocreate do modelo de Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4465d-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="4465d-149">Você pode usar o hello toonarrow de filtro para baixo na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="4465d-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="4465d-150">Você pode ver uma lista de recursos que contém duas redes virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="4465d-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="4465d-151">Clique em Olá rede virtual que contenha Olá destino HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="4465d-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="4465d-152">Por exemplo, clique em **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="4465d-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="4465d-153">É possível ver três dispositivos com nomes que começam com **nic-zookeepermode-**.</span><span class="sxs-lookup"><span data-stu-id="4465d-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="4465d-154">Esses dispositivos são Olá três ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="4465d-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="4465d-155">Clique em uma saudação ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="4465d-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="4465d-156">Clique em **Configurações de IP**.</span><span class="sxs-lookup"><span data-stu-id="4465d-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="4465d-157">Clique em **ipConfig1** na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="4465d-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="4465d-158">Clique em **estático**e anote o endereço IP real de saudação.</span><span class="sxs-lookup"><span data-stu-id="4465d-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="4465d-159">Você precisará de endereço IP hello quando você executa a replicação de tooenable de ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="4465d-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![IP estático do ZooKeeper para replicação de HBase no HDInsight](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="4465d-161">Repita a etapa 6 tooset Olá endereço IP para Olá outros dois nós ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="4465d-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="4465d-162">Para o cenário de rede entre hello, você deve usar o hello **- ip** alternar ao chamar hello **hdi_enable_replication.sh** ação de script.</span><span class="sxs-lookup"><span data-stu-id="4465d-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="4465d-163">Configurar duas redes virtuais em duas regiões diferentes</span><span class="sxs-lookup"><span data-stu-id="4465d-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="4465d-164">Clique em Olá seguinte imagem toocreate duas redes virtuais em duas regiões diferentes.</span><span class="sxs-lookup"><span data-stu-id="4465d-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="4465d-165">Olá modelo é armazenado em um contêiner de Blob do Azure público.</span><span class="sxs-lookup"><span data-stu-id="4465d-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="4465d-166">Crie um gateway VPN entre duas redes virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="4465d-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="4465d-167">Para obter instruções, veja [Criar uma VNet com uma conexão site a site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4465d-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="4465d-168">A replicação do HBase usa endereços IP de saudação ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="4465d-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="4465d-169">Você deve configurar endereços IP estáticos para nós de HBase ZooKeeper de destino hello.</span><span class="sxs-lookup"><span data-stu-id="4465d-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="4465d-170">tooconfigure IP estático, consulte a seção "configurar duas redes virtuais Olá mesma região" hello neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4465d-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="4465d-171">Para o cenário de rede entre hello, você deve usar o hello **- ip** alternar ao chamar hello **hdi_enable_replication.sh** ação de script.</span><span class="sxs-lookup"><span data-stu-id="4465d-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="4465d-172">Carregar dados de teste</span><span class="sxs-lookup"><span data-stu-id="4465d-172">Load test data</span></span>

<span data-ttu-id="4465d-173">Quando você replica um cluster, você deve especificar Olá tabelas tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="4465d-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="4465d-174">Nesta seção, você irá carregar alguns dados em cluster de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="4465d-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="4465d-175">Na próxima seção, Olá, você habilitará a replicação entre dois clusters de saudação.</span><span class="sxs-lookup"><span data-stu-id="4465d-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="4465d-176">Siga as instruções de saudação em [HBase tutorial: começar a usar o Apache HBase com Hadoop baseado em Linux no HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate um **contatos** tabela e insira alguns dados na tabela hello.</span><span class="sxs-lookup"><span data-stu-id="4465d-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="4465d-177">Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="4465d-177">Enable replication</span></span>

<span data-ttu-id="4465d-178">Olá, as etapas a seguir mostra como toocall Olá script de ação de script de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4465d-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="4465d-179">Para executar uma ação de script usando o PowerShell do Azure e hello interface de linha de comando (CLI) do Azure, consulte [HDInsight baseados em Linux personalizar clusters usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4465d-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="4465d-180">**replicação do HBase tooenable de saudação portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="4465d-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="4465d-181">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4465d-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4465d-182">Abra o cluster do hello fonte HBase.</span><span class="sxs-lookup"><span data-stu-id="4465d-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="4465d-183">No menu de cluster hello, clique em **ações de Script**.</span><span class="sxs-lookup"><span data-stu-id="4465d-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="4465d-184">Clique em **Enviar nova** da parte superior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="4465d-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="4465d-185">Selecione ou insira Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="4465d-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="4465d-186">**Nome**: insira **Habilitar a replicação**.</span><span class="sxs-lookup"><span data-stu-id="4465d-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="4465d-187">**URL do Script Bash**: insira **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="4465d-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="4465d-188">**Cabeçalho**: selecionado.</span><span class="sxs-lookup"><span data-stu-id="4465d-188">**Head**: Selected.</span></span> <span data-ttu-id="4465d-189">Olá desmarque os outros tipos de nó.</span><span class="sxs-lookup"><span data-stu-id="4465d-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="4465d-190">**Parâmetros**: seguinte Olá parâmetros habilitar replicação para todas as tabelas existentes de saudação de exemplo e copiar todos os dados de saudação do cluster de destino toohello do cluster de origem hello:</span><span class="sxs-lookup"><span data-stu-id="4465d-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="4465d-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4465d-191">Click **Create**.</span></span> <span data-ttu-id="4465d-192">script Hello pode levar algum tempo, especialmente quando o argumento de copydata - Olá é usado.</span><span class="sxs-lookup"><span data-stu-id="4465d-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="4465d-193">Argumentos necessários:</span><span class="sxs-lookup"><span data-stu-id="4465d-193">Required arguments:</span></span>

|<span data-ttu-id="4465d-194">Nome</span><span class="sxs-lookup"><span data-stu-id="4465d-194">Name</span></span>|<span data-ttu-id="4465d-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="4465d-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="4465d-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="4465d-196">-s, --src-cluster</span></span> | <span data-ttu-id="4465d-197">Especifique o nome DNS de saudação do cluster do hello fonte HBase.</span><span class="sxs-lookup"><span data-stu-id="4465d-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="4465d-198">Por exemplo: -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="4465d-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="4465d-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="4465d-199">-d, --dst-cluster</span></span> | <span data-ttu-id="4465d-200">Especifique o nome DNS de saudação do destino hello (réplica) cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="4465d-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="4465d-201">Por exemplo: -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="4465d-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="4465d-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="4465d-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="4465d-203">Especifica senha do administrador Olá para Ambari no cluster do hello origem HBase.</span><span class="sxs-lookup"><span data-stu-id="4465d-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="4465d-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="4465d-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="4465d-205">Especifica senha do administrador Olá para Ambari no cluster do hello destino HBase.</span><span class="sxs-lookup"><span data-stu-id="4465d-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="4465d-206">Argumentos opcionais:</span><span class="sxs-lookup"><span data-stu-id="4465d-206">Optional arguments:</span></span>

|<span data-ttu-id="4465d-207">Nome</span><span class="sxs-lookup"><span data-stu-id="4465d-207">Name</span></span>|<span data-ttu-id="4465d-208">Descrição</span><span class="sxs-lookup"><span data-stu-id="4465d-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="4465d-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="4465d-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="4465d-210">Especifique o nome de usuário de administrador de Olá para Ambari no cluster do hello origem HBase.</span><span class="sxs-lookup"><span data-stu-id="4465d-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="4465d-211">valor padrão de saudação é **admin**.</span><span class="sxs-lookup"><span data-stu-id="4465d-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="4465d-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="4465d-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="4465d-213">Especifique o nome de usuário de administrador de Olá para Ambari no cluster do hello destino HBase.</span><span class="sxs-lookup"><span data-stu-id="4465d-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="4465d-214">valor padrão de saudação é **admin**.</span><span class="sxs-lookup"><span data-stu-id="4465d-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="4465d-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="4465d-215">-t, --table-list</span></span> | <span data-ttu-id="4465d-216">Especifique Olá toobe de tabelas replicada.</span><span class="sxs-lookup"><span data-stu-id="4465d-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="4465d-217">Por exemplo: --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="4465d-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="4465d-218">Se você não especificar tabelas, todas as tabelas HBase existentes serão replicadas.</span><span class="sxs-lookup"><span data-stu-id="4465d-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="4465d-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="4465d-219">-m, --machine</span></span> | <span data-ttu-id="4465d-220">Especifique o nó principal Olá onde a ação de script hello será executado.</span><span class="sxs-lookup"><span data-stu-id="4465d-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="4465d-221">valor de saudação é hn1 ou hn0.</span><span class="sxs-lookup"><span data-stu-id="4465d-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="4465d-222">Como hn0 geralmente está mais ocupado, é recomendável usar hn1.</span><span class="sxs-lookup"><span data-stu-id="4465d-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="4465d-223">Você usar essa opção quando você estiver executando o script hello $0 como uma ação de script do portal de HDInsight hello ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4465d-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="4465d-224">-ip</span><span class="sxs-lookup"><span data-stu-id="4465d-224">-ip</span></span> | <span data-ttu-id="4465d-225">Esse argumento é necessário quando você estiver habilitando a replicação entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="4465d-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="4465d-226">Esse argumento atua como um comutador toouse Olá estático IPs de ZooKeeper nós de clusters de réplica em vez de nomes FQDN.</span><span class="sxs-lookup"><span data-stu-id="4465d-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="4465d-227">Olá estático IPs necessário toobe pré-configurado antes de habilitar a replicação.</span><span class="sxs-lookup"><span data-stu-id="4465d-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="4465d-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="4465d-228">-cp, -copydata</span></span> | <span data-ttu-id="4465d-229">Habilite a migração de saudação dos dados existentes nas tabelas de saudação em que a replicação está habilitada.</span><span class="sxs-lookup"><span data-stu-id="4465d-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="4465d-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="4465d-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="4465d-231">Habilite a replicação nas tabelas do sistema Phoenix.</span><span class="sxs-lookup"><span data-stu-id="4465d-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="4465d-232">*Use esta opção com cuidado.*</span><span class="sxs-lookup"><span data-stu-id="4465d-232">*Use this option with caution.*</span></span> <span data-ttu-id="4465d-233">É recomendável que você recrie tabelas Phoenix em clusters de réplica antes de usar esse script.</span><span class="sxs-lookup"><span data-stu-id="4465d-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="4465d-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="4465d-234">-h, --help</span></span> | <span data-ttu-id="4465d-235">Exibir informações de uso.</span><span class="sxs-lookup"><span data-stu-id="4465d-235">Display usage information.</span></span> |

<span data-ttu-id="4465d-236">Olá Olá seção print_usage() [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) fornece uma explicação detalhada de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4465d-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="4465d-237">Após a ação de script hello com êxito implantado, você pode usar SSH tooconnect toohello destino HBase cluster e verificar dados saudação foi replicados.</span><span class="sxs-lookup"><span data-stu-id="4465d-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="4465d-238">Cenários de replicação</span><span class="sxs-lookup"><span data-stu-id="4465d-238">Replication scenarios</span></span>

<span data-ttu-id="4465d-239">Olá lista a seguir mostra alguns casos de uso geral e suas configurações de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="4465d-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="4465d-240">**Habilitar a replicação em todas as tabelas entre clusters Olá dois**.</span><span class="sxs-lookup"><span data-stu-id="4465d-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="4465d-241">Esse cenário não requer Olá/migração com cópia dos dados existentes nas tabelas de saudação e não usa tabelas Phoenix.</span><span class="sxs-lookup"><span data-stu-id="4465d-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="4465d-242">Use Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="4465d-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="4465d-243">**Habilitar a replicação em tabelas específicas**.</span><span class="sxs-lookup"><span data-stu-id="4465d-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="4465d-244">Use Olá seguindo a replicação tooenable parâmetros na table1, table2 e Tabela3:</span><span class="sxs-lookup"><span data-stu-id="4465d-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="4465d-245">**Habilitar a replicação em tabelas específicas e copie os dados existentes Olá**.</span><span class="sxs-lookup"><span data-stu-id="4465d-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="4465d-246">Use Olá seguindo a replicação tooenable parâmetros na table1, table2 e Tabela3:</span><span class="sxs-lookup"><span data-stu-id="4465d-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="4465d-247">**Habilitar a replicação em todas as tabelas com replicando phoenix metadados de origem toodestination**.</span><span class="sxs-lookup"><span data-stu-id="4465d-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="4465d-248">A replicação de metadados Phoenix não é ideal e deve ser habilitada com cuidado.</span><span class="sxs-lookup"><span data-stu-id="4465d-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="4465d-249">Copiar e migrar dados</span><span class="sxs-lookup"><span data-stu-id="4465d-249">Copy and migrate data</span></span>

<span data-ttu-id="4465d-250">Há dois scripts de ação de script separados para copiar/migrar dados após a replicação ser habilitada:</span><span class="sxs-lookup"><span data-stu-id="4465d-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="4465d-251">[Script para tabelas pequenas](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (alguns gigabytes de tamanho e geral cópia é toofinish esperado em menos de uma hora)</span><span class="sxs-lookup"><span data-stu-id="4465d-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="4465d-252">[Script para tabelas grandes](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (esperado tootake mais de uma hora toocopy)</span><span class="sxs-lookup"><span data-stu-id="4465d-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="4465d-253">Você pode seguir Olá mesmo procedimento no [habilitar replicação](#enable-replication) toocall ação de script hello com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="4465d-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="4465d-254">Olá Olá seção print_usage() [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) fornece uma descrição detalhada dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4465d-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="4465d-255">Cenários</span><span class="sxs-lookup"><span data-stu-id="4465d-255">Scenarios</span></span>

- <span data-ttu-id="4465d-256">**Copiar tabelas específicas (test1, test2 e test3) para todas as linhas editadas até o momento (carimbo de hora atual)**:</span><span class="sxs-lookup"><span data-stu-id="4465d-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="4465d-257">ou o</span><span class="sxs-lookup"><span data-stu-id="4465d-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="4465d-258">**Copiar tabelas específicas com intervalo de tempo especificado**:</span><span class="sxs-lookup"><span data-stu-id="4465d-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="4465d-259">Desabilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="4465d-259">Disable replication</span></span>

<span data-ttu-id="4465d-260">replicação toodisable, você usa outro script de ação de script localizado em [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="4465d-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="4465d-261">Você pode seguir Olá mesmo procedimento no [habilitar replicação](#enable-replication) toocall ação de script hello com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="4465d-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="4465d-262">Olá Olá seção print_usage() [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) fornece uma explicação detalhada de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4465d-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="4465d-263">Cenários</span><span class="sxs-lookup"><span data-stu-id="4465d-263">Scenarios</span></span>

- <span data-ttu-id="4465d-264">**Desabilitar a replicação em todas as tabelas**:</span><span class="sxs-lookup"><span data-stu-id="4465d-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="4465d-265">ou o</span><span class="sxs-lookup"><span data-stu-id="4465d-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="4465d-266">**Desabilitar a replicação em tabelas específicas (table1, table2 e table3)**:</span><span class="sxs-lookup"><span data-stu-id="4465d-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="4465d-267">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4465d-267">Next steps</span></span>

<span data-ttu-id="4465d-268">Neste tutorial, você aprendeu como tooconfigure HBase replicação entre dois datacenters.</span><span class="sxs-lookup"><span data-stu-id="4465d-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="4465d-269">toolearn mais sobre o HDInsight e HBase, consulte:</span><span class="sxs-lookup"><span data-stu-id="4465d-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="4465d-270">[Introdução ao Apache HBase no HDInsight][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="4465d-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="4465d-271">[Visão geral do HDInsight HBase][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="4465d-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="4465d-272">[Criar clusters HBase na rede virtual do Azure][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="4465d-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="4465d-273">[Analisar o sentimento do Twitter em tempo real com o HBase][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="4465d-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="4465d-274">[Analisar dados de sensor com o Storm e o HBase no HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="4465d-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
