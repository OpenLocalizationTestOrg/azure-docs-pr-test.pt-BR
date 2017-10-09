---
title: clusters aaaInstall e uso de Giraph no Hadoop no HDInsight - Azure | Microsoft Docs
description: Saiba como toocustomize HDInsight cluster com Giraph e toouse Giraph.
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
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="6735b-103">Instalar e usar o Giraph em clusters HDInsight baseados no Windows</span><span class="sxs-lookup"><span data-stu-id="6735b-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="6735b-104">Saiba como toocustomize Windows com base no cluster HDInsight com Giraph usando a ação de Script e toouse Giraph tooprocess em larga escala gráficos.</span><span class="sxs-lookup"><span data-stu-id="6735b-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="6735b-105">Para obter informações sobre como usar o Giraph com um cluster baseado no Linux, consulte [Instalar o Giraph em clusters Hadoop do HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6735b-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6735b-106">Olá etapas para esse documento só funciona com clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="6735b-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="6735b-107">O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="6735b-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="6735b-108">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6735b-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6735b-109">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6735b-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="6735b-110">Para obter informações sobre como tooinstall Giraph em um cluster HDInsight baseados em Linux, consulte [Giraph instalar em clusters de HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6735b-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="6735b-111">Você pode instalar o Giraph em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight usando a *Ação de Script*.</span><span class="sxs-lookup"><span data-stu-id="6735b-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="6735b-112">Tooinstall um script de exemplo Giraph em um cluster HDInsight está disponível de um blob de armazenamento do Azure somente leitura em [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="6735b-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="6735b-113">script de exemplo Hello funciona apenas com a versão 3.1 do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6735b-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="6735b-114">Para obter mais informações sobre as versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="6735b-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="6735b-115">**Artigos relacionados**</span><span class="sxs-lookup"><span data-stu-id="6735b-115">**Related articles**</span></span>

* [<span data-ttu-id="6735b-116">Instalar o Giraph em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="6735b-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="6735b-117">[Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="6735b-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="6735b-118">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="6735b-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="6735b-119">[Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="6735b-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="6735b-120">O que é Giraph?</span><span class="sxs-lookup"><span data-stu-id="6735b-120">What is Giraph?</span></span>
<span data-ttu-id="6735b-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> permite gráfico tooperform processamento usando Hadoop e pode ser usado com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6735b-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="6735b-122">Gráficos de modelar relações entre objetos, como conexões Olá entre roteadores em uma rede grande como saudação da Internet, ou relações entre as pessoas em redes sociais (às vezes chamado tooas um gráfico social).</span><span class="sxs-lookup"><span data-stu-id="6735b-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="6735b-123">Processamento de gráfico permite que você tooreason sobre relações de saudação entre objetos em um gráfico, como:</span><span class="sxs-lookup"><span data-stu-id="6735b-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="6735b-124">Identificar possíveis amigos com base em suas relações atuais.</span><span class="sxs-lookup"><span data-stu-id="6735b-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="6735b-125">Identificando a rota mais curta Olá entre dois computadores em uma rede.</span><span class="sxs-lookup"><span data-stu-id="6735b-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="6735b-126">Calculando a classificação de página Olá das páginas da Web.</span><span class="sxs-lookup"><span data-stu-id="6735b-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="6735b-127">Instalar o Giraph usando o Portal</span><span class="sxs-lookup"><span data-stu-id="6735b-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="6735b-128">Começar a criar um cluster usando Olá **criação personalizada** opção, conforme descrito em [Hadoop criar clusters de HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="6735b-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="6735b-129">Em Olá **ações de Script** página do Assistente de saudação, clique em **Adicionar ação de script** tooprovide detalhes sobre a ação de script hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="6735b-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="6735b-130">![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize de ação de Script de Use um cluster")</span><span class="sxs-lookup"><span data-stu-id="6735b-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="6735b-131">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6735b-131">Property</span></span></th><th><span data-ttu-id="6735b-132">Valor</span><span class="sxs-lookup"><span data-stu-id="6735b-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="6735b-133">Nome</span><span class="sxs-lookup"><span data-stu-id="6735b-133">Name</span></span></td>
            <td><span data-ttu-id="6735b-134">Especifique um nome para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="6735b-134">Specify a name for hello script action.</span></span> <span data-ttu-id="6735b-135">Por exemplo, <b>Instalar o Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="6735b-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="6735b-136">URI do script</span><span class="sxs-lookup"><span data-stu-id="6735b-136">Script URI</span></span></td>
            <td><span data-ttu-id="6735b-137">Especifique o script hello de toohello de identificador de recurso uniforme (URI) que é invocado toocustomize Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="6735b-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="6735b-138">Por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="6735b-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="6735b-139">Tipo de nó</span><span class="sxs-lookup"><span data-stu-id="6735b-139">Node Type</span></span></td>
            <td><span data-ttu-id="6735b-140">Especifica Olá nós em que o script de personalização de saudação é executado.</span><span class="sxs-lookup"><span data-stu-id="6735b-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="6735b-141">Você pode escolher <b>Todos os nós</b>, <b>Somente nós do cabeçalho</b> ou <b>Somente nós de trabalho</b>.</span><span class="sxs-lookup"><span data-stu-id="6735b-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="6735b-142">parâmetros</span><span class="sxs-lookup"><span data-stu-id="6735b-142">Parameters</span></span></td>
            <td><span data-ttu-id="6735b-143">Especifica parâmetros de hello, se exigido pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="6735b-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="6735b-144">Olá script tooinstall Giraph não requer nenhum parâmetro, você poderá deixar isso em branco.</span><span class="sxs-lookup"><span data-stu-id="6735b-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="6735b-145">Você pode adicionar mais de um tooinstall de ação de script vários componentes no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6735b-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="6735b-146">Depois de adicionar scripts de saudação, clique em Olá toostart de marca de seleção Criar cluster hello.</span><span class="sxs-lookup"><span data-stu-id="6735b-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="6735b-147">Usar o Giraph</span><span class="sxs-lookup"><span data-stu-id="6735b-147">Use Giraph</span></span>
<span data-ttu-id="6735b-148">Usamos Olá SimpleShortestPathsComputation exemplo toodemonstrate Olá basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementação para localizar o caminho mais curto de saudação entre objetos em um gráfico.</span><span class="sxs-lookup"><span data-stu-id="6735b-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="6735b-149">Use Olá etapas tooupload Olá exemplo hello e dados exemplo jar, executar um trabalho usando o exemplo de SimpleShortestPathsComputation hello e, em seguida, exibir hello resultados a seguir.</span><span class="sxs-lookup"><span data-stu-id="6735b-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="6735b-150">Carregar um tooAzure de arquivo de dados de exemplo armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="6735b-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="6735b-151">Em sua estação de trabalho local, crie um novo arquivo chamado **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="6735b-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="6735b-152">Ela deve conter Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="6735b-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="6735b-153">Carregar Olá tiny_graph.txt arquivo toohello armazenamento primário para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6735b-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="6735b-154">Para obter instruções sobre como tooupload dados, consulte [carregar dados para trabalhos de Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="6735b-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="6735b-155">Esses dados descrevem uma relação entre objetos em um gráfico direcionado, usando o formato de saudação [fonte\_id, fonte\_valor [[dest\_id], [borda\_valor],...]]. Cada linha representa uma relação entre um objeto **source\_id** e um ou mais objetos **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="6735b-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="6735b-156">Olá **borda\_valor** (ou peso) pode ser pensada como intensidade hello ou distância de conexão Olá entre **source_id** e **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="6735b-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="6735b-157">Desenhado, e usando o valor hello (ou peso) como a distância Olá entre objetos, Olá acima dados poderia se parecer com:</span><span class="sxs-lookup"><span data-stu-id="6735b-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![tiny_graph.txt Desenhado como círculos com linhas de distância variável entre](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="6735b-159">Execute o exemplo de SimpleShortestPathsComputation hello.</span><span class="sxs-lookup"><span data-stu-id="6735b-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="6735b-160">Use Olá seguindo o exemplo hello do Azure PowerShell cmdlets toorun usando o arquivo de tiny_graph.txt hello como entrada.</span><span class="sxs-lookup"><span data-stu-id="6735b-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6735b-161">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="6735b-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="6735b-162">Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6735b-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="6735b-163">Siga as etapas de saudação em [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Olá última versão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="6735b-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="6735b-164">Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6735b-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

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
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="6735b-165">Olá, o exemplo acima, substitua **clustername** com nome de saudação do cluster HDInsight com Giraph instalado.</span><span class="sxs-lookup"><span data-stu-id="6735b-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="6735b-166">Exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6735b-166">View hello results.</span></span> <span data-ttu-id="6735b-167">Quando tiver terminado de trabalho hello, Olá resultados serão armazenados em dois arquivos de saída no hello **wasb: / / / exemplo/out/shotestpaths** pasta.</span><span class="sxs-lookup"><span data-stu-id="6735b-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="6735b-168">Olá arquivos são chamados **parte-m-00001** e **parte-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="6735b-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="6735b-169">Execute Olá saída de hello toodownload e exibir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6735b-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="6735b-170">Isso criará Olá **saída/exemplo/shortestpaths** estrutura de diretório no diretório atual de saudação na sua estação de trabalho e download Olá duas saída arquivos toothat local.</span><span class="sxs-lookup"><span data-stu-id="6735b-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="6735b-171">Saudação de uso **Cat** cmdlet toodisplay Olá conteúdo arquivos hello:</span><span class="sxs-lookup"><span data-stu-id="6735b-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="6735b-172">saída de Hello deve aparecer a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="6735b-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="6735b-173">exemplo de SimpleShortestPathComputation Hello é toostart codificado com o objeto ID 1 e localizar Olá shortest path tooother objetos.</span><span class="sxs-lookup"><span data-stu-id="6735b-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="6735b-174">Para a saída de hello deve ser lidos como `destination_id distance`, onde distância é Olá valor (ou peso) das bordas Olá percorridas entre o objeto ID 1 e ID de destino hello.</span><span class="sxs-lookup"><span data-stu-id="6735b-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="6735b-175">Visualizar isso, você pode verificar os resultados de saudação percorrerem caminhos mais curto Olá ID 1 e todos os outros objetos.</span><span class="sxs-lookup"><span data-stu-id="6735b-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="6735b-176">Observe que Olá caminho mais curto entre ID 1 e 4 ID é 5.</span><span class="sxs-lookup"><span data-stu-id="6735b-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="6735b-177">Essa é a distância total Olá entre <span style="color:orange">ID 1 e 3</span>e, em seguida, <span style="color:red">ID 3 e 4</span>.</span><span class="sxs-lookup"><span data-stu-id="6735b-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Desenho dos objetos como círculos com os percursos mais curtos entre](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="6735b-179">Instalar o Giraph usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6735b-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="6735b-180">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="6735b-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="6735b-181">exemplo Hello demonstra como tooinstall Spark usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="6735b-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="6735b-182">Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="6735b-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="6735b-183">Instalar o Giraph usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="6735b-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="6735b-184">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="6735b-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="6735b-185">exemplo Hello demonstra como tooinstall Spark usando Olá .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="6735b-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="6735b-186">Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="6735b-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="6735b-187">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6735b-187">See also</span></span>
* [<span data-ttu-id="6735b-188">Instalar o Giraph em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="6735b-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="6735b-189">[Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="6735b-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="6735b-190">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="6735b-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="6735b-191">[Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="6735b-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="6735b-192">[Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]: exemplo de Ação de Script sobre a instalação do Spark.</span><span class="sxs-lookup"><span data-stu-id="6735b-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="6735b-193">[Instalar R em clusters HDInsight][hdinsight-install-r]: exemplo de Ação de Script sobre a instalação do R.</span><span class="sxs-lookup"><span data-stu-id="6735b-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="6735b-194">[Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install.md): exemplo de Ação de Script sobre a instalação do Solr.</span><span class="sxs-lookup"><span data-stu-id="6735b-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
