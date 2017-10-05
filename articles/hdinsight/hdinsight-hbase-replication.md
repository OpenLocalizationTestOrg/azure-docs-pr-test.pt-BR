---
title: "Configurar a replicação de cluster HBase dentro das redes virtuais – Azure | Microsoft Docs"
description: "Saiba como configurar a replicação de HBase para balanceamento de carga, alta disponibilidade, migração/atualização de uma versão do HDInsight para outra sem tempo de inatividade e recuperação de desastres."
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
ms.openlocfilehash: 895709391486acb4a9d7a54ef046956539913f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="ef943-103">Configurar a replicação de cluster HBase dentro das redes virtuais</span><span class="sxs-lookup"><span data-stu-id="ef943-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="ef943-104">Saiba como configurar a replicação de HBase em uma rede virtual (VNet) ou entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ef943-104">Learn how to configure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="ef943-105">A replicação de cluster usa uma metodologia de envio de origem.</span><span class="sxs-lookup"><span data-stu-id="ef943-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="ef943-106">Um cluster HBase pode ser uma fonte, um destino ou pode atender a ambas as funções de uma vez.</span><span class="sxs-lookup"><span data-stu-id="ef943-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="ef943-107">A replicação é assíncrona e o objetivo da replicação é a consistência eventual.</span><span class="sxs-lookup"><span data-stu-id="ef943-107">Replication is asynchronous, and the goal of replication is eventual consistency.</span></span> <span data-ttu-id="ef943-108">Quando a origem recebe uma edição para uma família de coluna com replicação habilitada, essa edição é propagada para todos os clusters de destino.</span><span class="sxs-lookup"><span data-stu-id="ef943-108">When the source receives an edit to a column family with replication enabled, that edit is propagated to all destination clusters.</span></span> <span data-ttu-id="ef943-109">Quando os dados são replicados de um cluster para outro, o cluster de origem e todos os clusters que já consumiram os dados são rastreados para evitar loops de replicação.</span><span class="sxs-lookup"><span data-stu-id="ef943-109">When data is replicated from one cluster to another, the source cluster and all clusters that have already consumed the data are tracked to prevent replication loops.</span></span>

<span data-ttu-id="ef943-110">Neste tutorial, você configurará uma replicação de origem/destino.</span><span class="sxs-lookup"><span data-stu-id="ef943-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="ef943-111">Para obter outras topologias de cluster, consulte o [Guia de referência do Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="ef943-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="ef943-112">Casos de uso de replicação de HBase para uma única rede virtual:</span><span class="sxs-lookup"><span data-stu-id="ef943-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="ef943-113">Balanceamento de carga: por exemplo, executando verificações ou trabalhos MapReduce no cluster de destino e ingestão de dados no cluster de origem</span><span class="sxs-lookup"><span data-stu-id="ef943-113">Load balancing--for example, running scans or MapReduce jobs on the destination cluster and ingesting data on the source cluster</span></span>
* <span data-ttu-id="ef943-114">Alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="ef943-114">High availability</span></span>
* <span data-ttu-id="ef943-115">Migrar dados de um cluster de HBase para outro</span><span class="sxs-lookup"><span data-stu-id="ef943-115">Migrating data from one HBase cluster to another</span></span>
* <span data-ttu-id="ef943-116">Atualizar um cluster HDInsight do Azure de uma versão para outra</span><span class="sxs-lookup"><span data-stu-id="ef943-116">Upgrading an Azure HDInsight cluster from one version to another</span></span>

<span data-ttu-id="ef943-117">Casos de uso de replicação de HBase para duas redes virtuais:</span><span class="sxs-lookup"><span data-stu-id="ef943-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="ef943-118">Recuperação de desastre</span><span class="sxs-lookup"><span data-stu-id="ef943-118">Disaster recovery</span></span>
* <span data-ttu-id="ef943-119">Balanceamento de carga e particionamento do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ef943-119">Load balancing and partitioning the application</span></span>
* <span data-ttu-id="ef943-120">Alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="ef943-120">High availability</span></span>

