---
title: "Instalar e usar o Giraph nos clusters Hadoop no HDInsight – Azure | Microsoft Docs"
description: Saiba como personalizar o cluster HDInsight com o Giraph, e como usar o Giraph.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="8d0c4-103">Instalar e usar o Giraph em clusters HDInsight baseados no Windows</span><span class="sxs-lookup"><span data-stu-id="8d0c4-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="8d0c4-104">Saiba como personalizar o cluster HDInsight baseado em Windows com Giraph usando Ação de Ação, e como usar o Giraph para processar gráficos em larga escala.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="8d0c4-105">Para obter informações sobre como usar o Giraph com um cluster baseado no Linux, consulte [Instalar o Giraph em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d0c4-106">As etapas neste documento só funcionam com clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="8d0c4-107">O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="8d0c4-108">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8d0c4-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="8d0c4-110">Para obter informações sobre como instalar o Giraph com um cluster HDInsight baseado no Linux, consulte [Instalar o Giraph em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="8d0c4-111">Você pode instalar o Giraph em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight usando a *Ação de Script*.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="8d0c4-112">Um script de exemplo para instalar o Giraph em um cluster HDInsight está disponível em um blob de armazenamento do Azure somente leitura em [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="8d0c4-113">O script de exemplo funciona apenas com o cluster HDInsight versão 3.1.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="8d0c4-114">Para obter mais informações sobre as versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="8d0c4-115">**Artigos relacionados**</span><span class="sxs-lookup"><span data-stu-id="8d0c4-115">**Related articles**</span></span>

* [<span data-ttu-id="8d0c4-116">Instalar o Giraph em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="8d0c4-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="8d0c4-117">[Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d0c4-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="8d0c4-118">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="8d0c4-119">[Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="8d0c4-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="8d0c4-120">O que é Giraph?</span><span class="sxs-lookup"><span data-stu-id="8d0c4-120">What is Giraph?</span></span>
<span data-ttu-id="8d0c4-121">O <a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> permite executar processamento de gráficos usando o Hadoop e pode ser usado com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="8d0c4-122">Os gráficos modelam as relações entre objetos, como as conexões entre roteadores em uma rede grande, como a Internet, ou as relações entre as pessoas nas redes sociais (às vezes chamados de gráficos sociais).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="8d0c4-123">O processamento de tabelas permite que você faça a análise das relações entre objetos em uma tabela, como:</span><span class="sxs-lookup"><span data-stu-id="8d0c4-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="8d0c4-124">Identificar possíveis amigos com base em suas relações atuais.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="8d0c4-125">Identificar a menor rota entre dois computadores em uma rede.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="8d0c4-126">Calcular a ordem de classificação de página da Web.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="8d0c4-127">Instalar o Giraph usando o Portal</span><span class="sxs-lookup"><span data-stu-id="8d0c4-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="8d0c4-128">Comece a criar um cluster usando a opção **CUSTOM CREATE**, como descrito em [Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="8d0c4-129">Na página **Ações de Script** do assistente, clique em **adicionar ação de script** para fornecer detalhes sobre a ação de script, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="8d0c4-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="8d0c4-130">![Usar Ação de Script para personalizar um cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Usar Ação de Script para personalizar um cluster")</span><span class="sxs-lookup"><span data-stu-id="8d0c4-130">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="8d0c4-131">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8d0c4-131">Property</span></span></th><th><span data-ttu-id="8d0c4-132">Valor</span><span class="sxs-lookup"><span data-stu-id="8d0c4-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="8d0c4-133">Nome</span><span class="sxs-lookup"><span data-stu-id="8d0c4-133">Name</span></span></td>
            <td><span data-ttu-id="8d0c4-134">Especifique um nome para a ação de script.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-134">Specify a name for the script action.</span></span> <span data-ttu-id="8d0c4-135">Por exemplo, <b>Instalar o Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="8d0c4-136">URI do script</span><span class="sxs-lookup"><span data-stu-id="8d0c4-136">Script URI</span></span></td>
            <td><span data-ttu-id="8d0c4-137">Especifique o URI (Uniform Resource Identifier) do script invocado para personalizar o cluster.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="8d0c4-138">Por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="8d0c4-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="8d0c4-139">Tipo de nó</span><span class="sxs-lookup"><span data-stu-id="8d0c4-139">Node Type</span></span></td>
            <td><span data-ttu-id="8d0c4-140">Especifique os nós em que o script de personalização deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="8d0c4-141">Você pode escolher <b>Todos os nós</b>, <b>Somente nós do cabeçalho</b> ou <b>Somente nós de trabalho</b>.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="8d0c4-142">parâmetros</span><span class="sxs-lookup"><span data-stu-id="8d0c4-142">Parameters</span></span></td>
            <td><span data-ttu-id="8d0c4-143">Especifique os parâmetros, se exigido pelo script.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="8d0c4-144">O script para instalar o Giraph não requer nenhum parâmetro; você pode deixar em branco.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="8d0c4-145">Você pode adicionar mais de uma ação de script para instalar vários componentes no cluster.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="8d0c4-146">Depois de adicionar os scripts, clique na marca de seleção para começar a criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="8d0c4-147">Usar o Giraph</span><span class="sxs-lookup"><span data-stu-id="8d0c4-147">Use Giraph</span></span>
<span data-ttu-id="8d0c4-148">Usamos o exemplo SimpleShortestPathsComputation para demonstrar a implementação básica <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> para encontrar o caminho mais curto entre objetos em um gráfico.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="8d0c4-149">Use as etapas a seguir para carregar os dados de exemplo e o jar do exemplo, executar um trabalho usando o exemplo SimpleShortestPathsComputation e exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="8d0c4-150">Carregue um arquivo de dados de exemplo no armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="8d0c4-151">Em sua estação de trabalho local, crie um novo arquivo chamado **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="8d0c4-152">Ele deve conter as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="8d0c4-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="8d0c4-153">Carregue o arquivo tiny_graph.txt no armazenamento primário para o seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="8d0c4-154">Para obter instruções sobre como carregar dados, consulte [Carregar dados de trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="8d0c4-155">Esses dados descrevem uma relação entre objetos em um gráfico direcionado, usando o formato [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span><span class="sxs-lookup"><span data-stu-id="8d0c4-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span></span> <span data-ttu-id="8d0c4-156">Cada linha representa uma relação entre um objeto **source\_id** e um ou mais objetos **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-156">Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="8d0c4-157">O **edge\_value** (ou peso) pode ser pensado como a força ou a distância da conexão entre **source_id** e **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-157">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="8d0c4-158">Desenhado e utilizando o valor (ou peso) como distância entre os objetos, os dados acima podem se parecer com os demonstrados aqui:</span><span class="sxs-lookup"><span data-stu-id="8d0c4-158">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![tiny_graph.txt Desenhado como círculos com linhas de distância variável entre](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="8d0c4-160">Execute o exemplo SimpleShortestPathsComputation.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-160">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="8d0c4-161">Use os seguintes cmdlets do PowerShell do Azure para executar o exemplo, usando o arquivo tiny_graph.txt como entrada.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-161">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8d0c4-162">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-162">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="8d0c4-163">As etapas neste documento usam os novos cmdlets do HDInsight que funcionam com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-163">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="8d0c4-164">Siga as etapas em [Instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para instalar a versão mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-164">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="8d0c4-165">Se você tiver scripts que precisam ser modificados para usar os novos cmdlets que funcionam com o Azure Resource Manager, confira [Migrando para as ferramentas de desenvolvimento baseadas no Azure Resource Manager dos clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-165">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="8d0c4-166">No exemplo acima, substitua **clustername** pelo nome do cluster HDInsight que tem o Giraph instalado.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-166">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="8d0c4-167">Exiba os resultados.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-167">View the results.</span></span> <span data-ttu-id="8d0c4-168">Assim que o trabalho tiver sido concluído, os resultados serão armazenados em dois arquivos de saída na pasta **wasbs:///example/out/shotestpaths**.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-168">Once the job has finished, the results will be stored in two output files in the **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="8d0c4-169">Os arquivos se chamam **part-m-00001** e **part-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-169">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="8d0c4-170">Execute as etapas a seguir para baixar e exibir a saída:</span><span class="sxs-lookup"><span data-stu-id="8d0c4-170">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="8d0c4-171">Isso criará a estrutura de diretório **example/output/shortestpaths** no diretório atual em sua estação de trabalho e baixará os dois arquivos de saída nesse local.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-171">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="8d0c4-172">Use o cmdlet **Cat** para exibir o conteúdo dos arquivos:</span><span class="sxs-lookup"><span data-stu-id="8d0c4-172">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="8d0c4-173">A saída deve ter aparência similar à exibida a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d0c4-173">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="8d0c4-174">O exemplo SimpleShortestPathComputation está codificado para começar com a ID do objeto 1 e localizar o caminho mais curto para os outros objetos.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-174">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="8d0c4-175">Logo, a saída deve ser lida como `destination_id distance`, em que a distância é o valor (ou peso) dos perímetros percorridos entre a ID do objeto 1 e a ID de destino.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-175">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="8d0c4-176">Visualizando isso, você pode verificar os resultados percorrendo os caminhos mais curtos entre a ID 1 e todos os outros objetos.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-176">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="8d0c4-177">Observe que o caminho mais curto entre a ID 1 e a ID 4 é 5.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-177">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="8d0c4-178">Essa é a distância total entre <span style="color:orange">ID 1 e 3</span> e, em seguida, entre <span style="color:red">ID 3 e 4</span>.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-178">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Desenho dos objetos como círculos com os percursos mais curtos entre](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="8d0c4-180">Instalar o Giraph usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d0c4-180">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="8d0c4-181">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-181">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="8d0c4-182">O exemplo demonstra como instalar o Spark usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-182">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="8d0c4-183">Você precisa personalizar o script para usar [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-183">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="8d0c4-184">Instalar o Giraph usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="8d0c4-184">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="8d0c4-185">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-185">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="8d0c4-186">O exemplo demonstra como instalar o Spark usando o SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-186">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="8d0c4-187">Você precisa personalizar o script para usar [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="8d0c4-187">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="8d0c4-188">Confira também</span><span class="sxs-lookup"><span data-stu-id="8d0c4-188">See also</span></span>
* [<span data-ttu-id="8d0c4-189">Instalar o Giraph em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="8d0c4-189">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="8d0c4-190">[Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d0c4-190">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="8d0c4-191">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-191">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="8d0c4-192">[Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="8d0c4-192">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="8d0c4-193">[Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]: exemplo de Ação de Script sobre a instalação do Spark.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-193">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="8d0c4-194">[Instalar R em clusters HDInsight][hdinsight-install-r]: exemplo de Ação de Script sobre a instalação do R.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-194">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="8d0c4-195">[Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md): exemplo de Ação de Script sobre a instalação do Solr.</span><span class="sxs-lookup"><span data-stu-id="8d0c4-195">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
