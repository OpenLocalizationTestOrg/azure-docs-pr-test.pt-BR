---
title: aaaCreate HBase clusters em uma rede Virtual - Azure | Microsoft Docs
description: "Introdução ao uso do HBase no Azure HDInsight. Saiba como toocreate HDInsight HBase clusters na rede Virtual do Azure."
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
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="8f178-104">Criar clusters HBase no HDInsight na Rede Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="8f178-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="8f178-105">Saiba como clusters de toocreate do Azure HDInsight HBase um [rede Virtual do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="8f178-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="8f178-106">Com a integração de rede virtual, clusters HBase podem ser implantado toohello mesmo virtual de rede como seus aplicativos para que aplicativos podem se comunicar com HBase diretamente.</span><span class="sxs-lookup"><span data-stu-id="8f178-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="8f178-107">Olá benefícios incluem:</span><span class="sxs-lookup"><span data-stu-id="8f178-107">hello benefits include:</span></span>

* <span data-ttu-id="8f178-108">Conectividade direta Olá web toohello de nós de aplicativos de cluster HBase hello, o que permite a comunicação por meio do procedimento remoto HBase Java chamar APIs de (RPC).</span><span class="sxs-lookup"><span data-stu-id="8f178-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="8f178-109">Desempenho aprimorado, evitando que o tráfego percorra diversos gateways e balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="8f178-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="8f178-110">Olá capacidade tooprocess informações confidenciais de forma mais segura sem expor um ponto de extremidade público.</span><span class="sxs-lookup"><span data-stu-id="8f178-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8f178-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f178-111">Prerequisites</span></span>
<span data-ttu-id="8f178-112">Antes de começar este tutorial, você deve ter Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f178-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="8f178-113">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="8f178-113">**An Azure subscription**.</span></span> <span data-ttu-id="8f178-114">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8f178-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8f178-115">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="8f178-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="8f178-116">Consulte [Instalar e usar o PowerShell do Azure](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="8f178-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="8f178-117">Criar clusters do HBase na rede virtual</span><span class="sxs-lookup"><span data-stu-id="8f178-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="8f178-118">Nesta seção, você criará um cluster HBase baseados em Linux com conta de armazenamento do Azure dependente Olá em uma rede virtual do Azure usando um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8f178-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="8f178-119">Para outros métodos de criação de cluster e Noções básicas sobre configurações de hello, consulte [HDInsight criar clusters](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="8f178-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="8f178-120">Para obter mais informações sobre como usar um modelo toocreate Hadoop clusters de HDInsight, consulte [Hadoop criar clusters de HDInsight usando modelos do Gerenciador de recursos do Azure](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="8f178-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="8f178-121">Algumas propriedades são embutidos em código no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f178-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="8f178-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8f178-122">For example:</span></span>
>
> * <span data-ttu-id="8f178-123">**Local**: Leste dos EUA 2</span><span class="sxs-lookup"><span data-stu-id="8f178-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="8f178-124">**Versão do cluster**: 3.5</span><span class="sxs-lookup"><span data-stu-id="8f178-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="8f178-125">**Contagem de nós de trabalho do cluster:** 2</span><span class="sxs-lookup"><span data-stu-id="8f178-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="8f178-126">**Conta de armazenamento padrão**: uma cadeia de caracteres exclusiva</span><span class="sxs-lookup"><span data-stu-id="8f178-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="8f178-127">**Nome da rede virtual**:&lt; Nome do cluster > -vnet</span><span class="sxs-lookup"><span data-stu-id="8f178-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="8f178-128">**Espaço de endereço da rede virtual**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="8f178-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="8f178-129">**Nome da sub-rede**: subnet1</span><span class="sxs-lookup"><span data-stu-id="8f178-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="8f178-130">**Intervalo de endereços da sub-rede**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="8f178-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="8f178-131">&lt;Nome do cluster > é substituído pelo nome do cluster Olá fornecem ao usar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f178-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="8f178-132">Clique em Olá seguindo o modelo de saudação tooopen imagem em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f178-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="8f178-133">Olá modelo está localizado em [modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="8f178-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="8f178-134">De saudação **implantação personalizada** folha, digite Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f178-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="8f178-135">**Assinatura**: selecione um cluster HDInsight do Azure assinatura usada toocreate hello, Olá dependente conta de armazenamento e Olá rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f178-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="8f178-136">**Grupo de recursos**: selecione **Criar novo** e especifique um novo nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8f178-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="8f178-137">**Local**: selecione um local para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f178-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="8f178-138">**ClusterName**: insira um nome para toobe de cluster de Hadoop Olá criado.</span><span class="sxs-lookup"><span data-stu-id="8f178-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="8f178-139">**Nome de logon e senha do cluster**: nome de logon padrão Olá é **admin**.</span><span class="sxs-lookup"><span data-stu-id="8f178-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="8f178-140">**SSH username e password**: nome de usuário saudação padrão é **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="8f178-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="8f178-141">Você pode renomeá-lo.</span><span class="sxs-lookup"><span data-stu-id="8f178-141">You can rename it.</span></span>
   * <span data-ttu-id="8f178-142">**Eu concordo toohello termos e condições de saudação declaradas acima**: (Selecionar)</span><span class="sxs-lookup"><span data-stu-id="8f178-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="8f178-143">Clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="8f178-143">Click **Purchase**.</span></span> <span data-ttu-id="8f178-144">Demora cerca de aproximadamente 20 minutos toocreate um cluster.</span><span class="sxs-lookup"><span data-stu-id="8f178-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="8f178-145">Depois de criar o cluster hello, você pode clicar em folha de cluster Olá em tooopen portal Olá-lo.</span><span class="sxs-lookup"><span data-stu-id="8f178-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="8f178-146">Depois de concluir o tutorial hello, talvez você queira toodelete cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f178-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="8f178-147">Com o HDInsight, seus dados são armazenados no Armazenamento do Azure, assim você poderá excluir, com segurança, um cluster quando ele não estiver em uso.</span><span class="sxs-lookup"><span data-stu-id="8f178-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="8f178-148">Você também é cobrado por um cluster HDInsight, mesmo quando ele não está em uso.</span><span class="sxs-lookup"><span data-stu-id="8f178-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="8f178-149">Como encargos Olá para cluster Olá são muitas vezes mais do que encargos Olá para armazenamento, faz sentido, financeiramente falando toodelete clusters quando eles não estiverem em uso.</span><span class="sxs-lookup"><span data-stu-id="8f178-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="8f178-150">Para obter instruções de saudação da exclusão de um cluster, consulte [clusters gerenciar Hadoop em HDInsight usando Olá portal do Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="8f178-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="8f178-151">toobegin trabalhando com seu novo cluster HBase, você pode usar os procedimentos de saudação encontrados no [iniciar o uso do HBase com Hadoop no HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f178-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="8f178-152">Conectar-se o cluster do HBase toohello usando APIs de RPC de Java do HBase</span><span class="sxs-lookup"><span data-stu-id="8f178-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="8f178-153">Criar uma infraestrutura como serviço (IaaS) máquina virtual em Olá mesma rede virtual do Azure e Olá mesma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8f178-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="8f178-154">Para obter instruções sobre como criar uma máquina virtual IaaS, confira [Criar uma máquina virtual executando o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8f178-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="8f178-155">Ao seguir as etapas de saudação neste documento, você deve usar Olá valores para a configuração de rede Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f178-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="8f178-156">**Rede virtual**:&lt; Nome do cluster > -vnet</span><span class="sxs-lookup"><span data-stu-id="8f178-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="8f178-157">**Sub-rede**: subnet1</span><span class="sxs-lookup"><span data-stu-id="8f178-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="8f178-158">Substituir &lt;nome do Cluster > com o nome da saudação usados ao criar o cluster do HDInsight Olá nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="8f178-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="8f178-159">Usando esses valores, Olá máquina virtual é colocada no hello mesma rede virtual e a sub-rede do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="8f178-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="8f178-160">Essa configuração permite que eles toodirectly se comunicar entre si.</span><span class="sxs-lookup"><span data-stu-id="8f178-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="8f178-161">Há uma maneira toocreate um cluster HDInsight com um nó de borda vazia.</span><span class="sxs-lookup"><span data-stu-id="8f178-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="8f178-162">nó de borda Olá pode ser o cluster de saudação do toomanage usado.</span><span class="sxs-lookup"><span data-stu-id="8f178-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="8f178-163">Para saber mais, confira [Usar nós de borda vazia no HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="8f178-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="8f178-164">Ao usar um tooHBase de tooconnect de aplicativo Java remotamente, você deve usar o nome de domínio totalmente qualificado da saudação (FQDN).</span><span class="sxs-lookup"><span data-stu-id="8f178-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="8f178-165">toodetermine isso, você deve obter o sufixo DNS específico da conexão saudação do cluster do HBase hello.</span><span class="sxs-lookup"><span data-stu-id="8f178-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="8f178-166">toodo que, você pode usar um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="8f178-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="8f178-167">Use um navegador de Web toomake uma chamada de Ambari:</span><span class="sxs-lookup"><span data-stu-id="8f178-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="8f178-168">Procurar toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / hospeda? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="8f178-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="8f178-169">Na verdade, um arquivo JSON com sufixos DNS hello.</span><span class="sxs-lookup"><span data-stu-id="8f178-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="8f178-170">Use Olá Ambari site:</span><span class="sxs-lookup"><span data-stu-id="8f178-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="8f178-171">Procurar muito https://&lt;ClusterName >. n e t.</span><span class="sxs-lookup"><span data-stu-id="8f178-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="8f178-172">Clique em **Hosts** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="8f178-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="8f178-173">Use chamadas REST ondulação toomake:</span><span class="sxs-lookup"><span data-stu-id="8f178-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="8f178-174">Em Olá dados JSON JavaScript Object Notation () retornado, localizar a entrada de "host_name" hello.</span><span class="sxs-lookup"><span data-stu-id="8f178-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="8f178-175">Ele contém Olá FQDN para nós de saudação em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8f178-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="8f178-176">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8f178-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="8f178-177">parte de saudação do hello domínio nome que começa com o nome do cluster Olá é sufixo DNS hello.</span><span class="sxs-lookup"><span data-stu-id="8f178-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="8f178-178">Por exemplo, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="8f178-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="8f178-179">Usar PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="8f178-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="8f178-180">Saudação de uso após a saudação de tooregister de script do PowerShell do Azure **ClusterDetail Get** função, que pode ser o sufixo DNS usado tooreturn hello:</span><span class="sxs-lookup"><span data-stu-id="8f178-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

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
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
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

     <span data-ttu-id="8f178-181">Depois de script do PowerShell do Azure Olá em execução, use Olá comando a seguir sufixo DNS Olá tooreturn usando Olá **ClusterDetail Get** função.</span><span class="sxs-lookup"><span data-stu-id="8f178-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="8f178-182">Especifique o nome do cluster do HBase do HDInsight, o nome e a senha do administrador ao usar esse comando.</span><span class="sxs-lookup"><span data-stu-id="8f178-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="8f178-183">Esse comando retorna o sufixo DNS hello.</span><span class="sxs-lookup"><span data-stu-id="8f178-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="8f178-184">Por exemplo, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="8f178-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="8f178-185">tooverify que Olá máquina virtual pode se comunicar com hello cluster HBase, use o comando Olá `ping headnode0.<dns suffix>` da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f178-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="8f178-186">Por exemplo, envie ping a headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="8f178-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="8f178-187">toouse essas informações em um aplicativo Java, você pode seguir etapas Olá [usar Maven toobuild os aplicativos Java que usa HBase com HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8f178-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="8f178-188">aplicativo de hello toohave conectar o servidor remoto de HBase tooa, modifique Olá **hbase-site.XML** Zookeeper no arquivo na saudação de toouse exemplo FQDN.</span><span class="sxs-lookup"><span data-stu-id="8f178-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="8f178-189">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8f178-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="8f178-190">Para obter mais informações sobre resolução de nomes em redes virtuais do Azure, incluindo como toouse seu próprio servidor DNS, consulte [resolução de nomes (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="8f178-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="8f178-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f178-191">Next steps</span></span>
<span data-ttu-id="8f178-192">Neste tutorial, você aprendeu como toocreate um cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="8f178-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="8f178-193">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="8f178-193">toolearn more, see:</span></span>

* [<span data-ttu-id="8f178-194">Introdução ao HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f178-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="8f178-195">Usar nós de borda vazios no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f178-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="8f178-196">Configurar a replicação do HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f178-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="8f178-197">Criar clusters Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f178-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="8f178-198">Introdução ao uso do HBase com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f178-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="8f178-199">Analisar dados de sentimento no Twitter com o HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f178-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="8f178-200">[Visão geral da Rede Virtual][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="8f178-200">[Virtual Network Overview][vnet-overview]</span></span>

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
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Detalhes de provisionar novo cluster de HBase Olá"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Use a ação de Script toocustomize um cluster HBase"

[azure-preview-portal]: https://portal.azure.com
