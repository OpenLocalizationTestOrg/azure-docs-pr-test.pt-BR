---
title: "Analisar dados de atraso de voo com o Hadoop no HDInsight – Azure | Microsoft Docs"
description: Saiba como usar um script do Windows PowerShell para criar um cluster HDInsight, executar um trabalho do Hive, executar um trabalho do Sqoop e excluir o cluster.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 77790136c9bd3a4e3f7dcabea2fbe0bcffb6eafe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="f125d-103">Analisar dados de atraso de voo usando o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f125d-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="f125d-104">O Hive fornece um meio para executar trabalhos MapReduce do Hadoop por meio de uma linguagem de script semelhante à SQL, chamada *[HiveQL][hadoop-hiveql]*, que pode ser aplicada para resumo, consulta e análise de grandes volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="f125d-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f125d-105">As etapas deste documento exigem um cluster HDInsight baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="f125d-105">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="f125d-106">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="f125d-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f125d-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f125d-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="f125d-108">Para conhecer as etapas que funcionam em um cluster baseado em Linux, confira [Analisar dados de atraso de voos usando o Hive no HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f125d-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="f125d-109">Um dos maiores benefícios do Azure HDInsight é a separação do armazenamento e computação de dados.</span><span class="sxs-lookup"><span data-stu-id="f125d-109">One of the major benefits of Azure HDInsight is the separation of data storage and compute.</span></span> <span data-ttu-id="f125d-110">O HDInsight usa o armazenamento de blob do Azure para o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f125d-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="f125d-111">Um trabalho típico envolve três partes:</span><span class="sxs-lookup"><span data-stu-id="f125d-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="f125d-112">**Armazenamento de dados no repositório de blob do Azure.**</span><span class="sxs-lookup"><span data-stu-id="f125d-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="f125d-113">Por exemplo, os dados climáticos, dados do sensor, logs da Web e, nesse caso, os dados de atraso do voo são salvos no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="f125d-114">**Executar trabalhos.**</span><span class="sxs-lookup"><span data-stu-id="f125d-114">**Run jobs.**</span></span> <span data-ttu-id="f125d-115">Quando for a hora de processar os dados, execute um script do Windows PowerShell (ou um aplicativo cliente) para criar um cluster HDInsight, executar trabalhos e excluir o cluster.</span><span class="sxs-lookup"><span data-stu-id="f125d-115">When it is time to process the data, you run a Windows PowerShell script (or a client application) to create an HDInsight cluster, run jobs, and delete the cluster.</span></span> <span data-ttu-id="f125d-116">Os trabalhos salvam dados de saída no armazenamento de blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-116">The jobs save output data to Azure Blob storage.</span></span> <span data-ttu-id="f125d-117">Os dados de saída são retidos mesmo depois que o cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="f125d-117">The output data is retained even after the cluster is deleted.</span></span> <span data-ttu-id="f125d-118">Dessa forma, você só paga pelo que consumiu.</span><span class="sxs-lookup"><span data-stu-id="f125d-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="f125d-119">**Recupere a saída do armazenamento do blob**ou, neste tutorial, exporte os dados para um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-119">**Retrieve the output from Azure Blob storage**, or in this tutorial, export the data to an Azure SQL database.</span></span>

<span data-ttu-id="f125d-120">O diagrama a seguir ilustra o cenário e a estrutura deste tutorial:</span><span class="sxs-lookup"><span data-stu-id="f125d-120">The following diagram illustrates the scenario and the structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="f125d-122">Observe que os números no diagrama correspondem aos títulos das seções.</span><span class="sxs-lookup"><span data-stu-id="f125d-122">Note that the numbers in the diagram correspond to the section titles.</span></span> <span data-ttu-id="f125d-123">**M** significa o processo principal.</span><span class="sxs-lookup"><span data-stu-id="f125d-123">**M** stands for the main process.</span></span> <span data-ttu-id="f125d-124">**A** significa o conteúdo no apêndice.</span><span class="sxs-lookup"><span data-stu-id="f125d-124">**A** stands for the content in the appendix.</span></span>

<span data-ttu-id="f125d-125">A maior parte do tutorial mostra como usar um script do Windows PowerShell para realizar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="f125d-125">The main portion of the tutorial shows you how to use one Windows PowerShell script to perform the following tasks:</span></span>

* <span data-ttu-id="f125d-126">Crie um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f125d-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="f125d-127">Executar um trabalho do Hive no cluster para calcular a média de atrasos nos aeroportos.</span><span class="sxs-lookup"><span data-stu-id="f125d-127">Run a Hive job on the cluster to calculate average delays at airports.</span></span> <span data-ttu-id="f125d-128">Os dados de atraso de voo são armazenados na conta de Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-128">The flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="f125d-129">Executar um trabalho do Sqoop para exportar a saída do trabalho do Hive para um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-129">Run a Sqoop job to export the Hive job output to an Azure SQL database.</span></span>
* <span data-ttu-id="f125d-130">Excluir o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f125d-130">Delete the HDInsight cluster.</span></span>

