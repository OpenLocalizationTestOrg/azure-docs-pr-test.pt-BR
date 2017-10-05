---
title: "Gerenciar clusters de Hadoop no HDInsight com o PowerShell – Azure | Microsoft Docs"
description: Saiba como realizar tarefas administrativas para os clusters Hadoop no HDInsight usando o PowerShell do Azure.
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
ms.openlocfilehash: c47dabd7c4aa4ba0be08c419989e536711f03677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="b1a75-103">Gerenciar clusters Hadoop no HDInsight Usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="b1a75-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="b1a75-104">O PowerShell do Azure é um ambiente de script poderoso que você pode usar para controlar e automatizar a implantação e o gerenciamento de suas cargas de trabalho no Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a75-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="b1a75-105">Neste artigo, você aprenderá como gerenciar clusters HDInsight do Azure usando um console local do PowerShell do Azure com Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1a75-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span></span> <span data-ttu-id="b1a75-106">Para obter a lista de cmdlets do HDInsight PowerShell, consulte [Referência ao cmdlets do HDInsight][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="b1a75-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="b1a75-107">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="b1a75-107">**Prerequisites**</span></span>

<span data-ttu-id="b1a75-108">Antes de começar este artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b1a75-108">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="b1a75-109">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b1a75-109">**An Azure subscription**.</span></span> <span data-ttu-id="b1a75-110">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b1a75-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="b1a75-111">Instale o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1a75-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="b1a75-112">Se você instalou o Azure PowerShell versão 0.9x, deve desinstalá-lo antes de instalar uma versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="b1a75-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="b1a75-113">Para verificar a versão do PowerShell instalado:</span><span class="sxs-lookup"><span data-stu-id="b1a75-113">To check the version of the installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="b1a75-114">Para desinstalar a versão mais antiga, execute Programas e Recursos no painel de controle.</span><span class="sxs-lookup"><span data-stu-id="b1a75-114">To uninstall the older version, run Programs and Features in the control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="b1a75-115">Criar clusters</span><span class="sxs-lookup"><span data-stu-id="b1a75-115">Create clusters</span></span>
<span data-ttu-id="b1a75-116">Confira [Criar clusters baseados em Linux no HDInsight usando o Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="b1a75-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="b1a75-117">Listar clusters</span><span class="sxs-lookup"><span data-stu-id="b1a75-117">List clusters</span></span>
<span data-ttu-id="b1a75-118">Use o seguinte comando para listar todos os clusters na assinatura atual:</span><span class="sxs-lookup"><span data-stu-id="b1a75-118">Use the following command to list all clusters in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="b1a75-119">Mostrar cluster</span><span class="sxs-lookup"><span data-stu-id="b1a75-119">Show cluster</span></span>
<span data-ttu-id="b1a75-120">Use o seguinte comando para mostrar os detalhes de um cluster específico na assinatura atual:</span><span class="sxs-lookup"><span data-stu-id="b1a75-120">Use the following command to show details of a specific cluster in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="b1a75-121">Excluir clusters</span><span class="sxs-lookup"><span data-stu-id="b1a75-121">Delete clusters</span></span>
<span data-ttu-id="b1a75-122">Use o seguinte comando para excluir um cluster:</span><span class="sxs-lookup"><span data-stu-id="b1a75-122">Use the following command to delete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="b1a75-123">Você também pode excluir um cluster removendo o grupo de recursos que contém o cluster.</span><span class="sxs-lookup"><span data-stu-id="b1a75-123">You can also delete a cluster by removing the resource group that contains the cluster.</span></span> <span data-ttu-id="b1a75-124">Observe que isso excluirá todos os recursos no grupo, incluindo a conta de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="b1a75-124">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="b1a75-125">Dimensionar clusters</span><span class="sxs-lookup"><span data-stu-id="b1a75-125">Scale clusters</span></span>
<span data-ttu-id="b1a75-126">O recurso de dimensionamento de clusters permite que você altere o número de nós de trabalhador usados por um cluster em execução no Azure HDInsight sem precisar recriar o cluster.</span><span class="sxs-lookup"><span data-stu-id="b1a75-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b1a75-127">Somente clusters HDInsight versão 3.1.3 ou superior são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="b1a75-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="b1a75-128">Se não tiver certeza quanto à versão de seu cluster, você poderá verificar a página Propriedades.</span><span class="sxs-lookup"><span data-stu-id="b1a75-128">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="b1a75-129">Confira [Listar e mostrar clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="b1a75-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="b1a75-130">O impacto da alteração do número de nós de dados em cada tipo de cluster com suporte do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b1a75-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="b1a75-131">O Hadoop</span><span class="sxs-lookup"><span data-stu-id="b1a75-131">Hadoop</span></span>

    <span data-ttu-id="b1a75-132">Você pode aumentar continuamente o número de nós de trabalhador em um cluster Hadoop em execução sem afetar os trabalhos pendentes ou em execução.</span><span class="sxs-lookup"><span data-stu-id="b1a75-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="b1a75-133">Novos trabalhos também podem ser enviados enquanto a operação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="b1a75-133">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="b1a75-134">Falhas em uma operação de dimensionamento são normalmente manipuladas para que o cluster sempre seja deixado em um estado funcional.</span><span class="sxs-lookup"><span data-stu-id="b1a75-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="b1a75-135">Quando um cluster Hadoop é reduzido verticalmente pela diminuição do número de nós de dados, alguns dos serviços no cluster são reiniciados.</span><span class="sxs-lookup"><span data-stu-id="b1a75-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="b1a75-136">Isso faz com que todos os trabalhos em execução e pendentes falhem após a conclusão da operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b1a75-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="b1a75-137">Você pode, no entanto, reenviar os trabalhos quando a operação for concluída.</span><span class="sxs-lookup"><span data-stu-id="b1a75-137">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="b1a75-138">HBase</span><span class="sxs-lookup"><span data-stu-id="b1a75-138">HBase</span></span>

    <span data-ttu-id="b1a75-139">Você pode adicionar ou remover diretamente nós do cluster HBase enquanto ele é executado.</span><span class="sxs-lookup"><span data-stu-id="b1a75-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="b1a75-140">Servidores Regionais são equilibrados automaticamente em alguns minutos após o término da operação de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b1a75-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="b1a75-141">No entanto, você pode equilibrar manualmente os servidores regionais fazendo logon no nó de cabeçalho do cluster e executando os seguintes comandos em uma janela de prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="b1a75-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="b1a75-142">Storm</span><span class="sxs-lookup"><span data-stu-id="b1a75-142">Storm</span></span>

    <span data-ttu-id="b1a75-143">Você pode adicionar ou remover nós de dados continuamente para seu cluster Strom enquanto ele é executado.</span><span class="sxs-lookup"><span data-stu-id="b1a75-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="b1a75-144">Mas, após a conclusão bem-sucedida da operação de dimensionamento, você precisará redistribuir a topologia.</span><span class="sxs-lookup"><span data-stu-id="b1a75-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="b1a75-145">A redistribuição pode ser feita de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="b1a75-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="b1a75-146">Interface da Web Storm</span><span class="sxs-lookup"><span data-stu-id="b1a75-146">Storm web UI</span></span>
  * <span data-ttu-id="b1a75-147">Ferramenta CLI (interface de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="b1a75-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="b1a75-148">Consulte a [documentação do Apache Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="b1a75-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="b1a75-149">A IU da Web do Storm está disponível no cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b1a75-149">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight storm dimensionar novo balanceamento](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="b1a75-151">Aqui está um exemplo de como usar o comando CLI para reequilibrar a topologia do Storm:</span><span class="sxs-lookup"><span data-stu-id="b1a75-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="b1a75-152">Para alterar o tamanho do cluster Hadoop usando o PowerShell do Azure, execute este comando no computador cliente:</span><span class="sxs-lookup"><span data-stu-id="b1a75-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="b1a75-153">Conceder/revogar acesso</span><span class="sxs-lookup"><span data-stu-id="b1a75-153">Grant/revoke access</span></span>
<span data-ttu-id="b1a75-154">Os clusters HDInsight têm os seguintes serviços Web HTTP (todos esses serviços têm pontos de extremidade RESTful):</span><span class="sxs-lookup"><span data-stu-id="b1a75-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="b1a75-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="b1a75-155">ODBC</span></span>
* <span data-ttu-id="b1a75-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="b1a75-156">JDBC</span></span>
* <span data-ttu-id="b1a75-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="b1a75-157">Ambari</span></span>
* <span data-ttu-id="b1a75-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="b1a75-158">Oozie</span></span>
* <span data-ttu-id="b1a75-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="b1a75-159">Templeton</span></span>

<span data-ttu-id="b1a75-160">Por padrão, esses serviços são concedidos para acesso.</span><span class="sxs-lookup"><span data-stu-id="b1a75-160">By default, these services are granted for access.</span></span> <span data-ttu-id="b1a75-161">Você pode revogar/conceder o acesso.</span><span class="sxs-lookup"><span data-stu-id="b1a75-161">You can revoke/grant the access.</span></span> <span data-ttu-id="b1a75-162">Para revogar:</span><span class="sxs-lookup"><span data-stu-id="b1a75-162">To revoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="b1a75-163">Para conceder:</span><span class="sxs-lookup"><span data-stu-id="b1a75-163">To grant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter the Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="b1a75-164">Ao conceder/revogar o acesso, você redefinirá o nome de usuário de cluster e a senha.</span><span class="sxs-lookup"><span data-stu-id="b1a75-164">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="b1a75-165">Isso também pode ser feito por meio do Portal.</span><span class="sxs-lookup"><span data-stu-id="b1a75-165">This can also be done via the Portal.</span></span> <span data-ttu-id="b1a75-166">Consulte [Administrar o HDInsight usando o Portal do Azure][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="b1a75-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="b1a75-167">Atualizar credenciais de usuário HTTP</span><span class="sxs-lookup"><span data-stu-id="b1a75-167">Update HTTP user credentials</span></span>
<span data-ttu-id="b1a75-168">É o mesmo procedimento para [acessar Conceder/Revogar HTTP](#grant/revoke-access). Se o cluster recebeu o acesso HTTP, você deverá revogá-lo.</span><span class="sxs-lookup"><span data-stu-id="b1a75-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="b1a75-169">E, em seguida, conceder acesso com novas credenciais de usuário HTTP.</span><span class="sxs-lookup"><span data-stu-id="b1a75-169">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="b1a75-170">Encontrar a conta de armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="b1a75-170">Find the default storage account</span></span>
<span data-ttu-id="b1a75-171">O script do Powershell a seguir demonstra como obter o nome da conta de armazenamento padrão e a chave da conta de armazenamento padrão de um cluster.</span><span class="sxs-lookup"><span data-stu-id="b1a75-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-the-resource-group"></a><span data-ttu-id="b1a75-172">Encontrar o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b1a75-172">Find the resource group</span></span>
<span data-ttu-id="b1a75-173">No modo do Gerenciador de Recursos, cada cluster HDInsight pertence a um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1a75-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span></span>  <span data-ttu-id="b1a75-174">Encontrar o grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="b1a75-174">To find the resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="b1a75-175">Enviar trabalhos</span><span class="sxs-lookup"><span data-stu-id="b1a75-175">Submit jobs</span></span>
<span data-ttu-id="b1a75-176">**Enviar trabalhos MapReduce**</span><span class="sxs-lookup"><span data-stu-id="b1a75-176">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="b1a75-177">Veja [Executar exemplos do MapReduce do Hadoop no HDInsight baseado em Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b1a75-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="b1a75-178">**Enviar trabalhos Hive**</span><span class="sxs-lookup"><span data-stu-id="b1a75-178">**To submit Hive jobs**</span></span>

<span data-ttu-id="b1a75-179">Veja [Executar consultas do Hive usando o PowerShell](hdinsight-hadoop-use-hive-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="b1a75-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="b1a75-180">**Enviar trabalhos Pig**</span><span class="sxs-lookup"><span data-stu-id="b1a75-180">**To submit Pig jobs**</span></span>

<span data-ttu-id="b1a75-181">[Consulte Executar trabalhos do Pig usando o PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b1a75-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="b1a75-182">**Para enviar trabalhos de Sqoop**</span><span class="sxs-lookup"><span data-stu-id="b1a75-182">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="b1a75-183">Consulte [Usar o Sqoop com o HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="b1a75-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="b1a75-184">**Para enviar trabalhos de Oozie**</span><span class="sxs-lookup"><span data-stu-id="b1a75-184">**To submit Oozie jobs**</span></span>

<span data-ttu-id="b1a75-185">Consulte [Usar o Oozie com Hadoop para definir e executar um fluxo de trabalho no HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="b1a75-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="b1a75-186">Carregar dados no armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="b1a75-186">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="b1a75-187">Veja [Carregar dados no HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="b1a75-187">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="b1a75-188">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b1a75-188">See Also</span></span>
* <span data-ttu-id="b1a75-189">[Documentação de referência do cmdlet do HDInsight][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="b1a75-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="b1a75-190">[Administrar o HDInsight usando o Portal do Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="b1a75-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="b1a75-191">[Administrar o HDInsight usando uma interface de linha de comando][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="b1a75-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="b1a75-192">[Criar clusters HDInsight][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="b1a75-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="b1a75-193">[Carregar dados no HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="b1a75-193">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="b1a75-194">[Enviar trabalhos Hadoop de forma programática][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="b1a75-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="b1a75-195">[Introdução ao Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b1a75-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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