<span data-ttu-id="ef943-121">Replicar clusters usando scripts [ação de script](hdinsight-hadoop-customize-cluster-linux.md) localizados no [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="ef943-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef943-122">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ef943-122">Prerequisites</span></span>
<span data-ttu-id="ef943-123">Antes de começar este tutorial, você deverá ter uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef943-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="ef943-124">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ef943-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-the-environments"></a><span data-ttu-id="ef943-125">Configurar os ambientes</span><span class="sxs-lookup"><span data-stu-id="ef943-125">Configure the environments</span></span>

<span data-ttu-id="ef943-126">Há três opções de configuração possíveis:</span><span class="sxs-lookup"><span data-stu-id="ef943-126">There are three possible configurations:</span></span>

- <span data-ttu-id="ef943-127">Dois clusters de HBase em uma rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="ef943-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="ef943-128">Dois clusters de HBase em duas redes virtuais diferentes na mesma região</span><span class="sxs-lookup"><span data-stu-id="ef943-128">Two HBase clusters in two different virtual networks in the same region</span></span>
- <span data-ttu-id="ef943-129">Dois clusters de HBase em duas redes virtuais diferentes em duas regiões diferentes (replicação geográfica)</span><span class="sxs-lookup"><span data-stu-id="ef943-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="ef943-130">Para facilitar a configuração dos ambientes, nós criamos alguns [modelos do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef943-130">To make it easier to configure the environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ef943-131">Se você preferir configurar os ambientes usando outros métodos, veja:</span><span class="sxs-lookup"><span data-stu-id="ef943-131">If you prefer to configure the environments by using other methods, see:</span></span>

- [<span data-ttu-id="ef943-132">Criar clusters Hadoop baseados em Linux em HDInsight</span><span class="sxs-lookup"><span data-stu-id="ef943-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="ef943-133">Criar clusters HBase na rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="ef943-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="ef943-134">Configurar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="ef943-134">Configure one virtual network</span></span>

<span data-ttu-id="ef943-135">Clique na imagem a seguir para criar dois clusters HBase na mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="ef943-135">Click the following image to create two HBase clusters in the same virtual network.</span></span> <span data-ttu-id="ef943-136">O modelo está armazenado em [Modelos de Início Rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="ef943-136">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

### <a name="configure-two-virtual-networks-in-the-same-region"></a><span data-ttu-id="ef943-137">Configurar duas redes virtuais na mesma região</span><span class="sxs-lookup"><span data-stu-id="ef943-137">Configure two virtual networks in the same region</span></span>

<span data-ttu-id="ef943-138">Clique na imagem a seguir para criar duas redes virtuais com emparelhamento VNet e dois clusters HBase na mesma região.</span><span class="sxs-lookup"><span data-stu-id="ef943-138">Click the following image to create two virtual networks with VNet peering and two HBase clusters in the same region.</span></span> <span data-ttu-id="ef943-139">O modelo está armazenado em [Modelos de Início Rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="ef943-139">The template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>



<span data-ttu-id="ef943-140">Esse cenário requer o [emparelhamento VNet](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ef943-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="ef943-141">O modelo permite o emparelhamento VNet.</span><span class="sxs-lookup"><span data-stu-id="ef943-141">The template enables VNet peering.</span></span>   

<span data-ttu-id="ef943-142">A replicação de HBase usa endereços IP das VMs do ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="ef943-142">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="ef943-143">Você deve configurar endereços IP estáticos para os nós de destino do HBase ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="ef943-143">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="ef943-144">**Para configurar endereços IP estáticos**</span><span class="sxs-lookup"><span data-stu-id="ef943-144">**To configure static IP addresses**</span></span>

1. <span data-ttu-id="ef943-145">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef943-145">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ef943-146">No menu à esquerda, clique em **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="ef943-146">From the left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="ef943-147">Clique em seu grupo de recursos que contém o cluster HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="ef943-147">Click your resource group that contains the destination HBase cluster.</span></span> <span data-ttu-id="ef943-148">Esse é o grupo de recursos que você especificou ao usar o modelo do Resource Manager para criar o ambiente.</span><span class="sxs-lookup"><span data-stu-id="ef943-148">This is the resource group that you specified when you used the Resource Manager template to create the environment.</span></span> <span data-ttu-id="ef943-149">Você pode usar o filtro para restringir a lista.</span><span class="sxs-lookup"><span data-stu-id="ef943-149">You can use the filter to narrow down the list.</span></span> <span data-ttu-id="ef943-150">É possível exibir uma lista de recursos que contém as duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ef943-150">You can see a list of resources that contains the two virtual networks.</span></span>
4. <span data-ttu-id="ef943-151">Clique na rede virtual que contém o cluster HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="ef943-151">Click the virtual network that contains the destination HBase cluster.</span></span> <span data-ttu-id="ef943-152">Por exemplo, clique em **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="ef943-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="ef943-153">É possível ver três dispositivos com nomes que começam com **nic-zookeepermode-**.</span><span class="sxs-lookup"><span data-stu-id="ef943-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="ef943-154">Esses dispositivos são as três VMs do ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="ef943-154">Those devices are the three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="ef943-155">Clique em uma das VMs do ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="ef943-155">Click one of the ZooKeeper VMs.</span></span>
6. <span data-ttu-id="ef943-156">Clique em **Configurações de IP**.</span><span class="sxs-lookup"><span data-stu-id="ef943-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="ef943-157">Clique em **ipConfig1** na lista.</span><span class="sxs-lookup"><span data-stu-id="ef943-157">Click **ipConfig1** from the list.</span></span>
8. <span data-ttu-id="ef943-158">Clique em **Estático** e anote o endereço IP real.</span><span class="sxs-lookup"><span data-stu-id="ef943-158">Click **Static**, and write down the actual IP address.</span></span> <span data-ttu-id="ef943-159">Você precisará do endereço IP ao executar a ação de script para habilitar a replicação.</span><span class="sxs-lookup"><span data-stu-id="ef943-159">You will need the IP address when you run the script action to enable replication.</span></span>

  ![IP estático do ZooKeeper para replicação de HBase no HDInsight](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="ef943-161">Repita a etapa 6 para definir o endereço IP estático para os outros dois nós ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="ef943-161">Repeat step 6 to set the static IP address for the other two ZooKeeper nodes.</span></span>

<span data-ttu-id="ef943-162">Para o cenário de rede virtual cruzada, você deve usar a opção **-ip** ao chamar a ação de script **hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="ef943-162">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="ef943-163">Configurar duas redes virtuais em duas regiões diferentes</span><span class="sxs-lookup"><span data-stu-id="ef943-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="ef943-164">Clique na imagem a seguir para criar duas redes virtuais em duas regiões diferentes.</span><span class="sxs-lookup"><span data-stu-id="ef943-164">Click the following image to create two virtual networks in two different regions.</span></span> <span data-ttu-id="ef943-165">O modelo está localizado em um contêiner de blob público do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef943-165">The template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy to Azure"></a>

<span data-ttu-id="ef943-166">Crie um gateway de VPN entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ef943-166">Create a VPN gateway between the two virtual networks.</span></span> <span data-ttu-id="ef943-167">Para obter instruções, veja [Criar uma VNet com uma conexão site a site](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ef943-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="ef943-168">A replicação de HBase usa endereços IP das VMs do ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="ef943-168">HBase replication uses IP addresses of the ZooKeeper VMs.</span></span> <span data-ttu-id="ef943-169">Você deve configurar endereços IP estáticos para os nós de destino do HBase ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="ef943-169">You must configure static IP addresses for the destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="ef943-170">Para configurar o endereço IP estático, veja a seção "Configurar duas redes virtuais na mesma região" neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ef943-170">To configure static IP, see the "Configure two virtual networks in the same region" section in this article.</span></span>

<span data-ttu-id="ef943-171">Para o cenário de rede virtual cruzada, você deve usar a opção **-ip** ao chamar a ação de script **hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="ef943-171">For the cross-VNet scenario, you must use the **-ip** switch when calling the **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="ef943-172">Carregar dados de teste</span><span class="sxs-lookup"><span data-stu-id="ef943-172">Load test data</span></span>

<span data-ttu-id="ef943-173">Ao replicar um cluster, você deve especificar as tabelas a serem replicadas.</span><span class="sxs-lookup"><span data-stu-id="ef943-173">When you replicate a cluster, you must specify the tables to replicate.</span></span> <span data-ttu-id="ef943-174">Nesta seção, você carregará alguns dados no cluster de origem.</span><span class="sxs-lookup"><span data-stu-id="ef943-174">In this section, you will load some data into the source cluster.</span></span> <span data-ttu-id="ef943-175">Na próxima seção, você habilitará a replicação entre os dois clusters.</span><span class="sxs-lookup"><span data-stu-id="ef943-175">In the next section, you will enable replication between the two clusters.</span></span>

<span data-ttu-id="ef943-176">Siga as instruções em [Tutorial do HBase: Introdução ao uso do Apache HBase com o Hadoop baseado em Linux no HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) para criar uma tabela **Contatos** e inserir alguns dados na tabela.</span><span class="sxs-lookup"><span data-stu-id="ef943-176">Follow the instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) to create a **Contacts** table and insert some data into the table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="ef943-177">Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="ef943-177">Enable replication</span></span>

<span data-ttu-id="ef943-178">As etapas a seguir mostram como chamar o script de ação de script no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ef943-178">The following steps show how to call the script action script from the Azure portal.</span></span> <span data-ttu-id="ef943-179">Para executar uma ação de script usando o Azure PowerShell e a CLI (interface de linha de comando) do Azure, veja [Personalizar clusters HDInsight baseados em Linux usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ef943-179">For running a script action by using Azure PowerShell and the Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="ef943-180">**Para habilitar a replicação de HBase no Portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="ef943-180">**To enable HBase replication from the Azure portal**</span></span>

1. <span data-ttu-id="ef943-181">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef943-181">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ef943-182">Abra o cluster HBase de origem.</span><span class="sxs-lookup"><span data-stu-id="ef943-182">Open the source HBase cluster.</span></span>
3. <span data-ttu-id="ef943-183">No menu do cluster, clique em **Ações de Script**.</span><span class="sxs-lookup"><span data-stu-id="ef943-183">From the cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="ef943-184">Clique em **Enviar Novo** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="ef943-184">Click **Submit New** from the top of the blade.</span></span>
5. <span data-ttu-id="ef943-185">Selecione ou insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="ef943-185">Select or enter the following information:</span></span>

  - <span data-ttu-id="ef943-186">**Nome**: insira **Habilitar a replicação**.</span><span class="sxs-lookup"><span data-stu-id="ef943-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="ef943-187">**URL do Script Bash**: insira **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="ef943-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="ef943-188">**Cabeçalho**: selecionado.</span><span class="sxs-lookup"><span data-stu-id="ef943-188">**Head**: Selected.</span></span> <span data-ttu-id="ef943-189">Desmarque os outros tipos de nós.</span><span class="sxs-lookup"><span data-stu-id="ef943-189">Clear the other node types.</span></span>
  - <span data-ttu-id="ef943-190">**Parâmetros**: os seguintes parâmetros de exemplo habilitam a replicação de todas as tabelas existentes e copiam todos os dados do cluster de origem para o cluster de destino:</span><span class="sxs-lookup"><span data-stu-id="ef943-190">**Parameters**: The following sample parameters enable replication for all the existing tables and copy all the data from the source cluster to the destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="ef943-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ef943-191">Click **Create**.</span></span> <span data-ttu-id="ef943-192">O script pode demorar, especialmente quando o argumento -copydata for usado.</span><span class="sxs-lookup"><span data-stu-id="ef943-192">The script can take some time, especially when the -copydata argument is used.</span></span>

<span data-ttu-id="ef943-193">Argumentos necessários:</span><span class="sxs-lookup"><span data-stu-id="ef943-193">Required arguments:</span></span>

|<span data-ttu-id="ef943-194">Nome</span><span class="sxs-lookup"><span data-stu-id="ef943-194">Name</span></span>|<span data-ttu-id="ef943-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="ef943-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="ef943-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="ef943-196">-s, --src-cluster</span></span> | <span data-ttu-id="ef943-197">Especifique o nome DNS do cluster HBase de origem.</span><span class="sxs-lookup"><span data-stu-id="ef943-197">Specify the DNS name of the source HBase cluster.</span></span> <span data-ttu-id="ef943-198">Por exemplo: -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="ef943-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="ef943-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="ef943-199">-d, --dst-cluster</span></span> | <span data-ttu-id="ef943-200">Especifique o nome DNS do cluster HBase de destino (réplica).</span><span class="sxs-lookup"><span data-stu-id="ef943-200">Specify the DNS name of the destination (replica) HBase cluster.</span></span> <span data-ttu-id="ef943-201">Por exemplo: -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="ef943-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="ef943-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="ef943-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="ef943-203">Especifique a senha de administrador para Ambari no cluster HBase de origem.</span><span class="sxs-lookup"><span data-stu-id="ef943-203">Specify the admin password for Ambari on the source HBase cluster.</span></span> |
|<span data-ttu-id="ef943-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="ef943-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="ef943-205">Especifique a senha de administrador para Ambari no cluster HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="ef943-205">Specify the admin password for Ambari on the destination HBase cluster.</span></span>|

<span data-ttu-id="ef943-206">Argumentos opcionais:</span><span class="sxs-lookup"><span data-stu-id="ef943-206">Optional arguments:</span></span>

|<span data-ttu-id="ef943-207">Nome</span><span class="sxs-lookup"><span data-stu-id="ef943-207">Name</span></span>|<span data-ttu-id="ef943-208">Descrição</span><span class="sxs-lookup"><span data-stu-id="ef943-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="ef943-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="ef943-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="ef943-210">Especifique o nome de usuário de administrador para Ambari no cluster HBase de origem.</span><span class="sxs-lookup"><span data-stu-id="ef943-210">Specify the admin username for Ambari on the source HBase cluster.</span></span> <span data-ttu-id="ef943-211">O valor padrão é **admin**.</span><span class="sxs-lookup"><span data-stu-id="ef943-211">The default value is **admin**.</span></span> |
|<span data-ttu-id="ef943-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="ef943-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="ef943-213">Especifique o nome de usuário de administrador para Ambari no cluster HBase de destino.</span><span class="sxs-lookup"><span data-stu-id="ef943-213">Specify the admin username for Ambari on the destination HBase cluster.</span></span> <span data-ttu-id="ef943-214">O valor padrão é **admin**.</span><span class="sxs-lookup"><span data-stu-id="ef943-214">The default value is **admin**.</span></span> |
|<span data-ttu-id="ef943-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="ef943-215">-t, --table-list</span></span> | <span data-ttu-id="ef943-216">Especifique as tabelas a replicar.</span><span class="sxs-lookup"><span data-stu-id="ef943-216">Specify the tables to be replicated.</span></span> <span data-ttu-id="ef943-217">Por exemplo: --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="ef943-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="ef943-218">Se você não especificar tabelas, todas as tabelas HBase existentes serão replicadas.</span><span class="sxs-lookup"><span data-stu-id="ef943-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="ef943-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="ef943-219">-m, --machine</span></span> | <span data-ttu-id="ef943-220">Especifique o nó de cabeçalho em que a ação de script será executada.</span><span class="sxs-lookup"><span data-stu-id="ef943-220">Specify the head node where the script action will run.</span></span> <span data-ttu-id="ef943-221">O valor é hn1 ou hn0.</span><span class="sxs-lookup"><span data-stu-id="ef943-221">The value is either hn1 or hn0.</span></span> <span data-ttu-id="ef943-222">Como hn0 geralmente está mais ocupado, é recomendável usar hn1.</span><span class="sxs-lookup"><span data-stu-id="ef943-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="ef943-223">Use essa opção quando estiver executando o script de $0 como uma ação de script do portal do HDInsight ou do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef943-223">You use this option when you're running the $0 script as a script action from the HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="ef943-224">-ip</span><span class="sxs-lookup"><span data-stu-id="ef943-224">-ip</span></span> | <span data-ttu-id="ef943-225">Esse argumento é necessário quando você estiver habilitando a replicação entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ef943-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="ef943-226">Esse argumento atua como uma opção para usar os IPs estáticos de nós ZooKeeper de clusters de réplica em vez de nomes FQDN.</span><span class="sxs-lookup"><span data-stu-id="ef943-226">This argument acts as a switch to use the static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="ef943-227">Os IPs estáticos precisam ser pré-configurados antes de habilitar a replicação.</span><span class="sxs-lookup"><span data-stu-id="ef943-227">The static IPs need to be preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="ef943-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="ef943-228">-cp, -copydata</span></span> | <span data-ttu-id="ef943-229">Habilite a migração dos dados existentes nas tabelas em que a replicação está habilitada.</span><span class="sxs-lookup"><span data-stu-id="ef943-229">Enable the migration of existing data on the tables where replication is enabled.</span></span> |
|<span data-ttu-id="ef943-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="ef943-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="ef943-231">Habilite a replicação nas tabelas do sistema Phoenix.</span><span class="sxs-lookup"><span data-stu-id="ef943-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="ef943-232">*Use esta opção com cuidado.*</span><span class="sxs-lookup"><span data-stu-id="ef943-232">*Use this option with caution.*</span></span> <span data-ttu-id="ef943-233">É recomendável que você recrie tabelas Phoenix em clusters de réplica antes de usar esse script.</span><span class="sxs-lookup"><span data-stu-id="ef943-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="ef943-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="ef943-234">-h, --help</span></span> | <span data-ttu-id="ef943-235">Exibir informações de uso.</span><span class="sxs-lookup"><span data-stu-id="ef943-235">Display usage information.</span></span> |

<span data-ttu-id="ef943-236">A seção print_usage() do [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) fornece uma explicação detalhada dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ef943-236">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="ef943-237">Após a ação de script ser implantada com êxito, você pode usar SSH para se conectar ao cluster HBase de destino e verificar se os dados foram replicados.</span><span class="sxs-lookup"><span data-stu-id="ef943-237">After the script action is successfully deployed, you can use SSH to connect to the destination HBase cluster, and verify the data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="ef943-238">Cenários de replicação</span><span class="sxs-lookup"><span data-stu-id="ef943-238">Replication scenarios</span></span>

<span data-ttu-id="ef943-239">A lista a seguir mostra alguns casos de uso geral e suas configurações de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="ef943-239">The following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="ef943-240">**Habilitar a replicação em todas as tabelas entre os dois clusters**.</span><span class="sxs-lookup"><span data-stu-id="ef943-240">**Enable replication on all tables between the two clusters**.</span></span> <span data-ttu-id="ef943-241">Esse cenário não requer a cópia/migração dos dados existentes nas tabelas, e não usa tabelas Phoenix.</span><span class="sxs-lookup"><span data-stu-id="ef943-241">This scenario does not require the copy/migration of existing data on the tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="ef943-242">Use os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="ef943-242">Use the following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="ef943-243">**Habilitar a replicação em tabelas específicas**.</span><span class="sxs-lookup"><span data-stu-id="ef943-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="ef943-244">Use os parâmetros a seguir para habilitar a replicação em table1, table2 e table3:</span><span class="sxs-lookup"><span data-stu-id="ef943-244">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="ef943-245">**Habilitar a replicação em tabelas específicas e copiar os dados existentes**.</span><span class="sxs-lookup"><span data-stu-id="ef943-245">**Enable replication on specific tables and copy the existing data**.</span></span> <span data-ttu-id="ef943-246">Use os parâmetros a seguir para habilitar a replicação em table1, table2 e table3:</span><span class="sxs-lookup"><span data-stu-id="ef943-246">Use the following parameters to enable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="ef943-247">**Habilitar a replicação em todas as tabelas com metadados phoenix replicados da origem para o destino**.</span><span class="sxs-lookup"><span data-stu-id="ef943-247">**Enable replication on all tables with replicating phoenix metadata from source to destination**.</span></span> <span data-ttu-id="ef943-248">A replicação de metadados Phoenix não é ideal e deve ser habilitada com cuidado.</span><span class="sxs-lookup"><span data-stu-id="ef943-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="ef943-249">Copiar e migrar dados</span><span class="sxs-lookup"><span data-stu-id="ef943-249">Copy and migrate data</span></span>

<span data-ttu-id="ef943-250">Há dois scripts de ação de script separados para copiar/migrar dados após a replicação ser habilitada:</span><span class="sxs-lookup"><span data-stu-id="ef943-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="ef943-251">[Script para tabelas pequenas](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (apenas alguns gigabytes de tamanho e deve levar menos que uma hora para copiar)</span><span class="sxs-lookup"><span data-stu-id="ef943-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected to finish in less than one hour)</span></span>

- <span data-ttu-id="ef943-252">[Script para tabelas grandes](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (devem levar mais de uma hora para copiar)</span><span class="sxs-lookup"><span data-stu-id="ef943-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected to take longer than one hour to copy)</span></span>

<span data-ttu-id="ef943-253">Você pode seguir o mesmo procedimento em [Habilitar replicação](#enable-replication) para chamar a ação de script com os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="ef943-253">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="ef943-254">A seção print_usage() do [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) fornece uma descrição detalhada dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ef943-254">The print_usage() section of the [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="ef943-255">Cenários</span><span class="sxs-lookup"><span data-stu-id="ef943-255">Scenarios</span></span>

- <span data-ttu-id="ef943-256">**Copiar tabelas específicas (test1, test2 e test3) para todas as linhas editadas até o momento (carimbo de hora atual)**:</span><span class="sxs-lookup"><span data-stu-id="ef943-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="ef943-257">ou o</span><span class="sxs-lookup"><span data-stu-id="ef943-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="ef943-258">**Copiar tabelas específicas com intervalo de tempo especificado**:</span><span class="sxs-lookup"><span data-stu-id="ef943-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="ef943-259">Desabilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="ef943-259">Disable replication</span></span>

<span data-ttu-id="ef943-260">Para desabilitar a replicação, use outro script de ação de script localizado no [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="ef943-260">To disable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="ef943-261">Você pode seguir o mesmo procedimento em [Habilitar replicação](#enable-replication) para chamar a ação de script com os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="ef943-261">You can follow the same procedure in [Enable replication](#enable-replication) to call the script action with the following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="ef943-262">A seção print_usage() do [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) fornece uma explicação detalhada dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ef943-262">The print_usage() section of the [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="ef943-263">Cenários</span><span class="sxs-lookup"><span data-stu-id="ef943-263">Scenarios</span></span>

- <span data-ttu-id="ef943-264">**Desabilitar a replicação em todas as tabelas**:</span><span class="sxs-lookup"><span data-stu-id="ef943-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="ef943-265">ou o</span><span class="sxs-lookup"><span data-stu-id="ef943-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="ef943-266">**Desabilitar a replicação em tabelas específicas (table1, table2 e table3)**:</span><span class="sxs-lookup"><span data-stu-id="ef943-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="ef943-267">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef943-267">Next steps</span></span>

<span data-ttu-id="ef943-268">Neste tutorial, você aprendeu a configurar a replicação do HBase entre dois data centers.</span><span class="sxs-lookup"><span data-stu-id="ef943-268">In this tutorial, you learned how to configure HBase replication across two datacenters.</span></span> <span data-ttu-id="ef943-269">Para saber mais sobre HDInsight e HBase, consulte:</span><span class="sxs-lookup"><span data-stu-id="ef943-269">To learn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="ef943-270">[Introdução ao Apache HBase no HDInsight][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="ef943-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="ef943-271">[Visão geral do HDInsight HBase][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="ef943-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="ef943-272">[Criar clusters HBase na rede virtual do Azure][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="ef943-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="ef943-273">[Analisar o sentimento do Twitter em tempo real com o HBase][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="ef943-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="ef943-274">[Analisar dados de sensor com o Storm e o HBase no HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="ef943-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

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
