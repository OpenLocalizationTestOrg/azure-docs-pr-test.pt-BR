---
title: "Personalizar os Clusters HDInsight usando ações de script – Azure | Microsoft Docs"
description: "Saiba como personalizar os clusters HDInsight usando a ação de Script."
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
ms.openlocfilehash: ec95b6d66c71b4278dd1e16807fcc75f5e8b1c36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="e9a18-103">Personalizar clusters HDInsight baseados em Windows usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="e9a18-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="e9a18-104">**Ação de Script** pode ser usada para invocar [scripts personalizados](hdinsight-hadoop-script-actions.md) durante o processo de criação de cluster para instalar software adicional em um cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-104">**Script Action** can be used to invoke [custom scripts](hdinsight-hadoop-script-actions.md) during the cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="e9a18-105">As informações contidas neste artigo são específicas aos clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="e9a18-105">The information in this article is specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="e9a18-106">Para cluster baseados em Linux, confira [Personalizar clusters do HDInsight baseados em Linux usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9a18-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="e9a18-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e9a18-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e9a18-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="e9a18-109">Clusters HDInsight também podem ser personalizados de várias outras formas, como incluir contas adicionais do Armazenamento do Azure, alterar os arquivos de configuração do Hadoop (core-site.xml, hive-site.xml, etc.) ou adicionar bibliotecas compartilhadas (p.ex., Hive, Oozie) em locais comuns no cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing the Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in the cluster.</span></span> <span data-ttu-id="e9a18-110">Essas personalizações podem ser feitas por meio do Azure PowerShell, SDK do .NET do Azure HDInsight ou Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9a18-110">These customizations can be done through Azure PowerShell, the Azure HDInsight .NET SDK, or the Azure portal.</span></span> <span data-ttu-id="e9a18-111">Para obter mais informações, veja [Criar clusters Hadoop no HDInsight][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="e9a18-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="e9a18-112">Ação de Script no processo de criação do cluster</span><span class="sxs-lookup"><span data-stu-id="e9a18-112">Script Action in the cluster creation process</span></span>
<span data-ttu-id="e9a18-113">A Ação de Script só é usada enquanto um cluster está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="e9a18-113">Script Action is only used while a cluster is in the process of being created.</span></span> <span data-ttu-id="e9a18-114">O diagrama a seguir ilustra quando a Ação de Script é executada durante o processo de criação:</span><span class="sxs-lookup"><span data-stu-id="e9a18-114">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="e9a18-115">![Personalização do cluster HDInsight e estágios durante a criação de cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="e9a18-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="e9a18-116">Quando o script é executado, o cluster entra no estágio **ClusterCustomization** .</span><span class="sxs-lookup"><span data-stu-id="e9a18-116">When the script is running, the cluster enters the **ClusterCustomization** stage.</span></span> <span data-ttu-id="e9a18-117">Nesse estágio, o script é executado na conta de administrador do sistema, em paralelo com todos os nós especificados no cluster e fornece privilégios totais de administrador nos nós.</span><span class="sxs-lookup"><span data-stu-id="e9a18-117">At this stage, the script is run under the system admin account, in parallel on all the specified nodes in the cluster, and provides full admin privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="e9a18-118">Por ter privilégios administrativos nos nós de cluster durante o estágio **ClusterCustomization** , você pode usar o script para executar operações como parar e iniciar serviços, inclusive serviços relacionados ao Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e9a18-118">Because you have admin privileges on the cluster nodes during the **ClusterCustomization** stage, you can use the script to perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="e9a18-119">Logo, como parte do script, você deve garantir que os serviços Ambari e outros serviços relacionados ao Hadoop estejam funcionando antes do script terminar a execução.</span><span class="sxs-lookup"><span data-stu-id="e9a18-119">So, as part of the script, you must ensure that the Ambari services and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="e9a18-120">Esses serviços são necessários para verificar a integridade e o estado do cluster enquanto ele estiver sendo criado.</span><span class="sxs-lookup"><span data-stu-id="e9a18-120">These services are required to successfully ascertain the health and state of the cluster while it is being created.</span></span> <span data-ttu-id="e9a18-121">Se você alterar qualquer configuração no cluster que afete esses serviços, é necessário usar as funções auxiliares que são fornecidas.</span><span class="sxs-lookup"><span data-stu-id="e9a18-121">If you change any configuration on the cluster that affects these services, you must use the helper functions that are provided.</span></span> <span data-ttu-id="e9a18-122">Para obter mais informações sobre funções auxiliares, confira [Desenvolver scripts de Ação de Script para o HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="e9a18-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="e9a18-123">Os logs de saída e de erros do script são armazenados na conta padrão do Armazenamento que você especificou para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-123">The output and the error logs for the script are stored in the default Storage account you specified for the cluster.</span></span> <span data-ttu-id="e9a18-124">Os logs são armazenados em uma tabela de nome **u<\fragmento-do-nome-do-cluster><\carimbo-de-data-e-hora>setuplog**.</span><span class="sxs-lookup"><span data-stu-id="e9a18-124">The logs are stored in a table with the name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="e9a18-125">São logs agregados dos scripts executados em todos os nós (nó de cabeçalho e nós de trabalho) no cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-125">These are aggregate logs from the script run on all the nodes (head node and worker nodes) in the cluster.</span></span>

<span data-ttu-id="e9a18-126">Cada cluster pode aceitar várias ações de script, que são invocadas na ordem em que elas são especificadas.</span><span class="sxs-lookup"><span data-stu-id="e9a18-126">Each cluster can accept multiple script actions that are invoked in the order in which they are specified.</span></span> <span data-ttu-id="e9a18-127">Um script pode ser executado no nó principal, nos nós de trabalho ou em ambos.</span><span class="sxs-lookup"><span data-stu-id="e9a18-127">A script can be ran on the head node, the worker nodes, or both.</span></span>

<span data-ttu-id="e9a18-128">O HDInsight fornece vários scripts para instalar os seguintes componentes em clusters do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e9a18-128">HDInsight provides several scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="e9a18-129">Nome</span><span class="sxs-lookup"><span data-stu-id="e9a18-129">Name</span></span> | <span data-ttu-id="e9a18-130">Script</span><span class="sxs-lookup"><span data-stu-id="e9a18-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="e9a18-131">**Instalar Spark**</span><span class="sxs-lookup"><span data-stu-id="e9a18-131">**Install Spark**</span></span> |<span data-ttu-id="e9a18-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="e9a18-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="e9a18-133">Consulte [Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="e9a18-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="e9a18-134">**Instalar R**</span><span class="sxs-lookup"><span data-stu-id="e9a18-134">**Install R**</span></span> |<span data-ttu-id="e9a18-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="e9a18-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="e9a18-136">Consulte [Instalar e usar o R em clusters HDInsight][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="e9a18-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="e9a18-137">**Instalar Solr**</span><span class="sxs-lookup"><span data-stu-id="e9a18-137">**Install Solr**</span></span> |<span data-ttu-id="e9a18-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="e9a18-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="e9a18-139">Consulte [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="e9a18-140">- **Instalar o Giraph**</span><span class="sxs-lookup"><span data-stu-id="e9a18-140">- **Install Giraph**</span></span> |<span data-ttu-id="e9a18-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="e9a18-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="e9a18-142">Consulte [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="e9a18-143">**Pré-carregar bibliotecas Hive**</span><span class="sxs-lookup"><span data-stu-id="e9a18-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="e9a18-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="e9a18-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="e9a18-145">Consulte [Adicionar bibliotecas do Hive em clusters do HDInsight](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="e9a18-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-the-azure-portal"></a><span data-ttu-id="e9a18-146">Chamar scripts usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e9a18-146">Call scripts using the Azure portal</span></span>
<span data-ttu-id="e9a18-147">**No Portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="e9a18-147">**From the Azure portal**</span></span>

1. <span data-ttu-id="e9a18-148">Comece criando um cluster como descrito em [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="e9a18-149">Na Configuração Opcional, para a folha **Ações de Script**, clique em **adicionar ação de script** para fornecer detalhes sobre a ação de script, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="e9a18-149">Under Optional Configuration, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="e9a18-150">![Usar Ação de Script para personalizar um cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Usar Ação de Script para personalizar um cluster")</span><span class="sxs-lookup"><span data-stu-id="e9a18-150">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="e9a18-151">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e9a18-151">Property</span></span></th><th><span data-ttu-id="e9a18-152">Valor</span><span class="sxs-lookup"><span data-stu-id="e9a18-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="e9a18-153">Nome</span><span class="sxs-lookup"><span data-stu-id="e9a18-153">Name</span></span></td>
            <td><span data-ttu-id="e9a18-154">Especifique um nome para a ação de script.</span><span class="sxs-lookup"><span data-stu-id="e9a18-154">Specify a name for the script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="e9a18-155">URI do script</span><span class="sxs-lookup"><span data-stu-id="e9a18-155">Script URI</span></span></td>
            <td><span data-ttu-id="e9a18-156">Especifique o URI para o script que é chamado para personalizar o cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-156">Specify the URI to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="e9a18-157">s</span><span class="sxs-lookup"><span data-stu-id="e9a18-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="e9a18-158">Cabeçalho/Trabalho</span><span class="sxs-lookup"><span data-stu-id="e9a18-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="e9a18-159">Especifique os nós (**Cabeçalho** ou **Trabalho**) nos quais o script de personalização é executado</b>.</span><span class="sxs-lookup"><span data-stu-id="e9a18-159">Specify the nodes (**Head** or **Worker**) on which the customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="e9a18-160">parâmetros</span><span class="sxs-lookup"><span data-stu-id="e9a18-160">Parameters</span></span></td>
            <td><span data-ttu-id="e9a18-161">Especifique os parâmetros, se exigido pelo script.</span><span class="sxs-lookup"><span data-stu-id="e9a18-161">Specify the parameters, if required by the script.</span></span></td></tr>
    </table>

    <span data-ttu-id="e9a18-162">Pressione ENTER para adicionar mais de uma ação de script para instalar vários componentes no cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-162">Press ENTER to add more than one script action to install multiple components on the cluster.</span></span>
3. <span data-ttu-id="e9a18-163">Clique em **Selecionar** para salvar a configuração de ação de script e continuar com a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-163">Click **Select** to save the script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="e9a18-164">Chamar scripts usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9a18-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="e9a18-165">Esse script PowerShell a seguir demonstra como instalar o Spark no cluster HDInsight baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="e9a18-165">This following PowerShell script demonstrates how to install Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" to list IDs.

    $nameToken = "<Enter A Name Token>"  # The token is use to create Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect to Azure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare the dependent components
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

    # Specify the configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action to the cluster configuration
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


<span data-ttu-id="e9a18-166">Para instalar outros softwares, você precisará substituir o arquivo de script no script:</span><span class="sxs-lookup"><span data-stu-id="e9a18-166">To install other software, you will need to replace the script file in the script:</span></span>

<span data-ttu-id="e9a18-167">Quando solicitado, insira as credenciais para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-167">When prompted, enter the credentials for the cluster.</span></span> <span data-ttu-id="e9a18-168">Pode levar alguns minutos até que o cluster seja criado.</span><span class="sxs-lookup"><span data-stu-id="e9a18-168">It can take several minutes before the cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="e9a18-169">Scripts de chamada usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="e9a18-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="e9a18-170">A amostra a seguir demonstra como instalar o Spark no cluster HDInsight baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="e9a18-170">The following sample demonstrates how to install Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="e9a18-171">Para instalar outros softwares, você precisará substituir o arquivo de script no código.</span><span class="sxs-lookup"><span data-stu-id="e9a18-171">To install other software, you will need to replace the script file in the code.</span></span>

<span data-ttu-id="e9a18-172">**Para criar um cluster HDInsight com Spark**</span><span class="sxs-lookup"><span data-stu-id="e9a18-172">**To create an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="e9a18-173">No Visual Studio, crie um aplicativo de console C#.</span><span class="sxs-lookup"><span data-stu-id="e9a18-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="e9a18-174">No Console do Gerenciador de Pacotes NuGet, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="e9a18-174">From the Nuget Package Manager Console, run the following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="e9a18-175">Use as seguintes instruções using no arquivo Program.cs:</span><span class="sxs-lookup"><span data-stu-id="e9a18-175">Use the following using statements in the Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="e9a18-176">Substitua o código na classe pelo seguinte:</span><span class="sxs-lookup"><span data-stu-id="e9a18-176">Place the code in the class with the following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
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
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">The AAD tenant ID</param>
        /// <param name="ClientId">The AAD client ID</param>
        /// <param name="SubscriptionId">The Azure subscription ID</param>
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
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="e9a18-177">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e9a18-177">Press **F5** to run the application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="e9a18-178">Suporte para software livre utilizado em clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9a18-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="e9a18-179">O serviço Microsoft Azure HDInsight é uma plataforma flexível que permite compilar aplicativos Big Data na nuvem usando um ecossistema de tecnologias de software livre baseado no Hadoop.</span><span class="sxs-lookup"><span data-stu-id="e9a18-179">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="e9a18-180">O Microsoft Azure fornece um nível geral de suporte para tecnologias de software livre, como discutimos na seção **Escopo do suporte** do <a href="http://azure.microsoft.com/support/faq/" target="_blank">site de Perguntas frequentes sobre o Suporte do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="e9a18-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="e9a18-181">O serviço HDInsight fornece um nível adicional de suporte a alguns dos componentes, como descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="e9a18-181">The HDInsight service provides an additional level of support for some of the components, as described below.</span></span>

<span data-ttu-id="e9a18-182">Há dois tipos de componentes de software livre disponíveis no serviço HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e9a18-182">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="e9a18-183">**Componentes internos** : estes componentes estão pré-instalado em clusters HDInsight e fornecem a funcionalidade básica do cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="e9a18-184">Por exemplo, o gerenciador de recursos YARN RM, o HiveQL (linguagem de consulta do Hive) e a biblioteca Mahout pertencem a esta categoria.</span><span class="sxs-lookup"><span data-stu-id="e9a18-184">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="e9a18-185">Uma lista completa dos componentes de cluster está disponível em [Novidades nas versões do cluster Hadoop fornecidas pelo HDInsight?](hdinsight-component-versioning.md)</a>.</span><span class="sxs-lookup"><span data-stu-id="e9a18-185">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="e9a18-186">**Componentes personalizados** : como usuário do cluster, você pode instalar ou usar em sua carga de trabalho qualquer componente disponível na comunidade ou criado por você.</span><span class="sxs-lookup"><span data-stu-id="e9a18-186">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

<span data-ttu-id="e9a18-187">Componentes internos são totalmente compatíveis e o Suporte da Microsoft ajudará a isolar e resolver problemas relacionados a esses componentes.</span><span class="sxs-lookup"><span data-stu-id="e9a18-187">Built-in components are fully supported, and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>

> [!WARNING]
> <span data-ttu-id="e9a18-188">Há suporte total a componentes fornecidos com o cluster HDInsight e o Suporte da Microsoft ajudará a isolar e resolver problemas relacionados a esses componentes.</span><span class="sxs-lookup"><span data-stu-id="e9a18-188">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="e9a18-189">Componentes personalizados recebem suporte comercialmente razoável para ajudá-lo a solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="e9a18-189">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="e9a18-190">Isso pode resultar na resolução do problema ou na solicitação de você buscar nos canais disponíveis as tecnologias de código-fonte aberto, onde é possível encontrar conhecimento aprofundado sobre essa tecnologia.</span><span class="sxs-lookup"><span data-stu-id="e9a18-190">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="e9a18-191">Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="e9a18-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="e9a18-192">E mais, os projetos Apache têm sites de projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="e9a18-192">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="e9a18-193">O serviço HDInsight possibilita o uso de componentes personalizados de várias formas.</span><span class="sxs-lookup"><span data-stu-id="e9a18-193">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="e9a18-194">Seja como for usado ou instalado em um cluster, o mesmo nível de suporte se aplica ao componente.</span><span class="sxs-lookup"><span data-stu-id="e9a18-194">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span></span> <span data-ttu-id="e9a18-195">Mostramos, a seguir, uma lista das formas mais comuns de usar os componentes personalizados em clusters HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e9a18-195">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="e9a18-196">Envio de trabalhos: trabalhos do Hadoop ou de outros tipos que executam ou usam componentes personalizados podem ser enviados para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-196">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>
2. <span data-ttu-id="e9a18-197">Personalização de clusters: durante a criação de clusters, você pode especificar configurações adicionais e componentes personalizados que serão instalados nos nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="e9a18-197">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on the cluster nodes.</span></span>
3. <span data-ttu-id="e9a18-198">Exemplos: para componentes personalizados populares, a Microsoft e outras empresas podem fornecer exemplos de uso desses componentes em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e9a18-198">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="e9a18-199">Esses exemplos são fornecidos sem suporte.</span><span class="sxs-lookup"><span data-stu-id="e9a18-199">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="e9a18-200">Desenvolver scripts de Ação de script</span><span class="sxs-lookup"><span data-stu-id="e9a18-200">Develop Script Action scripts</span></span>
<span data-ttu-id="e9a18-201">Confira [Desenvolver scripts da Ação de Script para o HDInsight][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="e9a18-201">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="e9a18-202">Consulte também</span><span class="sxs-lookup"><span data-stu-id="e9a18-202">See also</span></span>
* <span data-ttu-id="e9a18-203">[Criar clusters Hadoop no HDInsight][hdinsight-provision-cluster] fornece instruções sobre como criar um cluster HDInsight usando outras opções personalizadas.</span><span class="sxs-lookup"><span data-stu-id="e9a18-203">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="e9a18-204">[Desenvolver scripts de Ação de Script para o HDInsight][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="e9a18-204">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="e9a18-205">[Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="e9a18-205">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="e9a18-206">[Instalar e usar R em clusters do HDInsight][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="e9a18-206">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="e9a18-207">[Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-207">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="e9a18-208">[Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="e9a18-208">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="e9a18-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Estágios durante a criação de cluster"</span><span class="sxs-lookup"><span data-stu-id="e9a18-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
