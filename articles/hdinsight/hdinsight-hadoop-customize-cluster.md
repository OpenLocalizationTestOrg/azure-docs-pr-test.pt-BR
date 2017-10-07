---
title: "aaaCustomize Clusters HDInsight usando script de ações - Azure | Microsoft Docs"
description: "Saiba como toocustomize HDInsight clusters usando a ação de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="52ce6-103">Personalizar clusters HDInsight baseados em Windows usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="52ce6-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="52ce6-104">**Ação de script** pode ser usado tooinvoke [scripts personalizados](hdinsight-hadoop-script-actions.md) durante processo de criação de cluster Olá para instalar software adicional em um cluster.</span><span class="sxs-lookup"><span data-stu-id="52ce6-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="52ce6-105">informações Olá neste artigo são específico com base em tooWindows clusters de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52ce6-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="52ce6-106">Para cluster baseados em Linux, confira [Personalizar clusters do HDInsight baseados em Linux usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="52ce6-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52ce6-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="52ce6-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="52ce6-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="52ce6-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="52ce6-109">Clusters HDInsight podem ser personalizados em uma variedade de outras maneiras, como incluir contas de armazenamento do Azure adicionais, alterar Olá Hadoop arquivos de configuração (Core-site.XML, hive-site.XML, etc.) ou adicionando compartilhado bibliotecas (por exemplo, Hive, Oozie) em locais comuns em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="52ce6-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="52ce6-110">Essas personalizações podem ser feitas por meio do PowerShell do Azure, hello Azure HDInsight .NET SDK, ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ce6-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="52ce6-111">Para obter mais informações, veja [Criar clusters Hadoop no HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="52ce6-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="52ce6-112">Ação de script no processo de criação de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="52ce6-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="52ce6-113">Ação de script é usada apenas enquanto um cluster está no processo de saudação do que está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="52ce6-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="52ce6-114">Olá seguinte diagrama ilustra quando a ação de Script é executada durante o processo de criação de saudação:</span><span class="sxs-lookup"><span data-stu-id="52ce6-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="52ce6-115">![Personalização do cluster HDInsight e estágios durante a criação de cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="52ce6-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="52ce6-116">Quando estiver executando o script hello, cluster Olá insere Olá **ClusterCustomization** estágio.</span><span class="sxs-lookup"><span data-stu-id="52ce6-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="52ce6-117">Neste estágio, script hello é executado na conta de administrador de sistema hello, paralelamente em todas as Olá especificado nós no cluster hello e fornece privilégios totais de administrador em nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ce6-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="52ce6-118">Porque você tem privilégios de administrador em nós de cluster Olá durante o **ClusterCustomization** estágio, você pode usar operações de tooperform script hello como parar e iniciar serviços, incluindo serviços relacionados ao Hadoop.</span><span class="sxs-lookup"><span data-stu-id="52ce6-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="52ce6-119">Portanto, como parte do script hello, você deve garantir que os serviços do Ambari hello e outros serviços relacionados ao Hadoop estão funcionando antes que o script hello terminar a execução.</span><span class="sxs-lookup"><span data-stu-id="52ce6-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="52ce6-120">Esses serviços são necessários toosuccessfully verificar integridade hello e estado do cluster Olá enquanto ele está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="52ce6-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="52ce6-121">Se você alterar qualquer configuração no cluster que afeta a esses serviços, você deve usar funções auxiliares Olá fornecidos.</span><span class="sxs-lookup"><span data-stu-id="52ce6-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="52ce6-122">Para obter mais informações sobre funções auxiliares, confira [Desenvolver scripts de Ação de Script para o HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="52ce6-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="52ce6-123">saída de Hello e logs de erros de saudação para script hello são armazenados na conta de armazenamento padrão de saudação especificado para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ce6-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="52ce6-124">Olá logs são armazenados em uma tabela com o nome da saudação **u < \cluster-name-fragment >< \time-stamp > setuplog**.</span><span class="sxs-lookup"><span data-stu-id="52ce6-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="52ce6-125">Esses são os logs de agregação de script hello executado em todos os nós de saudação (nó principal e nós de trabalho) no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="52ce6-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="52ce6-126">Cada cluster pode aceitar várias ações de script que são invocadas em ordem de saudação na qual elas são especificadas.</span><span class="sxs-lookup"><span data-stu-id="52ce6-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="52ce6-127">Um script pode ser executado no nó principal hello, nós de trabalho hello ou ambos.</span><span class="sxs-lookup"><span data-stu-id="52ce6-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="52ce6-128">HDInsight fornece Olá de tooinstall scripts vários componentes a seguir em clusters de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="52ce6-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="52ce6-129">Nome</span><span class="sxs-lookup"><span data-stu-id="52ce6-129">Name</span></span> | <span data-ttu-id="52ce6-130">Script</span><span class="sxs-lookup"><span data-stu-id="52ce6-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="52ce6-131">**Instalar Spark**</span><span class="sxs-lookup"><span data-stu-id="52ce6-131">**Install Spark**</span></span> |<span data-ttu-id="52ce6-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="52ce6-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="52ce6-133">Consulte [Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="52ce6-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="52ce6-134">**Instalar R**</span><span class="sxs-lookup"><span data-stu-id="52ce6-134">**Install R**</span></span> |<span data-ttu-id="52ce6-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="52ce6-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="52ce6-136">Consulte [Instalar e usar o R em clusters HDInsight][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="52ce6-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="52ce6-137">**Instalar Solr**</span><span class="sxs-lookup"><span data-stu-id="52ce6-137">**Install Solr**</span></span> |<span data-ttu-id="52ce6-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="52ce6-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="52ce6-139">Consulte [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="52ce6-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="52ce6-140">- **Instalar o Giraph**</span><span class="sxs-lookup"><span data-stu-id="52ce6-140">- **Install Giraph**</span></span> |<span data-ttu-id="52ce6-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="52ce6-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="52ce6-142">Consulte [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="52ce6-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="52ce6-143">**Pré-carregar bibliotecas Hive**</span><span class="sxs-lookup"><span data-stu-id="52ce6-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="52ce6-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="52ce6-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="52ce6-145">Consulte [Adicionar bibliotecas do Hive em clusters do HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="52ce6-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="52ce6-146">Scripts de chamada usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="52ce6-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="52ce6-147">**De saudação portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="52ce6-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="52ce6-148">Comece criando um cluster como descrito em [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="52ce6-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="52ce6-149">Em configuração opcional, para Olá **ações de Script** folha, clique em **Adicionar ação de script** tooprovide detalhes sobre a ação de script hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="52ce6-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="52ce6-150">![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "toocustomize de ação de Script de Use um cluster")</span><span class="sxs-lookup"><span data-stu-id="52ce6-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="52ce6-151">Propriedade</span><span class="sxs-lookup"><span data-stu-id="52ce6-151">Property</span></span></th><th><span data-ttu-id="52ce6-152">Valor</span><span class="sxs-lookup"><span data-stu-id="52ce6-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="52ce6-153">Nome</span><span class="sxs-lookup"><span data-stu-id="52ce6-153">Name</span></span></td>
            <td><span data-ttu-id="52ce6-154">Especifique um nome para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="52ce6-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="52ce6-155">URI do script</span><span class="sxs-lookup"><span data-stu-id="52ce6-155">Script URI</span></span></td>
            <td><span data-ttu-id="52ce6-156">Especifique Olá URI toohello script que é invocado toocustomize Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="52ce6-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="52ce6-157">s</span><span class="sxs-lookup"><span data-stu-id="52ce6-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="52ce6-158">Cabeçalho/Trabalho</span><span class="sxs-lookup"><span data-stu-id="52ce6-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="52ce6-159">Especificar nós de saudação (**Head** ou **trabalho**) no qual personalização Olá script é executado.</b>.</span><span class="sxs-lookup"><span data-stu-id="52ce6-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="52ce6-160">parâmetros</span><span class="sxs-lookup"><span data-stu-id="52ce6-160">Parameters</span></span></td>
            <td><span data-ttu-id="52ce6-161">Especifica parâmetros de hello, se exigido pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="52ce6-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="52ce6-162">Pressione ENTER tooadd mais de um script ação tooinstall vários componentes no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="52ce6-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="52ce6-163">Clique em **selecione** toosave Olá configuração da ação de script e continuar com a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="52ce6-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="52ce6-164">Chamar scripts usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="52ce6-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="52ce6-165">Esse script de PowerShell a seguir demonstra como tooinstall Spark no Windows com base em cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52ce6-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="52ce6-166">tooinstall outros softwares, você precisará de arquivo de script hello tooreplace no script hello:</span><span class="sxs-lookup"><span data-stu-id="52ce6-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="52ce6-167">Quando solicitado, insira as credenciais de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="52ce6-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="52ce6-168">Pode levar vários minutos antes de saudação cluster é criado.</span><span class="sxs-lookup"><span data-stu-id="52ce6-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="52ce6-169">Scripts de chamada usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="52ce6-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="52ce6-170">Olá exemplo a seguir demonstra como tooinstall Spark no Windows com base em cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52ce6-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="52ce6-171">tooinstall outros softwares, você precisará de arquivo de script hello tooreplace no código de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ce6-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="52ce6-172">**toocreate um cluster HDInsight com Spark**</span><span class="sxs-lookup"><span data-stu-id="52ce6-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="52ce6-173">No Visual Studio, crie um aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="52ce6-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="52ce6-174">Olá Nuget Package Manager Console, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="52ce6-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="52ce6-175">Saudação de uso usando as instruções no arquivo Program.cs de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="52ce6-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="52ce6-176">Coloque o código de saudação na classe Olá com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="52ce6-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="52ce6-177">Pressione **F5** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="52ce6-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="52ce6-178">Suporte para software livre utilizado em clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="52ce6-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="52ce6-179">saudação de serviço do Microsoft Azure HDInsight é uma plataforma flexível que permite que aplicativos de dados grandes de toobuild na nuvem hello usando um ecossistema de tecnologias de código-fonte aberto formado em torno do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="52ce6-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="52ce6-180">Microsoft Azure fornece um nível geral de suporte para tecnologias do código-fonte aberto, conforme discutido em Olá **escopo suporte** seção Olá <a href="http://azure.microsoft.com/support/faq/" target="_blank">site de perguntas Frequentes de suporte do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="52ce6-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="52ce6-181">Olá serviço HDInsight fornece um nível adicional de suporte para alguns dos componentes do hello, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="52ce6-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="52ce6-182">Há dois tipos de componentes de código-fonte aberto que estão disponíveis no hello serviço HDInsight:</span><span class="sxs-lookup"><span data-stu-id="52ce6-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="52ce6-183">**Componentes internos** -esses componentes são pré-instaladas em clusters de HDInsight e fornecem funcionalidade principal do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="52ce6-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="52ce6-184">Por exemplo, o ResourceManager YARN, linguagem de consulta de Hive hello (HiveQL) e biblioteca de Mahout Olá pertencem toothis categoria.</span><span class="sxs-lookup"><span data-stu-id="52ce6-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="52ce6-185">Uma lista completa dos componentes do cluster está disponível em [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight?](hdinsight-component-versioning.md) </a>.</span><span class="sxs-lookup"><span data-stu-id="52ce6-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="52ce6-186">**Componentes personalizados** -você, como um usuário de cluster hello, instalar ou usar em sua carga de trabalho qualquer componente criado por você ou disponível na comunidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ce6-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="52ce6-187">Componentes internos são totalmente suportados e ajudarão tooisolate e resolver problemas relacionados toothese componentes Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="52ce6-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="52ce6-188">Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados e ajudarão tooisolate e resolver problemas relacionados toothese componentes Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="52ce6-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="52ce6-189">Componentes personalizados recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ce6-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="52ce6-190">Isso pode resultar em resolver o problema de saudação ou solicitando que tooengage de canais disponíveis para Olá abrir tecnologias de origem onde profundo conhecimento para que a tecnologia é encontrado.</span><span class="sxs-lookup"><span data-stu-id="52ce6-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="52ce6-191">Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). E mais, os projetos Apache têm sites de projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="52ce6-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="52ce6-192">Olá serviço HDInsight fornece várias maneiras de componentes personalizados toouse.</span><span class="sxs-lookup"><span data-stu-id="52ce6-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="52ce6-193">Independentemente de como um componente for usado ou instalado no cluster hello, hello mesmo nível de suporte se aplica.</span><span class="sxs-lookup"><span data-stu-id="52ce6-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="52ce6-194">Abaixo está uma lista das maneiras mais comuns de saudação que componentes personalizados podem ser usados em clusters de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="52ce6-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="52ce6-195">Envio de trabalho - Hadoop ou outros tipos de trabalhos em execução ou usam componentes personalizados pode ser enviado toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="52ce6-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="52ce6-196">Personalização de cluster - durante a criação do cluster, você pode especificar configurações adicionais e componentes personalizados que serão instalados em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="52ce6-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="52ce6-197">Exemplos - para os componentes personalizados, Microsoft e outros podem fornecer exemplos de como esses componentes podem ser usados em clusters de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="52ce6-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="52ce6-198">Esses exemplos são fornecidos sem suporte.</span><span class="sxs-lookup"><span data-stu-id="52ce6-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="52ce6-199">Desenvolver scripts de Ação de script</span><span class="sxs-lookup"><span data-stu-id="52ce6-199">Develop Script Action scripts</span></span>
<span data-ttu-id="52ce6-200">Confira [Desenvolver scripts da Ação de Script para o HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="52ce6-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="52ce6-201">Consulte também</span><span class="sxs-lookup"><span data-stu-id="52ce6-201">See also</span></span>
* <span data-ttu-id="52ce6-202">[Criar clusters de Hadoop em HDInsight] [ hdinsight-provision-cluster] fornece instruções sobre como toocreate uma HDInsight cluster usando outras opções personalizadas.</span><span class="sxs-lookup"><span data-stu-id="52ce6-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="52ce6-203">[Desenvolver scripts de Ação de Script para o HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="52ce6-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="52ce6-204">[Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="52ce6-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="52ce6-205">[Instalar e usar R em clusters do HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="52ce6-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="52ce6-206">[Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="52ce6-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="52ce6-207">[Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="52ce6-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Estágios durante a criação de cluster"