<span data-ttu-id="f125d-131">Nos apêndices, você pode encontrar instruções de carregamento dos dados de atraso de voos, de criação/carregamento de cadeias de consulta do Hive e de preparação do banco de dados SQL do Azure para o trabalho do Sqoop.</span><span class="sxs-lookup"><span data-stu-id="f125d-131">In the appendixes, you can find the instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing the Azure SQL database for the Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="f125d-132">As etapas deste documento são específicas de clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="f125d-132">The steps in this document are specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="f125d-133">Para conhecer as etapas que funcionam em um cluster baseado em Linux, confira [Analisar dados de atraso de voos usando o Hive no HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="f125d-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f125d-134">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f125d-134">Prerequisites</span></span>
<span data-ttu-id="f125d-135">Antes de começar este tutorial, você deve ter os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="f125d-135">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="f125d-136">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f125d-136">**An Azure subscription**.</span></span> <span data-ttu-id="f125d-137">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f125d-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="f125d-138">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f125d-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f125d-139">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="f125d-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="f125d-140">As etapas neste documento usam os novos cmdlets do HDInsight que funcionam com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f125d-140">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="f125d-141">Siga as etapas em [Instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para instalar a versão mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f125d-141">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="f125d-142">Se você tiver scripts que precisam ser modificados para usar os novos cmdlets que funcionam com o Azure Resource Manager, confira [Migrando para as ferramentas de desenvolvimento baseadas no Azure Resource Manager dos clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="f125d-142">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="f125d-143">**Arquivos usados neste tutorial**</span><span class="sxs-lookup"><span data-stu-id="f125d-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="f125d-144">Este tutorial usa o desempenho pontual de dados de voos de companhias aéreas do [Research and Innovative Technology Administration, Bureau of Transportation Statistics ou RITA][rita-website].</span><span class="sxs-lookup"><span data-stu-id="f125d-144">This tutorial uses the on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="f125d-145">Uma cópia dos dados foi carregada para um contêiner de armazenamento de Blobs do Azure com a permissão de acesso de Blob Público.</span><span class="sxs-lookup"><span data-stu-id="f125d-145">A copy of the data has been uploaded to an Azure Blob storage container with the Public Blob access permission.</span></span>
<span data-ttu-id="f125d-146">Uma parte do script do PowerShell copia os dados do contêiner de blob público para o contêiner de blob padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="f125d-146">A part of your PowerShell script copies the data from the public blob container to the default blob container of your cluster.</span></span> <span data-ttu-id="f125d-147">O script do HiveQL também é carregado no mesmo contêiner do Blob.</span><span class="sxs-lookup"><span data-stu-id="f125d-147">The HiveQL script is also copied to the same Blob container.</span></span>
<span data-ttu-id="f125d-148">Se quiser saber como obter/carregar os dados em sua própria conta de Armazenamento e como criar/carregar o arquivo de script do HiveQL, consulte o [Apêndice A](#appendix-a) e o [Apêndice B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="f125d-148">If you want to learn how to get/upload the data to your own Storage account, and how to create/upload the HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="f125d-149">A tabela a seguir lista os arquivos usados neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="f125d-149">The following table lists the files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="f125d-150">Arquivos</span><span class="sxs-lookup"><span data-stu-id="f125d-150">Files</span></span></th><th><span data-ttu-id="f125d-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="f125d-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="f125d-152">O arquivo de script HiveQL usado pelo o trabalho do Hive.</span><span class="sxs-lookup"><span data-stu-id="f125d-152">The HiveQL script file used by the Hive job.</span></span> <span data-ttu-id="f125d-153">Este script foi carregado em uma conta de Armazenamento de Blob do Azure com acesso público.</span><span class="sxs-lookup"><span data-stu-id="f125d-153">This script has been uploaded to an Azure Blob storage account with the public access.</span></span> <span data-ttu-id="f125d-154">O <a href="#appendix-b">Apêndice B</a> contém instruções para preparar e carregar este arquivo em sua própria conta de Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file to your own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="f125d-155">Dados de entrada para o trabalho do Hive.</span><span class="sxs-lookup"><span data-stu-id="f125d-155">Input data for the Hive job.</span></span> <span data-ttu-id="f125d-156">Os dados foram carregados em uma conta de armazenamento de Blob do Azure com acesso público.</span><span class="sxs-lookup"><span data-stu-id="f125d-156">The data has been uploaded to an Azure Blob storage account with the public access.</span></span> <span data-ttu-id="f125d-157">O <a href="#appendix-a">Apêndice A</a> contém instruções para obter e carregar os dados em sua própria conta de Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-157"><a href="#appendix-a">Appendix A</a> has instructions on getting the data and uploading the data to your own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="f125d-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="f125d-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="f125d-159">O caminho de saída para o trabalho do Hive.</span><span class="sxs-lookup"><span data-stu-id="f125d-159">The output path for the Hive job.</span></span> <span data-ttu-id="f125d-160">O contêiner padrão é usado para armazenar os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="f125d-160">The default container is used for storing the output data.</span></span></td></tr>
<tr><td><span data-ttu-id="f125d-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="f125d-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="f125d-162">A pasta de status do trabalho do Hive no contêiner padrão.</span><span class="sxs-lookup"><span data-stu-id="f125d-162">The Hive job status folder on the default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="f125d-163">Criar cluster e executar trabalhos do Hive/Sqoop</span><span class="sxs-lookup"><span data-stu-id="f125d-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="f125d-164">O MapReduce do Hadoop é um processamento em lote.</span><span class="sxs-lookup"><span data-stu-id="f125d-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="f125d-165">A maneira mais econômica de executar um trabalho do Hive é criar um cluster para o trabalho e excluir o trabalho após ele ser concluído.</span><span class="sxs-lookup"><span data-stu-id="f125d-165">The most cost-effective way to run a Hive job is to create a cluster for the job, and delete the job after the job is completed.</span></span> <span data-ttu-id="f125d-166">O script a seguir aborda todo o processo.</span><span class="sxs-lookup"><span data-stu-id="f125d-166">The following script covers the whole process.</span></span>
<span data-ttu-id="f125d-167">Para obter mais informações sobre como criar um cluster HDInsight e executar trabalhos do Hive, consulte [Criar clusters do Hadoop no HDInsight][hdinsight-provision] e [Usar o Hive com o HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="f125d-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="f125d-168">**Para executar as consultas do Hive usando o Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="f125d-168">**To run the Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="f125d-169">Crie um banco de dados SQL do Azure para a saída do trabalho do Sqoop usando as instruções fornecidas no [Apêndice C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="f125d-169">Create an Azure SQL database and the table for the Sqoop job output by using the instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="f125d-170">Abra o ISE do Windows PowerShell e execute o seguinte script:</span><span class="sxs-lookup"><span data-stu-id="f125d-170">Open Windows PowerShell ISE, and run the following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure the follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on the version, the folder can be different

    ###########################################
    # (Optional) configure the following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter the Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use the cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create the default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create the default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create the HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare the HiveQL script and source data
    ###########################################

    # Create the temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download the sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data to default container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit the Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit the Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete the cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="f125d-171">Conecte-se ao banco de dados SQL e consulte a média dos atrasos de voo por cidade na tabela AvgDelays:</span><span class="sxs-lookup"><span data-stu-id="f125d-171">Connect to your SQL database and see average flight delays by city in the AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="f125d-173"><a id="appendix-a"></a>Apêndice A - Carregar os dados de atraso de voo para o armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="f125d-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data to Azure Blob storage</span></span>
<span data-ttu-id="f125d-174">Carregar o arquivo de dados e os arquivos de script HiveQL (consulte o [Apêndice B](#appendix-b)) exige algum planejamento.</span><span class="sxs-lookup"><span data-stu-id="f125d-174">Uploading the data file and the HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="f125d-175">A ideia é armazenar os arquivos de dados e o arquivo do HiveQL antes de criar um cluster do HDInsight e executar o trabalho do Hive.</span><span class="sxs-lookup"><span data-stu-id="f125d-175">The idea is to store the data files and the HiveQL file before creating an HDInsight cluster and running the Hive job.</span></span> <span data-ttu-id="f125d-176">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="f125d-176">You have two options:</span></span>

* <span data-ttu-id="f125d-177">**Usar a mesma conta de armazenamento do Azure que será usada pelo cluster do HDInsight como sistema de arquivos padrão.**</span><span class="sxs-lookup"><span data-stu-id="f125d-177">**Use the same Azure Storage account that will be used by the HDInsight cluster as the default file system.**</span></span> <span data-ttu-id="f125d-178">Como o cluster do HDInsight terá a chave de acesso da conta de armazenamento, você não precisará fazer alterações adicionais.</span><span class="sxs-lookup"><span data-stu-id="f125d-178">Because the HDInsight cluster will have the Storage account access key, you don't need to make any additional changes.</span></span>
* <span data-ttu-id="f125d-179">**Use uma conta de armazenamento do Azure diferente do sistema de arquivos padrão do cluster do HDInsight.**</span><span class="sxs-lookup"><span data-stu-id="f125d-179">**Use a different Azure Storage account from the HDInsight cluster default file system.**</span></span> <span data-ttu-id="f125d-180">Se esse for o caso, modifique a parte de criar do script do Windows PowerShell encontrado em [Criar cluster HDInsight e executar trabalhos do Hive/Sqoop](#runjob) para incluir a conta de armazenamento como uma conta de armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="f125d-180">If this is the case, you must modify the creation part of the Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) to link the Storage account as an additional Storage account.</span></span> <span data-ttu-id="f125d-181">Para obter instruções, consulte [Criar clusters do Hadoop no HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="f125d-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="f125d-182">O cluster do HDInsight então conhecerá a chave de acesso da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f125d-182">The HDInsight cluster then knows the access key for the Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="f125d-183">O caminho do armazenamento Blob para o arquivo de dados é embutido em código no arquivo de script do HiveQL.</span><span class="sxs-lookup"><span data-stu-id="f125d-183">The Blob storage path for the data file is hard coded in the HiveQL script file.</span></span> <span data-ttu-id="f125d-184">É necessário atualizá-lo de acordo.</span><span class="sxs-lookup"><span data-stu-id="f125d-184">You must update it accordingly.</span></span>

<span data-ttu-id="f125d-185">**Para baixar os dados de voos**</span><span class="sxs-lookup"><span data-stu-id="f125d-185">**To download the flight data**</span></span>

1. <span data-ttu-id="f125d-186">Navegue para [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span><span class="sxs-lookup"><span data-stu-id="f125d-186">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="f125d-187">Na página, selecione os valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="f125d-187">On the page, select the following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="f125d-188">Nome</span><span class="sxs-lookup"><span data-stu-id="f125d-188">Name</span></span></th><th><span data-ttu-id="f125d-189">Valor</span><span class="sxs-lookup"><span data-stu-id="f125d-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="f125d-190">Filtrar por ano</span><span class="sxs-lookup"><span data-stu-id="f125d-190">Filter Year</span></span></td><td><span data-ttu-id="f125d-191">2013</span><span class="sxs-lookup"><span data-stu-id="f125d-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="f125d-192">Filtrar por período</span><span class="sxs-lookup"><span data-stu-id="f125d-192">Filter Period</span></span></td><td><span data-ttu-id="f125d-193">Janeiro</span><span class="sxs-lookup"><span data-stu-id="f125d-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="f125d-194">Campos</span><span class="sxs-lookup"><span data-stu-id="f125d-194">Fields</span></span></td><td><span data-ttu-id="f125d-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (limpar todos os outros campos)</span><span class="sxs-lookup"><span data-stu-id="f125d-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="f125d-196">
3. Clique em **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="f125d-196">
3. Click **Download**.</span></span>
<span data-ttu-id="f125d-197">4.</span><span class="sxs-lookup"><span data-stu-id="f125d-197">4.</span></span> <span data-ttu-id="f125d-198">Descompacte o arquivo na pasta **C:\Tutorials\FlightDelay\2013Data**.</span><span class="sxs-lookup"><span data-stu-id="f125d-198">Unzip the file to the **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="f125d-199">Cada arquivo é um arquivo CSV e tem aproximadamente 60 GB de tamanho.</span><span class="sxs-lookup"><span data-stu-id="f125d-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="f125d-200">5.</span><span class="sxs-lookup"><span data-stu-id="f125d-200">5.</span></span> <span data-ttu-id="f125d-201">Renomeie o arquivo com o nome do mês ao qual seus dados se referem.</span><span class="sxs-lookup"><span data-stu-id="f125d-201">Rename the file to the name of the month that it contains data for.</span></span> <span data-ttu-id="f125d-202">Por exemplo, o arquivo que contém os dados de janeiro seria nomeado *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="f125d-202">For example, the file containing the January data would be named *January.csv*.</span></span>
<span data-ttu-id="f125d-203">6.</span><span class="sxs-lookup"><span data-stu-id="f125d-203">6.</span></span> <span data-ttu-id="f125d-204">Repita as etapas 2 e 5 para baixar um arquivo para cada um dos 12 meses de 2013.</span><span class="sxs-lookup"><span data-stu-id="f125d-204">Repeat steps 2 and 5 to download a file for each of the 12 months in 2013.</span></span> <span data-ttu-id="f125d-205">Você precisará de pelo menos um arquivo para executar o tutorial.</span><span class="sxs-lookup"><span data-stu-id="f125d-205">You will need a minimum of one file to run the tutorial.</span></span>

<span data-ttu-id="f125d-206">**Para carregar os dados de atraso de voo para o armazenamento de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="f125d-206">**To upload the flight delay data to Azure Blob storage**</span></span>

1. <span data-ttu-id="f125d-207">Prepare os parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f125d-207">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="f125d-208">Nome de variável</span><span class="sxs-lookup"><span data-stu-id="f125d-208">Variable Name</span></span></th><th><span data-ttu-id="f125d-209">Observações</span><span class="sxs-lookup"><span data-stu-id="f125d-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="f125d-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="f125d-210">$storageAccountName</span></span></td><td><span data-ttu-id="f125d-211">A conta de armazenamento do Azure para a qual você deseja carregar os dados.</span><span class="sxs-lookup"><span data-stu-id="f125d-211">The Azure Storage account where you want to upload the data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="f125d-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="f125d-212">$blobContainerName</span></span></td><td><span data-ttu-id="f125d-213">O contêiner de Blob para o qual você deseja carregar os dados.</span><span class="sxs-lookup"><span data-stu-id="f125d-213">The Blob container where you want to upload the data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="f125d-214">Abra o ISE do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="f125d-215">3.</span><span class="sxs-lookup"><span data-stu-id="f125d-215">3.</span></span> <span data-ttu-id="f125d-216">Cole o seguinte script no painel de script:</span><span class="sxs-lookup"><span data-stu-id="f125d-216">Paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure storage account name for creating a new HDInsight cluster. If the account doesn't exist, the script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure blob container name for creating a new HDInsight cluster. If not specified, the HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # The source folder
    $destFolder = "tutorials/flightdelay/2013data"     #The blob name prefix for the files to be uploaded
    #EndRegion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating the Azure Storage account and the Blob container..." -ForegroundColor Green
    # Validate the Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "The storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate the container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "The Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy the file from local workstation to Azure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName to $blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "The source folder on the workstation doesn't exist" -ForegroundColor Red
    }

    # List the uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="f125d-217">Pressione **F5** para executar o script.</span><span class="sxs-lookup"><span data-stu-id="f125d-217">Press **F5** to run the script.</span></span>

<span data-ttu-id="f125d-218">Se você optar por usar um método diferente para carregar os arquivos, verifique se o caminho do arquivo é tutorials/flightdelay/data.</span><span class="sxs-lookup"><span data-stu-id="f125d-218">If you choose to use a different method for uploading the files, please make sure the file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="f125d-219">A sintaxe para acessar os arquivos é:</span><span class="sxs-lookup"><span data-stu-id="f125d-219">The syntax for accessing the files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="f125d-220">O caminho tutorials/flightdelay/data é a pasta virtual que você criou quando carregou os arquivos.</span><span class="sxs-lookup"><span data-stu-id="f125d-220">The path tutorials/flightdelay/data is the virtual folder you created when you uploaded the files.</span></span> <span data-ttu-id="f125d-221">Verifique se há 12 arquivos, um para cada mês.</span><span class="sxs-lookup"><span data-stu-id="f125d-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="f125d-222">Você precisa atualizar a consulta do Hive para ler por meio do novo local.</span><span class="sxs-lookup"><span data-stu-id="f125d-222">You must update the Hive query to read from the new location.</span></span>
>
> <span data-ttu-id="f125d-223">Você precisa configurar a permissão de acesso do contêiner para ser pública ou para associar a conta de armazenamento ao cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f125d-223">You must either configure the container access permission to be public or bind the Storage account to the HDInsight cluster.</span></span> <span data-ttu-id="f125d-224">Caso contrário, a cadeia de consulta do Hive não conseguirá acessar os arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="f125d-224">Otherwise, the Hive query string will not be able to access the data files.</span></span>

- - -

## <span data-ttu-id="f125d-225"><a id="appendix-b"></a>Apêndice B - Criar e carregar o script HiveQL</span><span class="sxs-lookup"><span data-stu-id="f125d-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="f125d-226">Usando o PowerShell do Azure, você pode executar várias instruções HiveQL uma por vez ou empacotar a instrução HiveQL em um arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="f125d-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="f125d-227">Esta seção mostra como criar um script HiveQL e carregá-lo no armazenamento de Blob do Azure usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-227">This section shows you how to create a HiveQL script and upload the script to Azure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="f125d-228">O Hive exige que os scripts de HiveQL sejam armazenados no armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-228">Hive requires the HiveQL scripts to be stored in Azure Blob storage.</span></span>

<span data-ttu-id="f125d-229">O script HiveQL executará o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f125d-229">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="f125d-230">**Remova a tabela delays_raw**, caso a tabela já exista.</span><span class="sxs-lookup"><span data-stu-id="f125d-230">**Drop the delays_raw table**, in case the table already exists.</span></span>
2. <span data-ttu-id="f125d-231">**Crie a tabela externa do Hive delays_raw** apontando para a localização do Armazenamento de Blobs com os arquivos de atraso de voo.</span><span class="sxs-lookup"><span data-stu-id="f125d-231">**Create the delays_raw external Hive table** pointing to the Blob storage location with the flight delay files.</span></span> <span data-ttu-id="f125d-232">Esta consulta especifica que os campos são delimitados por "," e que as linhas são finalizadas por "\n".</span><span class="sxs-lookup"><span data-stu-id="f125d-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="f125d-233">Isso representa um problema quando os valores dos campos contêm vírgulas porque o Hive não pode diferenciar entre uma vírgula, que é um campo delimitado, e uma que faz parte de um valor do campo (que é o caso nos valores de campo de ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span><span class="sxs-lookup"><span data-stu-id="f125d-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is the case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="f125d-234">Para resolver isso, a consulta cria colunas TEMP para bloquear dados que estão divididos incorretamente em colunas.</span><span class="sxs-lookup"><span data-stu-id="f125d-234">To address this, the query creates TEMP columns to hold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="f125d-235">**Remova a tabela de atrasos**, caso a tabela já exista.</span><span class="sxs-lookup"><span data-stu-id="f125d-235">**Drop the delays table**, in case the table already exists.</span></span>
4. <span data-ttu-id="f125d-236">**Crie a tabela de atrasos**.</span><span class="sxs-lookup"><span data-stu-id="f125d-236">**Create the delays table**.</span></span> <span data-ttu-id="f125d-237">É útil limpar os dados antes de continuar o processamento.</span><span class="sxs-lookup"><span data-stu-id="f125d-237">It is helpful to clean up the data before further processing.</span></span> <span data-ttu-id="f125d-238">Esta consulta cria uma nova tabela, *delays* por meio da tabela delays_raw.</span><span class="sxs-lookup"><span data-stu-id="f125d-238">This query creates a new table, *delays*, from the delays_raw table.</span></span> <span data-ttu-id="f125d-239">Observe que as colunas TEMP (conforme mencionado anteriormente) não são copiadas e que a função **substring** é usada para remover marcas de aspas dos dados.</span><span class="sxs-lookup"><span data-stu-id="f125d-239">Note that the TEMP columns (as mentioned previously) are not copied, and that the **substring** function is used to remove quotation marks from the data.</span></span>
5. <span data-ttu-id="f125d-240">**Calcula a média de atraso de tempo e agrupa os resultados por nome de cidade.**</span><span class="sxs-lookup"><span data-stu-id="f125d-240">**Compute the average weather delay and groups the results by city name.**</span></span> <span data-ttu-id="f125d-241">Ela também produzirá os resultados para o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="f125d-241">It will also output the results to Blob storage.</span></span> <span data-ttu-id="f125d-242">Observe que a consulta removerá apóstrofos dos dados e excluirá linhas em que o valor de **weather_delay** é nulo.</span><span class="sxs-lookup"><span data-stu-id="f125d-242">Note that the query will remove apostrophes from the data and will exclude rows where the value for **weather_delay** is null.</span></span> <span data-ttu-id="f125d-243">Isso é necessário porque o Sqoop, usado mais adiante neste tutorial, não trata desses valores normalmente por padrão.</span><span class="sxs-lookup"><span data-stu-id="f125d-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="f125d-244">Para obter uma lista completa dos comandos HiveQL, consulte [Linguagem de Definição de Dados do Hive][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="f125d-244">For a full list of the HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="f125d-245">Cada comando HiveQL deve terminar com um ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="f125d-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="f125d-246">**Para criar um arquivo de script HiveQL**</span><span class="sxs-lookup"><span data-stu-id="f125d-246">**To create a HiveQL script file**</span></span>

1. <span data-ttu-id="f125d-247">Prepare os parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f125d-247">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="f125d-248">Nome de variável</span><span class="sxs-lookup"><span data-stu-id="f125d-248">Variable Name</span></span></th><th><span data-ttu-id="f125d-249">Observações</span><span class="sxs-lookup"><span data-stu-id="f125d-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="f125d-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="f125d-250">$storageAccountName</span></span></td><td><span data-ttu-id="f125d-251">A conta de armazenamento do Azure para a qual você deseja carregar o script do HiveQL.</span><span class="sxs-lookup"><span data-stu-id="f125d-251">The Azure Storage account where you want to upload the HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="f125d-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="f125d-252">$blobContainerName</span></span></td><td><span data-ttu-id="f125d-253">O contêiner de Blob para o qual você deseja carregar o script do HiveQL.</span><span class="sxs-lookup"><span data-stu-id="f125d-253">The Blob container where you want to upload the HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="f125d-254">Abra o ISE do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="f125d-255">3.</span><span class="sxs-lookup"><span data-stu-id="f125d-255">3.</span></span> <span data-ttu-id="f125d-256">Copie e cole o seguinte script no painel de script:</span><span class="sxs-lookup"><span data-stu-id="f125d-256">Copy and paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure storage account name for creating a new HDInsight cluster. If the account doesn't exist, the script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter the Azure blob container name for creating a new HDInsight cluster. If not specified, the HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # The HiveQL script file is exported as this file before it's uploaded to Blob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # The HiveQL script file will be uploaded to Blob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by the HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating the Azure Storage account and the Blob container..." -ForegroundColor Green
    # Validate the Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "The storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate the container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "The Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate the file and file path

    # Check if a file with the same file name already exists on the workstation
    Write-Host "`nvalidating the folder structure on the workstation for saving the HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'The file, ' $hqlLocalFileName ', exists.  Do you want to overwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create the folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write the Hive script into a local file
    Write-Host "`nWriting the Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload the Hive script to the default Blob container
    Write-Host "`nUploading the Hive script to the default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload the file from local workstation to Blob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of the PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="f125d-257">A seguir estão as variáveis usadas no script:</span><span class="sxs-lookup"><span data-stu-id="f125d-257">Here are the variables used in the script:</span></span>

   * <span data-ttu-id="f125d-258">**$hqlLocalFileName** - o script salva o arquivo de script HiveQL localmente antes de carregá-lo no armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="f125d-258">**$hqlLocalFileName** - The script saves the HiveQL script file locally before uploading it to Blob storage.</span></span> <span data-ttu-id="f125d-259">Esse é o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="f125d-259">This is the file name.</span></span> <span data-ttu-id="f125d-260">O valor padrão é <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="f125d-260">The default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="f125d-261">**$hqlBlobName** - Esse é o nome do blob do arquivo de script HiveQL usado no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-261">**$hqlBlobName** - This is the HiveQL script file blob name used in the Azure Blob storage.</span></span> <span data-ttu-id="f125d-262">O valor padrão é C:tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="f125d-262">The default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="f125d-263">Como o arquivo será escrito diretamente no armazenamento de Blobs do Azure, NÃO há "/" no início do nome do blob.</span><span class="sxs-lookup"><span data-stu-id="f125d-263">Because the file will be written directly to Azure Blob storage, there is NOT a "/" at the beginning of the blob name.</span></span> <span data-ttu-id="f125d-264">Se você quiser acessar o arquivo por meio do armazenamento de Blob, precisará adicionar uma "/" no início do nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="f125d-264">If you want to access the file from Blob storage, you will need to add a "/" at the beginning of the file name.</span></span>
   * <span data-ttu-id="f125d-265">**$srcDataFolder** e **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="f125d-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="f125d-266"><a id="appendix-c"></a>Apêndice C - Preparar o banco de dados SQL do Azure para a saída do trabalho do Sqoop</span><span class="sxs-lookup"><span data-stu-id="f125d-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for the Sqoop job output</span></span>
<span data-ttu-id="f125d-267">**Para preparar o Banco de Dados SQL (mescle o script do Sqoop a este)**</span><span class="sxs-lookup"><span data-stu-id="f125d-267">**To prepare the SQL database (merge this with the Sqoop script)**</span></span>

1. <span data-ttu-id="f125d-268">Prepare os parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f125d-268">Prepare the parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="f125d-269">Nome de variável</span><span class="sxs-lookup"><span data-stu-id="f125d-269">Variable Name</span></span></th><th><span data-ttu-id="f125d-270">Observações</span><span class="sxs-lookup"><span data-stu-id="f125d-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="f125d-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="f125d-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="f125d-272">O nome do servidor de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-272">The name of the Azure SQL database server.</span></span> <span data-ttu-id="f125d-273">Não insira nada para criar um novo servidor.</span><span class="sxs-lookup"><span data-stu-id="f125d-273">Enter nothing to create a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="f125d-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="f125d-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="f125d-275">O nome de logon para o servidor de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-275">The login name for the Azure SQL database server.</span></span> <span data-ttu-id="f125d-276">Se $sqlDatabaseServerName for um servidor existente, o logon e a senha de logon serão usados para autenticação no servidor.</span><span class="sxs-lookup"><span data-stu-id="f125d-276">If $sqlDatabaseServerName is an existing server, the login and login password are used to authenticate with the server.</span></span> <span data-ttu-id="f125d-277">Caso contrário, eles serão usados para criar um novo servidor.</span><span class="sxs-lookup"><span data-stu-id="f125d-277">Otherwise they are used to create a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="f125d-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="f125d-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="f125d-279">A senha de logon para o servidor de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-279">The login password for the Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="f125d-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="f125d-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="f125d-281">Esse valor é usado somente quando você estiver criando um novo servidor de banco de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="f125d-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="f125d-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="f125d-283">O banco de dados SQL usado para criar a tabela AvgDelays para o trabalho do Sqoop.</span><span class="sxs-lookup"><span data-stu-id="f125d-283">The SQL database used to create the AvgDelays table for the Sqoop job.</span></span> <span data-ttu-id="f125d-284">Deixar em branco criará um banco de dados chamado HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="f125d-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="f125d-285">O nome da tabela para a saída do trabalho Sqoop é AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="f125d-285">The table name for the Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="f125d-286">Abra o ISE do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="f125d-287">3.</span><span class="sxs-lookup"><span data-stu-id="f125d-287">3.</span></span> <span data-ttu-id="f125d-288">Copie e cole o seguinte script no painel de script:</span><span class="sxs-lookup"><span data-stu-id="f125d-288">Copy and paste the following script into the script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter the region to create the Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter the database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify the database name if you have one created. Otherwise use "" to have the script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #To allow other Azure services to access the server add a firewall rule and set both the StartIpAddress and EndIpAddress to 0.0.0.0. Note that this allows Azure traffic from any Azure subscription to access the server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command to create the AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of the PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="f125d-289">O script usa um serviço de transferência de estado representacional REST, http://bot.whatismyipaddress.com, para recuperar seu endereço IP externo.</span><span class="sxs-lookup"><span data-stu-id="f125d-289">The script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, to retrieve your external IP address.</span></span> <span data-ttu-id="f125d-290">O endereço IP é usado para criar uma regra de firewall para seu servidor do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f125d-290">The IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="f125d-291">A seguir estão algumas das variáveis usadas no script:</span><span class="sxs-lookup"><span data-stu-id="f125d-291">Here are some variables used in the script:</span></span>

   * <span data-ttu-id="f125d-292">**$ipAddressRestService** – O valor padrão é http://bot.whatismyipaddress.com.</span><span class="sxs-lookup"><span data-stu-id="f125d-292">**$ipAddressRestService** - The default value is http://bot.whatismyipaddress.com.</span></span> <span data-ttu-id="f125d-293">Trata-se de um serviço REST de endereço IP público para obter seu endereço IP externo.</span><span class="sxs-lookup"><span data-stu-id="f125d-293">It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="f125d-294">Você pode usar outros serviços se desejar.</span><span class="sxs-lookup"><span data-stu-id="f125d-294">You can use other services if you want.</span></span> <span data-ttu-id="f125d-295">O endereço IP externo recuperado por meio do serviço será usado para criar uma regra de firewall para seu servidor do banco de dados SQL do Azure, para que você possa acessar o banco de dados por meio da estação de trabalho (usando o script do Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="f125d-295">The external IP address retrieved through the service will be used to create a firewall rule for your Azure SQL database server, so that you can access the database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="f125d-296">**$fireWallRuleName** - esse é o nome da regra de firewall para o servidor de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-296">**$fireWallRuleName** - This is the name of the firewall rule for the Azure SQL database server.</span></span> <span data-ttu-id="f125d-297">O nome padrão é <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="f125d-297">The default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="f125d-298">Você pode renomeá-lo se desejar.</span><span class="sxs-lookup"><span data-stu-id="f125d-298">You can rename it if you want.</span></span>
   * <span data-ttu-id="f125d-299">**$sqlDatabaseMaxSizeGB** - Esse valor é usado apenas ao criar um novo servidor de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-299">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="f125d-300">O valor padrão é 10GB.</span><span class="sxs-lookup"><span data-stu-id="f125d-300">The default value is 10GB.</span></span> <span data-ttu-id="f125d-301">10GB são suficientes para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="f125d-301">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="f125d-302">**$sqlDatabaseName** - Esse valor é usado apenas ao criar um novo banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-302">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="f125d-303">O valor padrão é HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="f125d-303">The default value is HDISqoop.</span></span> <span data-ttu-id="f125d-304">Se você renomeá-lo, deverá atualizar o script do Windows PowerShell do Sqoop de acordo.</span><span class="sxs-lookup"><span data-stu-id="f125d-304">If you rename it, you must update the Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="f125d-305">Pressione **F5** para executar o script.</span><span class="sxs-lookup"><span data-stu-id="f125d-305">Press **F5** to run the script.</span></span>
5. <span data-ttu-id="f125d-306">Valide a saída do script.</span><span class="sxs-lookup"><span data-stu-id="f125d-306">Validate the script output.</span></span> <span data-ttu-id="f125d-307">Tenha certeza de que o script foi executado com sucesso.</span><span class="sxs-lookup"><span data-stu-id="f125d-307">Make sure the script ran successfully.</span></span>

## <span data-ttu-id="f125d-308"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f125d-308"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="f125d-309">Agora você compreende como carregar um arquivo para o armazenamento de Blob do Azure, como preencher uma tabela Hive usando os dados do armazenamento de Blob do Azure, como executar consultas do Hive e como usar o Sqoop para exportar dados do HDFS para o banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f125d-309">Now you understand how to upload a file to Azure Blob storage, how to populate a Hive table by using the data from Azure Blob storage, how to run Hive queries, and how to use Sqoop to export data from HDFS to an Azure SQL database.</span></span> <span data-ttu-id="f125d-310">Para saber mais, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="f125d-310">To learn more, see the following articles:</span></span>

* <span data-ttu-id="f125d-311">[Introdução ao HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f125d-311">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="f125d-312">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="f125d-312">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="f125d-313">[Usar o Oozie com o HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="f125d-313">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="f125d-314">[Use o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="f125d-314">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="f125d-315">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="f125d-315">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="f125d-316">[Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="f125d-316">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
