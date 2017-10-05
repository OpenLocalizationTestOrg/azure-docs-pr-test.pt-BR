---
title: "Criar clusters HBase em uma Rede Virtual – Azure | Microsoft Docs"
description: "Introdução ao uso do HBase no Azure HDInsight. Saiba como criar clusters HBase do HDInsight na rede virtual do Azure."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 668bd494ce3274188af56cf7d6253cec7af9abbc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="c2bf8-104">Criar clusters HBase no HDInsight na Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="c2bf8-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="c2bf8-105">Saiba como criar clusters HBase do Azure HDInsight em uma [Rede Virtual do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="c2bf8-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="c2bf8-106">Com a integração da rede virtual, os clusters do HBase podem ser implantados na mesma rede virtual que seus aplicativos, de modo que os aplicativos possam se comunicar diretamente com o HBase.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="c2bf8-107">Os benefícios incluem:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-107">The benefits include:</span></span>

* <span data-ttu-id="c2bf8-108">Conectividade direta do aplicativo Web com os nós do cluster do HBase, que permite a comunicação usando APIs RPC (chamada de procedimento remoto) Java do HBase.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="c2bf8-109">Desempenho aprimorado, evitando que o tráfego percorra diversos gateways e balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="c2bf8-110">Capacidade de processar informações confidenciais de maneira mais segura, sem expor um ponto de extremidade público.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c2bf8-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c2bf8-111">Prerequisites</span></span>
<span data-ttu-id="c2bf8-112">Antes de começar este tutorial, você deve ter os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-112">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="c2bf8-113">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-113">**An Azure subscription**.</span></span> <span data-ttu-id="c2bf8-114">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c2bf8-115">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="c2bf8-116">Consulte [Instalar e usar o PowerShell do Azure](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="c2bf8-117">Criar clusters do HBase na rede virtual</span><span class="sxs-lookup"><span data-stu-id="c2bf8-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="c2bf8-118">Nesta seção, você cria um cluster HBase baseado em Linux com a conta de armazenamento do Azure dependente em uma rede virtual do Azure usando um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="c2bf8-119">Para outros métodos de criação de cluster e noções básicas sobre as configurações, confira [Criar clusters do HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="c2bf8-120">Para obter mais informações sobre como usar um modelo para criar clusters Hadoop no HDInsight, confira [Criar clusters Hadoop no HDInsight usando modelos do Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="c2bf8-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="c2bf8-121">Algumas propriedades foram embutidas em código no modelo.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-121">Some properties are hard-coded into the template.</span></span> <span data-ttu-id="c2bf8-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-122">For example:</span></span>
>
> * <span data-ttu-id="c2bf8-123">**Local**: Leste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="c2bf8-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="c2bf8-124">**Versão do cluster**: 3.5</span><span class="sxs-lookup"><span data-stu-id="c2bf8-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="c2bf8-125">**Contagem de nós de trabalho do cluster:** 2</span><span class="sxs-lookup"><span data-stu-id="c2bf8-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="c2bf8-126">**Conta de armazenamento padrão**: uma cadeia de caracteres exclusiva</span><span class="sxs-lookup"><span data-stu-id="c2bf8-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="c2bf8-127">**Nome da rede virtual**:&lt; Nome do cluster > -vnet</span><span class="sxs-lookup"><span data-stu-id="c2bf8-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="c2bf8-128">**Espaço de endereço da rede virtual**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c2bf8-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="c2bf8-129">**Nome da sub-rede**: subnet1</span><span class="sxs-lookup"><span data-stu-id="c2bf8-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="c2bf8-130">**Intervalo de endereços da sub-rede**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="c2bf8-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="c2bf8-131">&lt;Nome do cluster > é substituído pelo nome do cluster que você fornecer ao usar o modelo.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span></span>
>
>

1. <span data-ttu-id="c2bf8-132">Clique na imagem a seguir para abrir o modelo no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-132">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="c2bf8-133">O modelo pode está localizado em [Modelos de Início Rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="c2bf8-134">Na folha **Implantação personalizada**, insira as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-134">From the **Custom deployment** blade, enter the following properties:</span></span>

   * <span data-ttu-id="c2bf8-135">**Assinatura**: selecione uma assinatura do Azure usada para criar o cluster HDInsight, a conta de armazenamento dependente e rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span></span>
   * <span data-ttu-id="c2bf8-136">**Grupo de recursos**: selecione **Criar novo** e especifique um novo nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="c2bf8-137">**Local**: selecione um local para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-137">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="c2bf8-138">**ClusterName**: insira um nome para o cluster Hadoop a ser criado.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span></span>
   * <span data-ttu-id="c2bf8-139">**Nome e senha de logon do cluster**: o nome de logon padrão é **admin**.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-139">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="c2bf8-140">**Nome de usuário e senha SSH**: o nome de usuário padrão é **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-140">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="c2bf8-141">Você pode renomeá-lo.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-141">You can rename it.</span></span>
   * <span data-ttu-id="c2bf8-142">**Concordo com os termos e condições declarados acima**: (selecionar)</span><span class="sxs-lookup"><span data-stu-id="c2bf8-142">**I agree to the terms and the conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="c2bf8-143">Clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-143">Click **Purchase**.</span></span> <span data-ttu-id="c2bf8-144">A criação de um cluster demora cerca de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-144">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="c2bf8-145">Após a criação do cluster, você pode clicar na folha do cluster no portal para abri-la.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="c2bf8-146">Depois de concluir o tutorial, talvez você queira excluir o cluster.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-146">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="c2bf8-147">Com o HDInsight, seus dados são armazenados no Armazenamento do Azure, assim você poderá excluir, com segurança, um cluster quando ele não estiver em uso.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="c2bf8-148">Você também é cobrado por um cluster HDInsight, mesmo quando ele não está em uso.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="c2bf8-149">Como os encargos para o cluster são muitas vezes maiores do que os encargos para armazenamento, faz sentido, do ponto de vista econômico, excluir os clusters quando não estiverem em uso.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="c2bf8-150">Para obter instruções sobre como excluir um cluster, confira [Gerenciar clusters Hadoop no HDInsight usando o Portal do Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="c2bf8-151">Para começar a trabalhar com o novo cluster do HBase, você pode usar os procedimentos encontrados em [Introdução ao uso do HBase com Hadoop no HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-to-the-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="c2bf8-152">Conectar-se ao cluster HBase usando as APIs de RPC HBase Java</span><span class="sxs-lookup"><span data-stu-id="c2bf8-152">Connect to the HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="c2bf8-153">Crie uma máquina virtual IaaS (infraestrutura como serviço) na mesma rede virtual do Azure e na mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span></span> <span data-ttu-id="c2bf8-154">Para obter instruções sobre como criar uma máquina virtual IaaS, confira [Criar uma máquina virtual executando o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="c2bf8-155">Ao seguir as etapas neste documento, você deve usar os seguintes valores para a configuração de Rede:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-155">When following the steps in this document, you must use the following values for the Network configuration:</span></span>

   * <span data-ttu-id="c2bf8-156">**Rede virtual**:&lt; Nome do cluster > -vnet</span><span class="sxs-lookup"><span data-stu-id="c2bf8-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="c2bf8-157">**Sub-rede**: subnet1</span><span class="sxs-lookup"><span data-stu-id="c2bf8-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c2bf8-158">Substitua &lt;Nome do cluster > pelo nome que você usou ao criar o cluster HDInsight nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="c2bf8-159">Ao usar esses valores, a máquina virtual é colocada na mesma rede virtual e na mesma sub-rede que o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span></span> <span data-ttu-id="c2bf8-160">Essa configuração permite que eles se comuniquem diretamente uns com os outros.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-160">This configuration allows them to directly communicate with each other.</span></span> <span data-ttu-id="c2bf8-161">Há uma maneira de criar um cluster HDInsight com um nó de borda vazio.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-161">There is a way to create an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="c2bf8-162">O nó de borda pode ser usado para gerenciar o cluster.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-162">The edge node can be used to manage the cluster.</span></span>  <span data-ttu-id="c2bf8-163">Para saber mais, confira [Usar nós de borda vazia no HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="c2bf8-164">Ao usar um aplicativo Java para se conectar ao HBase remotamente, você deve usar o nome de domínio totalmente qualificado (FQDN).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="c2bf8-165">Para determiná-lo, é preciso obter o sufixo DNS específico da conexão do cluster do HBase.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span></span> <span data-ttu-id="c2bf8-166">Para fazer isso, é possível usar um dos métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-166">To do that, you can use one of the following methods:</span></span>

   * <span data-ttu-id="c2bf8-167">Use um navegador da Web para fazer uma chamada ao Ambari:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-167">Use a Web browser to make an Ambari call:</span></span>

     <span data-ttu-id="c2bf8-168">Navegue até https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="c2bf8-169">Ele encontra um arquivo JSON com os sufixos DNS.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-169">It turns a JSON file with the DNS suffixes.</span></span>
   * <span data-ttu-id="c2bf8-170">Use o site do Ambari:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-170">Use the Ambari website:</span></span>

     1. <span data-ttu-id="c2bf8-171">Navegue até https://&lt;ClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="c2bf8-172">Clique em **Hosts** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-172">Click **Hosts** from the top menu.</span></span>
   * <span data-ttu-id="c2bf8-173">Use o Curl para fazer chamadas REST:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-173">Use Curl to make REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="c2bf8-174">Nos dados JSON (JavaScript Object Notation) retornados, localize a entrada "host_name".</span><span class="sxs-lookup"><span data-stu-id="c2bf8-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span></span> <span data-ttu-id="c2bf8-175">Contém o FQDN para os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-175">It contains the FQDN for the nodes in the cluster.</span></span> <span data-ttu-id="c2bf8-176">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="c2bf8-177">A parte do nome do domínio que começa com o nome do cluster é o sufixo DNS.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span></span> <span data-ttu-id="c2bf8-178">Por exemplo, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="c2bf8-179">Usar PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="c2bf8-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="c2bf8-180">Use o seguinte script do Azure PowerShell para registrar a função **Get-ClusterDetail** , que pode ser usada para retornar o sufixo DNS:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information to facilitate an HDInsight cluster-to-cluster scenario within the same virtual network.
            .Description
            This command shows the following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run the HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows the FQDN suffix of hosts in the cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows the value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows the value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run the HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows the FQDN suffix of hosts in the cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="c2bf8-181">Após executar o script do PowerShell do Azure, use o seguinte comando para retornar o sufixo DNS usando a função **Get-ClusterDetail** .</span><span class="sxs-lookup"><span data-stu-id="c2bf8-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span></span> <span data-ttu-id="c2bf8-182">Especifique o nome do cluster do HBase do HDInsight, o nome e a senha do administrador ao usar esse comando.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="c2bf8-183">Esse comando retorna o sufixo DNS.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-183">This command returns the DNS suffix.</span></span> <span data-ttu-id="c2bf8-184">Por exemplo, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change the primary DNS suffix configuration of the virtual machine. This enables the virtual machine to automatically resolve the host name of the HBase cluster without explicit specification of the suffix. For example, the *workernode0* host name will be correctly resolved to workernode0 of the HBase cluster.

    To make the configuration change:

    1. RDP into the virtual machine.
    2. Open **Local Group Policy Editor**. The executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** to the value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot the virtual machine.
-->

<span data-ttu-id="c2bf8-185">Para verificar se a máquina virtual pode se comunicar com o cluster do HBase, use o seguinte comando `ping headnode0.<dns suffix>` por meio da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-185">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span></span> <span data-ttu-id="c2bf8-186">Por exemplo, envie ping a headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="c2bf8-187">Para usar essa informação em um aplicativo Java, você pode seguir as etapas em [Utilizar o Maven para criar aplicativos Java que usam o HBase com o HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) para criar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-187">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span></span> <span data-ttu-id="c2bf8-188">Para que o aplicativo se conecte a um servidor HBase remoto, modifique o arquivo **hbase-site.xml** nesse exemplo para usar o FQDN para ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-188">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span></span> <span data-ttu-id="c2bf8-189">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="c2bf8-190">Para obter mais informações sobre a resolução de nome em redes virtuais do Azure, incluindo como usar seu próprio servidor DNS, consulte [Resolução do Nome (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="c2bf8-190">For more information about name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="c2bf8-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2bf8-191">Next steps</span></span>
<span data-ttu-id="c2bf8-192">Neste tutorial, você aprendeu a criar um cluster do HBase.</span><span class="sxs-lookup"><span data-stu-id="c2bf8-192">In this tutorial, you learned how to create an HBase cluster.</span></span> <span data-ttu-id="c2bf8-193">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="c2bf8-193">To learn more, see:</span></span>

* [<span data-ttu-id="c2bf8-194">Introdução ao HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2bf8-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="c2bf8-195">Usar nós de borda vazios no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2bf8-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="c2bf8-196">Configurar a replicação do HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2bf8-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="c2bf8-197">Criar clusters Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2bf8-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="c2bf8-198">Introdução ao uso do HBase com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2bf8-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="c2bf8-199">Analisar dados de sentimento no Twitter com o HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="c2bf8-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="c2bf8-200">[Visão geral da Rede Virtual][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="c2bf8-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Detalhes de provisionamento do novo cluster HBase"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Usar a Ação de Script para personalizar um cluster HBase"

[azure-preview-portal]: https://portal.azure.com
