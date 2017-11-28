---
title: clusters de aaaManage Hadoop no HDInsight com o PowerShell - Azure | Microsoft Docs
description: "Saiba como tarefas tooperform administrativa para Olá clusters Hadoop em HDInsight usando o PowerShell do Azure."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="bc182-103">Gerenciar clusters Hadoop no HDInsight Usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="bc182-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="bc182-104">PowerShell do Azure é um ambiente de script poderoso que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de suas cargas de trabalho no Azure.</span><span class="sxs-lookup"><span data-stu-id="bc182-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="bc182-105">Neste artigo, você aprenderá como usam o toomanage a clusters de Hadoop em HDInsight do Azure usando um console local do PowerShell do Azure por meio de saudação do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc182-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="bc182-106">Para lista de saudação do hello cmdlets do HDInsight PowerShell, consulte [referência de cmdlet do HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="bc182-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="bc182-107">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="bc182-107">**Prerequisites**</span></span>

<span data-ttu-id="bc182-108">Antes de começar este artigo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="bc182-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="bc182-109">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bc182-109">**An Azure subscription**.</span></span> <span data-ttu-id="bc182-110">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="bc182-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="bc182-111">Instale o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc182-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="bc182-112">Se você instalou o Azure PowerShell versão 0.9x, deve desinstalá-lo antes de instalar uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="bc182-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="bc182-113">toocheck versão Olá Olá instalada do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bc182-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="bc182-114">toouninstall Olá versão mais antiga, executar programas e recursos no painel de controle de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc182-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="bc182-115">Criar clusters</span><span class="sxs-lookup"><span data-stu-id="bc182-115">Create clusters</span></span>
<span data-ttu-id="bc182-116">Confira [Criar clusters baseados em Linux no HDInsight usando o Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="bc182-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="bc182-117">Listar clusters</span><span class="sxs-lookup"><span data-stu-id="bc182-117">List clusters</span></span>
<span data-ttu-id="bc182-118">Olá toolist de comando a seguir ao use todos os clusters na assinatura atual hello:</span><span class="sxs-lookup"><span data-stu-id="bc182-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="bc182-119">Mostrar cluster</span><span class="sxs-lookup"><span data-stu-id="bc182-119">Show cluster</span></span>
<span data-ttu-id="bc182-120">Use Olá comando tooshow detalhes de um cluster específico na assinatura atual Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc182-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="bc182-121">Excluir clusters</span><span class="sxs-lookup"><span data-stu-id="bc182-121">Delete clusters</span></span>
<span data-ttu-id="bc182-122">Use Olá comando toodelete um cluster a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc182-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="bc182-123">Você também pode excluir um cluster, removendo o grupo de recursos de saudação que contém o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc182-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="bc182-124">Observe que isso excluirá todos os recursos de saudação no grupo de hello, incluindo a conta de armazenamento padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc182-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="bc182-125">Dimensionar clusters</span><span class="sxs-lookup"><span data-stu-id="bc182-125">Scale clusters</span></span>
<span data-ttu-id="bc182-126">dimensionando o recurso de cluster de saudação permite toochange número de saudação de nós de trabalho usado por um cluster que está em execução no Azure HDInsight sem ter que toore-criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc182-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="bc182-127">Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="bc182-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="bc182-128">Se você não tiver certeza da versão de saudação do cluster, você pode verificar a página de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc182-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="bc182-129">Confira [Listar e mostrar clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="bc182-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="bc182-130">impacto de saudação do alterando o número de saudação de nós de dados para cada tipo de cluster HDInsight com suporte:</span><span class="sxs-lookup"><span data-stu-id="bc182-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="bc182-131">O Hadoop</span><span class="sxs-lookup"><span data-stu-id="bc182-131">Hadoop</span></span>

    <span data-ttu-id="bc182-132">Você perfeitamente pode aumentar o número de saudação de nós de trabalho em um cluster de Hadoop que está sendo executado sem afetar todos os trabalhos pendentes ou em execução.</span><span class="sxs-lookup"><span data-stu-id="bc182-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="bc182-133">Novos trabalhos também podem ser enviados enquanto Olá operação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="bc182-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="bc182-134">Falhas em uma operação de dimensionamento são controladas normalmente para que hello cluster seja sempre deixado em um estado funcional.</span><span class="sxs-lookup"><span data-stu-id="bc182-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="bc182-135">Quando um cluster Hadoop é reduzido, reduzindo o número de saudação de nós de dados, alguns dos serviços de saudação em cluster Olá são reiniciados.</span><span class="sxs-lookup"><span data-stu-id="bc182-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="bc182-136">Isso faz com que todas as e pendentes toofail trabalhos na conclusão de saudação do hello a operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="bc182-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="bc182-137">No entanto, você pode, reenviar trabalhos Olá após a conclusão da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc182-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="bc182-138">HBase</span><span class="sxs-lookup"><span data-stu-id="bc182-138">HBase</span></span>

    <span data-ttu-id="bc182-139">Sem problemas, você pode adicionar ou remover o cluster de HBase tooyour nós enquanto ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="bc182-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="bc182-140">Servidores regionais são balanceados automaticamente dentro de alguns minutos após o término da operação de dimensionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc182-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="bc182-141">No entanto, você pode equilibrar manualmente servidores regionais Olá fazendo logon em toohello um nó principal do cluster e em execução hello comandos a seguir em uma janela de prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="bc182-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="bc182-142">Storm</span><span class="sxs-lookup"><span data-stu-id="bc182-142">Storm</span></span>

    <span data-ttu-id="bc182-143">Sem problemas, você pode adicionar ou remover o cluster de profusão de tooyour de nós de dados enquanto ele está em execução.</span><span class="sxs-lookup"><span data-stu-id="bc182-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="bc182-144">Mas, após a conclusão bem-sucedida da operação de dimensionamento de saudação, você precisará de topologia de saudação toorebalance.</span><span class="sxs-lookup"><span data-stu-id="bc182-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="bc182-145">A redistribuição pode ser feita de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="bc182-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="bc182-146">Interface da Web Storm</span><span class="sxs-lookup"><span data-stu-id="bc182-146">Storm web UI</span></span>
  * <span data-ttu-id="bc182-147">Ferramenta CLI (interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="bc182-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="bc182-148">Consulte toohello [documentação do Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="bc182-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="bc182-149">Interface da web Hello Storm está disponível no cluster do HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="bc182-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![HDInsight storm dimensionar novo balanceamento](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="bc182-151">Aqui está um exemplo como toouse Olá CLI comando topologia de profusão de saudação toorebalance:</span><span class="sxs-lookup"><span data-stu-id="bc182-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="bc182-152">Olá toochange tamanho do cluster Hadoop usando o Azure PowerShell, execute Olá a seguir de comando de um computador cliente:</span><span class="sxs-lookup"><span data-stu-id="bc182-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="bc182-153">Conceder/revogar acesso</span><span class="sxs-lookup"><span data-stu-id="bc182-153">Grant/revoke access</span></span>
<span data-ttu-id="bc182-154">Clusters HDInsight tem Olá serviços da web HTTP (todos esses serviços têm pontos de extremidade RESTful) a seguir:</span><span class="sxs-lookup"><span data-stu-id="bc182-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="bc182-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="bc182-155">ODBC</span></span>
* <span data-ttu-id="bc182-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="bc182-156">JDBC</span></span>
* <span data-ttu-id="bc182-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="bc182-157">Ambari</span></span>
* <span data-ttu-id="bc182-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="bc182-158">Oozie</span></span>
* <span data-ttu-id="bc182-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="bc182-159">Templeton</span></span>

<span data-ttu-id="bc182-160">Por padrão, esses serviços são concedidos para acesso.</span><span class="sxs-lookup"><span data-stu-id="bc182-160">By default, these services are granted for access.</span></span> <span data-ttu-id="bc182-161">Você pode revogar/conceder acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc182-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="bc182-162">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="bc182-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="bc182-163">toogrant:</span><span class="sxs-lookup"><span data-stu-id="bc182-163">toogrant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="bc182-164">Revogando concedendo/acesso hello, redefinirá senha e nome de usuário de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="bc182-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="bc182-165">Isso também pode ser feito por meio do Portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc182-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="bc182-166">Consulte [HDInsight administrar usando Olá portal do Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="bc182-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="bc182-167">Atualizar credenciais de usuário HTTP</span><span class="sxs-lookup"><span data-stu-id="bc182-167">Update HTTP user credentials</span></span>
<span data-ttu-id="bc182-168">É Olá mesmo procedimento como [acesso Grant/revoke HTTP](#grant/revoke-access). Se foi concedida cluster Olá Olá acesso HTTP, você deve primeiro revogá-lo.</span><span class="sxs-lookup"><span data-stu-id="bc182-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="bc182-169">E, em seguida, conceder acesso de saudação com novas credenciais de usuário HTTP.</span><span class="sxs-lookup"><span data-stu-id="bc182-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="bc182-170">Localizar a conta de armazenamento saudação padrão</span><span class="sxs-lookup"><span data-stu-id="bc182-170">Find hello default storage account</span></span>
<span data-ttu-id="bc182-171">saudação de script do Powershell a seguir demonstra como tooget Olá nome de conta de armazenamento padrão e Olá chave de conta de armazenamento padrão para um cluster.</span><span class="sxs-lookup"><span data-stu-id="bc182-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="bc182-172">Localizar o grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="bc182-172">Find hello resource group</span></span>
<span data-ttu-id="bc182-173">No modo do Gerenciador de recursos de hello, cada cluster HDInsight pertence tooan grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc182-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="bc182-174">grupo de recursos de saudação toofind:</span><span class="sxs-lookup"><span data-stu-id="bc182-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="bc182-175">Enviar trabalhos</span><span class="sxs-lookup"><span data-stu-id="bc182-175">Submit jobs</span></span>
<span data-ttu-id="bc182-176">**trabalhos de MapReduce toosubmit**</span><span class="sxs-lookup"><span data-stu-id="bc182-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="bc182-177">Veja [Executar exemplos do MapReduce do Hadoop no HDInsight baseado em Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bc182-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="bc182-178">**trabalhos de Hive toosubmit**</span><span class="sxs-lookup"><span data-stu-id="bc182-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="bc182-179">Veja [Executar consultas do Hive usando o PowerShell](hdinsight-hadoop-use-hive-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="bc182-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="bc182-180">**trabalhos de Pig toosubmit**</span><span class="sxs-lookup"><span data-stu-id="bc182-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="bc182-181">[Consulte Executar trabalhos do Pig usando o PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bc182-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="bc182-182">**trabalhos de Sqoop toosubmit**</span><span class="sxs-lookup"><span data-stu-id="bc182-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="bc182-183">Consulte [Usar o Sqoop com o HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="bc182-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="bc182-184">**toosubmit Oozie trabalhos**</span><span class="sxs-lookup"><span data-stu-id="bc182-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="bc182-185">Consulte [Oozie de uso com toodefine Hadoop e executar um fluxo de trabalho no HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="bc182-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="bc182-186">Carregue o armazenamento de Blob de tooAzure de dados</span><span class="sxs-lookup"><span data-stu-id="bc182-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="bc182-187">Consulte [carregar dados tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="bc182-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="bc182-188">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bc182-188">See Also</span></span>
* <span data-ttu-id="bc182-189">[Documentação de referência do cmdlet do HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="bc182-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="bc182-190">[Administrar HDInsight usando Olá portal do Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="bc182-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="bc182-191">[Administrar o HDInsight usando uma interface de linha de comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="bc182-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="bc182-192">[Criar clusters HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="bc182-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="bc182-193">[Carregar dados tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="bc182-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="bc182-194">[Enviar trabalhos Hadoop de forma programática][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="bc182-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="bc182-195">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="bc182-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
