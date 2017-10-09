---
title: dados de atraso de voo aaaAnalyze com Hadoop no HDInsight - Azure | Microsoft Docs
description: Saiba como toouse um Windows PowerShell script toocreate um cluster HDInsight, execute um trabalho de Hive, execute um trabalho de Sqoop e excluir o cluster hello.
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
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a><span data-ttu-id="afa33-103">Analisar dados de atraso de voo usando o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="afa33-103">Analyze flight delay data by using Hive in HDInsight</span></span>
<span data-ttu-id="afa33-104">O Hive fornece um meio para executar trabalhos MapReduce do Hadoop por meio de uma linguagem de script semelhante à SQL, chamada *[HiveQL][hadoop-hiveql]*, que pode ser aplicada para resumo, consulta e análise de grandes volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="afa33-104">Hive provides a means of running Hadoop MapReduce jobs through an SQL-like scripting language called *[HiveQL][hadoop-hiveql]*, which can be applied towards summarizing, querying, and analyzing large volumes of data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afa33-105">Olá, as etapas neste documento exigem um cluster HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="afa33-105">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="afa33-106">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="afa33-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="afa33-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="afa33-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="afa33-108">Para conhecer as etapas que funcionam em um cluster baseado em Linux, confira [Analisar dados de atraso de voos usando o Hive no HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="afa33-108">For steps that work with a Linux-based cluster, see [Analyze flight delay data by using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).</span></span>

<span data-ttu-id="afa33-109">Um dos principais benefícios de saudação do HDInsight do Azure é a separação de saudação de computação e armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="afa33-109">One of hello major benefits of Azure HDInsight is hello separation of data storage and compute.</span></span> <span data-ttu-id="afa33-110">O HDInsight usa o armazenamento de blob do Azure para o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="afa33-110">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="afa33-111">Um trabalho típico envolve três partes:</span><span class="sxs-lookup"><span data-stu-id="afa33-111">A typical job involves three parts:</span></span>

1. <span data-ttu-id="afa33-112">**Armazenamento de dados no repositório de blob do Azure.**</span><span class="sxs-lookup"><span data-stu-id="afa33-112">**Store data in Azure Blob storage.**</span></span>  <span data-ttu-id="afa33-113">Por exemplo, os dados climáticos, dados do sensor, logs da Web e, nesse caso, os dados de atraso do voo são salvos no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-113">For example, weather data, sensor data, web logs, and in this case, flight delay data are saved into Azure Blob storage.</span></span>
2. <span data-ttu-id="afa33-114">**Executar trabalhos.**</span><span class="sxs-lookup"><span data-stu-id="afa33-114">**Run jobs.**</span></span> <span data-ttu-id="afa33-115">Quando dados de saudação do tempo tooprocess, executar um script do Windows PowerShell (ou um aplicativo cliente) toocreate um cluster HDInsight, executar trabalhos e excluir o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-115">When it is time tooprocess hello data, you run a Windows PowerShell script (or a client application) toocreate an HDInsight cluster, run jobs, and delete hello cluster.</span></span> <span data-ttu-id="afa33-116">Olá trabalhos salvar dados de saída tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="afa33-116">hello jobs save output data tooAzure Blob storage.</span></span> <span data-ttu-id="afa33-117">dados de saída de saudação são retidos até mesmo depois Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="afa33-117">hello output data is retained even after hello cluster is deleted.</span></span> <span data-ttu-id="afa33-118">Dessa forma, você só paga pelo que consumiu.</span><span class="sxs-lookup"><span data-stu-id="afa33-118">This way, you pay for only what you have consumed.</span></span>
3. <span data-ttu-id="afa33-119">**Recuperar a saída de saudação do armazenamento de BLOBs do Azure**, ou neste tutorial, exportar o banco de dados do SQL Azure tooan Olá dados.</span><span class="sxs-lookup"><span data-stu-id="afa33-119">**Retrieve hello output from Azure Blob storage**, or in this tutorial, export hello data tooan Azure SQL database.</span></span>

<span data-ttu-id="afa33-120">Olá diagrama a seguir ilustra o cenário de saudação e a estrutura de saudação deste tutorial:</span><span class="sxs-lookup"><span data-stu-id="afa33-120">hello following diagram illustrates hello scenario and hello structure of this tutorial:</span></span>

![HDI.FlightDelays.flow][img-hdi-flightdelays-flow]

<span data-ttu-id="afa33-122">Observe que Olá números no diagrama Olá correspondem toohello títulos de seção.</span><span class="sxs-lookup"><span data-stu-id="afa33-122">Note that hello numbers in hello diagram correspond toohello section titles.</span></span> <span data-ttu-id="afa33-123">**M** significa o processo principal hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-123">**M** stands for hello main process.</span></span> <span data-ttu-id="afa33-124">**Um** representa o conteúdo de saudação apêndice hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-124">**A** stands for hello content in hello appendix.</span></span>

<span data-ttu-id="afa33-125">a parte principal Olá tutorial Olá mostra como as tarefas de toouse um Windows PowerShell script tooperform Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="afa33-125">hello main portion of hello tutorial shows you how toouse one Windows PowerShell script tooperform hello following tasks:</span></span>

* <span data-ttu-id="afa33-126">Crie um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="afa33-126">Create an HDInsight cluster.</span></span>
* <span data-ttu-id="afa33-127">Execute um trabalho de Hive em atrasos de médio Olá cluster toocalculate em aeroportos.</span><span class="sxs-lookup"><span data-stu-id="afa33-127">Run a Hive job on hello cluster toocalculate average delays at airports.</span></span> <span data-ttu-id="afa33-128">dados de atraso de voo Olá são armazenados em uma conta de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-128">hello flight delay data is stored in an Azure Blob storage account.</span></span>
* <span data-ttu-id="afa33-129">Execute um Sqoop trabalho tooexport Olá Hive trabalho saída tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="afa33-129">Run a Sqoop job tooexport hello Hive job output tooan Azure SQL database.</span></span>
* <span data-ttu-id="afa33-130">Exclua cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-130">Delete hello HDInsight cluster.</span></span>

<span data-ttu-id="afa33-131">Apêndices Olá, você encontrará instruções Olá para carregar dados de atraso de voo, criação/carregamento de uma cadeia de caracteres de consulta de Hive e preparando o banco de dados do SQL Azure Olá para o trabalho de Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-131">In hello appendixes, you can find hello instructions for uploading flight delay data, creating/uploading a Hive query string, and preparing hello Azure SQL database for hello Sqoop job.</span></span>

> [!NOTE]
> <span data-ttu-id="afa33-132">etapas de saudação neste documento são específicas com base em tooWindows clusters de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="afa33-132">hello steps in this document are specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="afa33-133">Para conhecer as etapas que funcionam em um cluster baseado em Linux, confira [Analisar dados de atraso de voos usando o Hive no HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span><span class="sxs-lookup"><span data-stu-id="afa33-133">For steps that work with a Linux-based cluster, see [Analyze flight delay data using Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)</span></span>

### <a name="prerequisites"></a><span data-ttu-id="afa33-134">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="afa33-134">Prerequisites</span></span>
<span data-ttu-id="afa33-135">Antes de começar este tutorial, você deve ter Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="afa33-135">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="afa33-136">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="afa33-136">**An Azure subscription**.</span></span> <span data-ttu-id="afa33-137">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="afa33-137">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="afa33-138">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="afa33-138">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="afa33-139">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="afa33-139">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="afa33-140">Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-140">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="afa33-141">Siga as etapas de saudação em [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Olá última versão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-141">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="afa33-142">Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="afa33-142">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

<span data-ttu-id="afa33-143">**Arquivos usados neste tutorial**</span><span class="sxs-lookup"><span data-stu-id="afa33-143">**Files used in this tutorial**</span></span>

<span data-ttu-id="afa33-144">Este tutorial usa Olá pontualidade de dados de voo aérea de [pesquisa e administração de tecnologia inovadora, agência de transporte estatísticas ou RITA][rita-website].</span><span class="sxs-lookup"><span data-stu-id="afa33-144">This tutorial uses hello on-time performance of airline flight data from [Research and Innovative Technology Administration, Bureau of Transportation Statistics or RITA][rita-website].</span></span>
<span data-ttu-id="afa33-145">Uma cópia da saudação dados foram carregados tooan contêiner de armazenamento de BLOBs do Azure com permissão de acesso de Blob público hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-145">A copy of hello data has been uploaded tooan Azure Blob storage container with hello Public Blob access permission.</span></span>
<span data-ttu-id="afa33-146">Uma parte do script do PowerShell copia dados de saudação de Olá contêiner toohello padrão blob contêiner de blob público do seu cluster.</span><span class="sxs-lookup"><span data-stu-id="afa33-146">A part of your PowerShell script copies hello data from hello public blob container toohello default blob container of your cluster.</span></span> <span data-ttu-id="afa33-147">Olá HiveQL script também está copiado toohello mesmo contêiner de Blob.</span><span class="sxs-lookup"><span data-stu-id="afa33-147">hello HiveQL script is also copied toohello same Blob container.</span></span>
<span data-ttu-id="afa33-148">Se você quiser toolearn como tooget/carregar Olá dados tooyour possui conta de armazenamento e como toocreate/carregar Olá HiveQL scripts de arquivo, consulte [Apêndice A](#appendix-a) e [Apêndice B](#appendix-b).</span><span class="sxs-lookup"><span data-stu-id="afa33-148">If you want toolearn how tooget/upload hello data tooyour own Storage account, and how toocreate/upload hello HiveQL script file, see [Appendix A](#appendix-a) and [Appendix B](#appendix-b).</span></span>

<span data-ttu-id="afa33-149">Olá tabela a seguir lista os arquivos de saudação usados neste tutorial:</span><span class="sxs-lookup"><span data-stu-id="afa33-149">hello following table lists hello files used in this tutorial:</span></span>

<table border="1">
<tr><th><span data-ttu-id="afa33-150">Arquivos</span><span class="sxs-lookup"><span data-stu-id="afa33-150">Files</span></span></th><th><span data-ttu-id="afa33-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="afa33-151">Description</span></span></th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td><span data-ttu-id="afa33-152">arquivo de script HiveQL Olá usado por Olá trabalho de Hive.</span><span class="sxs-lookup"><span data-stu-id="afa33-152">hello HiveQL script file used by hello Hive job.</span></span> <span data-ttu-id="afa33-153">Esse script foi carregada tooan conta de armazenamento de BLOBs do Azure com acesso público de saudação.</span><span class="sxs-lookup"><span data-stu-id="afa33-153">This script has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="afa33-154"><a href="#appendix-b">Apêndice B</a> tem instruções sobre como preparar e carregar esta conta de armazenamento de BLOBs do Azure própria do arquivo tooyour.</span><span class="sxs-lookup"><span data-stu-id="afa33-154"><a href="#appendix-b">Appendix B</a> has instructions on preparing and uploading this file tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td><span data-ttu-id="afa33-155">Dados de entrada para o trabalho de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-155">Input data for hello Hive job.</span></span> <span data-ttu-id="afa33-156">dados de saudação foi carregado tooan conta de armazenamento de BLOBs do Azure com acesso público de saudação.</span><span class="sxs-lookup"><span data-stu-id="afa33-156">hello data has been uploaded tooan Azure Blob storage account with hello public access.</span></span> <span data-ttu-id="afa33-157"><a href="#appendix-a">Apêndice A</a> tem instruções sobre obter dados de saudação e carregar a conta de armazenamento do hello dados tooyour própria BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-157"><a href="#appendix-a">Appendix A</a> has instructions on getting hello data and uploading hello data tooyour own Azure Blob storage account.</span></span></td></tr>
<tr><td><span data-ttu-id="afa33-158">\tutorials\flightdelays\output</span><span class="sxs-lookup"><span data-stu-id="afa33-158">\tutorials\flightdelays\output</span></span></td><td><span data-ttu-id="afa33-159">Olá o caminho de saída para o trabalho de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-159">hello output path for hello Hive job.</span></span> <span data-ttu-id="afa33-160">contêiner padrão de saudação é usado para armazenar dados de saída de saudação.</span><span class="sxs-lookup"><span data-stu-id="afa33-160">hello default container is used for storing hello output data.</span></span></td></tr>
<tr><td><span data-ttu-id="afa33-161">\tutorials\flightdelays\jobstatus</span><span class="sxs-lookup"><span data-stu-id="afa33-161">\tutorials\flightdelays\jobstatus</span></span></td><td><span data-ttu-id="afa33-162">Olá Hive trabalho status pasta no contêiner de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="afa33-162">hello Hive job status folder on hello default container.</span></span></td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a><span data-ttu-id="afa33-163">Criar cluster e executar trabalhos do Hive/Sqoop</span><span class="sxs-lookup"><span data-stu-id="afa33-163">Create cluster and run Hive/Sqoop jobs</span></span>
<span data-ttu-id="afa33-164">O MapReduce do Hadoop é um processamento em lote.</span><span class="sxs-lookup"><span data-stu-id="afa33-164">Hadoop MapReduce is batch processing.</span></span> <span data-ttu-id="afa33-165">Olá toorun de maneira econômica mais um trabalho de Hive é toocreate um cluster para o trabalho de saudação e excluir trabalho Olá depois Olá trabalho for concluído.</span><span class="sxs-lookup"><span data-stu-id="afa33-165">hello most cost-effective way toorun a Hive job is toocreate a cluster for hello job, and delete hello job after hello job is completed.</span></span> <span data-ttu-id="afa33-166">Olá script a seguir abrange todo o processo hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-166">hello following script covers hello whole process.</span></span>
<span data-ttu-id="afa33-167">Para obter mais informações sobre como criar um cluster HDInsight e executar trabalhos do Hive, consulte [Criar clusters do Hadoop no HDInsight][hdinsight-provision] e [Usar o Hive com o HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="afa33-167">For more information on creating an HDInsight cluster and running Hive jobs, see [Create Hadoop clusters in HDInsight][hdinsight-provision] and [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

<span data-ttu-id="afa33-168">**consultas de Hive Olá toorun do PowerShell do Azure**</span><span class="sxs-lookup"><span data-stu-id="afa33-168">**toorun hello Hive queries by Azure PowerShell**</span></span>

1. <span data-ttu-id="afa33-169">Criar uma tabela de banco de dados e hello do SQL Azure para saída de trabalho de Sqoop hello usando instruções Olá [Apêndice C](#appendix-c).</span><span class="sxs-lookup"><span data-stu-id="afa33-169">Create an Azure SQL database and hello table for hello Sqoop job output by using hello instructions in [Appendix C](#appendix-c).</span></span>
2. <span data-ttu-id="afa33-170">Abra o Windows PowerShell ISE e execute Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="afa33-170">Open Windows PowerShell ISE, and run hello following script:</span></span>

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

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

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

    # Create hello HDInsight cluster
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
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
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
    # Submit hello Sqoop job
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
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. <span data-ttu-id="afa33-171">Conectar-se o banco de dados SQL tooyour e consulte atrasos de voo médio por cidade na tabela de AvgDelays hello:</span><span class="sxs-lookup"><span data-stu-id="afa33-171">Connect tooyour SQL database and see average flight delays by city in hello AvgDelays table:</span></span>

    ![HDI.FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <span data-ttu-id="afa33-173"><a id="appendix-a"></a>Apêndice A - carregamento voo atraso dados tooAzure armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="afa33-173"><a id="appendix-a"></a>Appendix A - Upload flight delay data tooAzure Blob storage</span></span>
<span data-ttu-id="afa33-174">Carregar arquivo de dados hello e arquivos de script HiveQL hello (consulte [Apêndice B](#appendix-b)) requer um planejamento.</span><span class="sxs-lookup"><span data-stu-id="afa33-174">Uploading hello data file and hello HiveQL script files (see [Appendix B](#appendix-b)) requires some planning.</span></span> <span data-ttu-id="afa33-175">ideia Olá é toostore arquivos de dados de saudação e arquivo de HiveQL de saudação antes de criar um cluster HDInsight e executando o trabalho de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-175">hello idea is toostore hello data files and hello HiveQL file before creating an HDInsight cluster and running hello Hive job.</span></span> <span data-ttu-id="afa33-176">Você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="afa33-176">You have two options:</span></span>

* <span data-ttu-id="afa33-177">**Use Olá a mesma conta de armazenamento do Azure que será usada pelo cluster do HDInsight hello como sistema de arquivos padrão de saudação.**</span><span class="sxs-lookup"><span data-stu-id="afa33-177">**Use hello same Azure Storage account that will be used by hello HDInsight cluster as hello default file system.**</span></span> <span data-ttu-id="afa33-178">Porque o cluster do HDInsight Olá terá chave de acesso da conta de armazenamento hello, você não precisa toomake qualquer alteração adicional.</span><span class="sxs-lookup"><span data-stu-id="afa33-178">Because hello HDInsight cluster will have hello Storage account access key, you don't need toomake any additional changes.</span></span>
* <span data-ttu-id="afa33-179">**Use uma conta de armazenamento do Azure diferente de saudação sistema de arquivos de padrão de cluster HDInsight.**</span><span class="sxs-lookup"><span data-stu-id="afa33-179">**Use a different Azure Storage account from hello HDInsight cluster default file system.**</span></span> <span data-ttu-id="afa33-180">Se esse for o caso de Olá, você deve modificar a parte de criação de saudação do hello Windows PowerShell script encontrado no [cluster HDInsight criar e executados trabalhos de Hive/Sqoop](#runjob) toolink Olá conta de armazenamento como uma conta de armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="afa33-180">If this is hello case, you must modify hello creation part of hello Windows PowerShell script found in [Create HDInsight cluster and run Hive/Sqoop jobs](#runjob) toolink hello Storage account as an additional Storage account.</span></span> <span data-ttu-id="afa33-181">Para obter instruções, consulte [Criar clusters do Hadoop no HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="afa33-181">For instructions, see [Create Hadoop clusters in HDInsight][hdinsight-provision].</span></span> <span data-ttu-id="afa33-182">cluster do HDInsight Olá sabe, em seguida, chave de acesso de saudação de saudação conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="afa33-182">hello HDInsight cluster then knows hello access key for hello Storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="afa33-183">caminho de armazenamento de Blob Olá para Olá arquivo de dados é codificado no arquivo de script hello HiveQL.</span><span class="sxs-lookup"><span data-stu-id="afa33-183">hello Blob storage path for hello data file is hard coded in hello HiveQL script file.</span></span> <span data-ttu-id="afa33-184">É necessário atualizá-lo de acordo.</span><span class="sxs-lookup"><span data-stu-id="afa33-184">You must update it accordingly.</span></span>

<span data-ttu-id="afa33-185">**dados de voo Olá toodownload**</span><span class="sxs-lookup"><span data-stu-id="afa33-185">**toodownload hello flight data**</span></span>

1. <span data-ttu-id="afa33-186">Procurar muito[pesquisa e administração de tecnologia inovadora, agência de transporte estatísticas][rita-website].</span><span class="sxs-lookup"><span data-stu-id="afa33-186">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>
2. <span data-ttu-id="afa33-187">Na página de saudação, selecione Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="afa33-187">On hello page, select hello following values:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="afa33-188">Nome</span><span class="sxs-lookup"><span data-stu-id="afa33-188">Name</span></span></th><th><span data-ttu-id="afa33-189">Valor</span><span class="sxs-lookup"><span data-stu-id="afa33-189">Value</span></span></th></tr>
    <tr><td><span data-ttu-id="afa33-190">Filtrar por ano</span><span class="sxs-lookup"><span data-stu-id="afa33-190">Filter Year</span></span></td><td><span data-ttu-id="afa33-191">2013</span><span class="sxs-lookup"><span data-stu-id="afa33-191">2013</span></span> </td></tr>
    <tr><td><span data-ttu-id="afa33-192">Filtrar por período</span><span class="sxs-lookup"><span data-stu-id="afa33-192">Filter Period</span></span></td><td><span data-ttu-id="afa33-193">Janeiro</span><span class="sxs-lookup"><span data-stu-id="afa33-193">January</span></span></td></tr>
    <tr><td><span data-ttu-id="afa33-194">Campos</span><span class="sxs-lookup"><span data-stu-id="afa33-194">Fields</span></span></td><td><span data-ttu-id="afa33-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (limpar todos os outros campos)</span><span class="sxs-lookup"><span data-stu-id="afa33-195">*Year*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *Origin*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*, *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (clear all other fields)</span></span></td></tr>
    </table><span data-ttu-id="afa33-196">
3. Clique em **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="afa33-196">
3. Click **Download**.</span></span>
<span data-ttu-id="afa33-197">4.</span><span class="sxs-lookup"><span data-stu-id="afa33-197">4.</span></span> <span data-ttu-id="afa33-198">Descompacte Olá arquivo toohello **C:\Tutorials\FlightDelay\2013Data** pasta.</span><span class="sxs-lookup"><span data-stu-id="afa33-198">Unzip hello file toohello **C:\Tutorials\FlightDelay\2013Data** folder.</span></span> <span data-ttu-id="afa33-199">Cada arquivo é um arquivo CSV e tem aproximadamente 60 GB de tamanho.</span><span class="sxs-lookup"><span data-stu-id="afa33-199">Each file is a CSV file and is approximately 60GB in size.</span></span>
<span data-ttu-id="afa33-200">5.</span><span class="sxs-lookup"><span data-stu-id="afa33-200">5.</span></span> <span data-ttu-id="afa33-201">Renomear Olá arquivo toohello do mês de saudação que ele contém dados.</span><span class="sxs-lookup"><span data-stu-id="afa33-201">Rename hello file toohello name of hello month that it contains data for.</span></span> <span data-ttu-id="afa33-202">Por exemplo, arquivo hello contendo dados de janeiro de saudação será chamado *January.csv*.</span><span class="sxs-lookup"><span data-stu-id="afa33-202">For example, hello file containing hello January data would be named *January.csv*.</span></span>
<span data-ttu-id="afa33-203">6.</span><span class="sxs-lookup"><span data-stu-id="afa33-203">6.</span></span> <span data-ttu-id="afa33-204">Repita toodownload as etapas 2 e 5 um arquivo para cada Olá 12 meses em 2013.</span><span class="sxs-lookup"><span data-stu-id="afa33-204">Repeat steps 2 and 5 toodownload a file for each of hello 12 months in 2013.</span></span> <span data-ttu-id="afa33-205">Será necessário um mínimo de um tutorial de saudação toorun de arquivo.</span><span class="sxs-lookup"><span data-stu-id="afa33-205">You will need a minimum of one file toorun hello tutorial.</span></span>

<span data-ttu-id="afa33-206">**atraso de voo do tooupload Olá dados tooAzure armazenamento de Blob**</span><span class="sxs-lookup"><span data-stu-id="afa33-206">**tooupload hello flight delay data tooAzure Blob storage**</span></span>

1. <span data-ttu-id="afa33-207">Olá parâmetros de preparação:</span><span class="sxs-lookup"><span data-stu-id="afa33-207">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="afa33-208">Nome de variável</span><span class="sxs-lookup"><span data-stu-id="afa33-208">Variable Name</span></span></th><th><span data-ttu-id="afa33-209">Observações</span><span class="sxs-lookup"><span data-stu-id="afa33-209">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="afa33-210">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="afa33-210">$storageAccountName</span></span></td><td><span data-ttu-id="afa33-211">Olá onde você deseja que tooupload Olá dados de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-211">hello Azure Storage account where you want tooupload hello data to.</span></span></td></tr>
    <tr><td><span data-ttu-id="afa33-212">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="afa33-212">$blobContainerName</span></span></td><td><span data-ttu-id="afa33-213">Olá onde você deseja que tooupload Olá dados de contêiner de Blob.</span><span class="sxs-lookup"><span data-stu-id="afa33-213">hello Blob container where you want tooupload hello data to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="afa33-214">Abra o ISE do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-214">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="afa33-215">3.</span><span class="sxs-lookup"><span data-stu-id="afa33-215">3.</span></span> <span data-ttu-id="afa33-216">Cole Olá script a seguir no painel de script hello:</span><span class="sxs-lookup"><span data-stu-id="afa33-216">Paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. <span data-ttu-id="afa33-217">Pressione **F5** toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="afa33-217">Press **F5** toorun hello script.</span></span>

<span data-ttu-id="afa33-218">Se você escolher um método diferente para carregar arquivos Olá toouse, verifique se o caminho do arquivo hello é flightdelay/tutoriais/dados.</span><span class="sxs-lookup"><span data-stu-id="afa33-218">If you choose toouse a different method for uploading hello files, please make sure hello file path is tutorials/flightdelay/data.</span></span> <span data-ttu-id="afa33-219">sintaxe de saudação para acessar arquivos de saudação é:</span><span class="sxs-lookup"><span data-stu-id="afa33-219">hello syntax for accessing hello files is:</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

<span data-ttu-id="afa33-220">Olá tutoriais/flightdelay/dados de caminho é criado ao carregar arquivos de saudação de pasta virtual do hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-220">hello path tutorials/flightdelay/data is hello virtual folder you created when you uploaded hello files.</span></span> <span data-ttu-id="afa33-221">Verifique se há 12 arquivos, um para cada mês.</span><span class="sxs-lookup"><span data-stu-id="afa33-221">Verify that there are 12 files, one for each month.</span></span>

> [!NOTE]
> <span data-ttu-id="afa33-222">Você deve atualizar Olá tooread de consulta de Hive do novo local de saudação.</span><span class="sxs-lookup"><span data-stu-id="afa33-222">You must update hello Hive query tooread from hello new location.</span></span>
>
> <span data-ttu-id="afa33-223">Você deve configurar Olá contêiner acesso permissão toobe público ou associar toohello conta de armazenamento Olá cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="afa33-223">You must either configure hello container access permission toobe public or bind hello Storage account toohello HDInsight cluster.</span></span> <span data-ttu-id="afa33-224">Caso contrário, cadeia de caracteres de consulta de Hive Olá não será capaz de tooaccess os arquivos de dados hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-224">Otherwise, hello Hive query string will not be able tooaccess hello data files.</span></span>

- - -

## <span data-ttu-id="afa33-225"><a id="appendix-b"></a>Apêndice B - Criar e carregar o script HiveQL</span><span class="sxs-lookup"><span data-stu-id="afa33-225"><a id="appendix-b"></a>Appendix B - Create and upload a HiveQL script</span></span>
<span data-ttu-id="afa33-226">Usando o PowerShell do Azure, você pode executar várias instruções HiveQL um em uma hora ou instrução de estilo de saudação de pacote em um arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="afa33-226">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="afa33-227">Esta seção mostra como toocreate um script HiveQL e carregamento Olá script tooAzure armazenamento de Blob usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-227">This section shows you how toocreate a HiveQL script and upload hello script tooAzure Blob storage by using Azure PowerShell.</span></span> <span data-ttu-id="afa33-228">Hive requer Olá HiveQL scripts toobe armazenado no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-228">Hive requires hello HiveQL scripts toobe stored in Azure Blob storage.</span></span>

<span data-ttu-id="afa33-229">Olá script HiveQL executará o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="afa33-229">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="afa33-230">**Descartar Olá delays_raw tabela**, no caso de Olá tabela já existir.</span><span class="sxs-lookup"><span data-stu-id="afa33-230">**Drop hello delays_raw table**, in case hello table already exists.</span></span>
2. <span data-ttu-id="afa33-231">**Criar tabela de Hive externa Olá delays_raw** apontando o local de armazenamento de Blob toohello com arquivos de atraso de voo hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-231">**Create hello delays_raw external Hive table** pointing toohello Blob storage location with hello flight delay files.</span></span> <span data-ttu-id="afa33-232">Esta consulta especifica que os campos são delimitados por "," e que as linhas são finalizadas por "\n".</span><span class="sxs-lookup"><span data-stu-id="afa33-232">This query specifies that fields are delimited by "," and that lines are terminated by "\n".</span></span> <span data-ttu-id="afa33-233">Isso representa um problema quando os valores de campo contêm vírgulas porque a seção não é possível diferenciar entre uma vírgula que é um delimitador de campo e uma que faz parte de um valor de campo (que é o caso de saudação em valores de campo para a origem de\_CITY\_nome e destino\_ Cidade\_nome).</span><span class="sxs-lookup"><span data-stu-id="afa33-233">This poses a problem when field values contain commas because Hive cannot differentiate between a comma that is a field delimiter and a one that is part of a field value (which is hello case in field values for ORIGIN\_CITY\_NAME and DEST\_CITY\_NAME).</span></span> <span data-ttu-id="afa33-234">tooaddress, Olá consulta cria colunas TEMP toohold dados incorretamente são divididos em colunas.</span><span class="sxs-lookup"><span data-stu-id="afa33-234">tooaddress this, hello query creates TEMP columns toohold data that is incorrectly split into columns.</span></span>
3. <span data-ttu-id="afa33-235">**Descartar a tabela de atrasos de saudação**, no caso de Olá tabela já existir.</span><span class="sxs-lookup"><span data-stu-id="afa33-235">**Drop hello delays table**, in case hello table already exists.</span></span>
4. <span data-ttu-id="afa33-236">**Criar tabela de atrasos de saudação**.</span><span class="sxs-lookup"><span data-stu-id="afa33-236">**Create hello delays table**.</span></span> <span data-ttu-id="afa33-237">É útil tooclean dados Olá antes de continuar o processamento.</span><span class="sxs-lookup"><span data-stu-id="afa33-237">It is helpful tooclean up hello data before further processing.</span></span> <span data-ttu-id="afa33-238">Esta consulta cria uma nova tabela, *atrasos*, da tabela de delays_raw hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-238">This query creates a new table, *delays*, from hello delays_raw table.</span></span> <span data-ttu-id="afa33-239">Observe que as colunas TEMP hello (conforme mencionado anteriormente) não são copiadas e que hello **subcadeia de caracteres** função é tooremove usadas aspas de dados saudação.</span><span class="sxs-lookup"><span data-stu-id="afa33-239">Note that hello TEMP columns (as mentioned previously) are not copied, and that hello **substring** function is used tooremove quotation marks from hello data.</span></span>
5. <span data-ttu-id="afa33-240">**Computação Olá tempo médio atraso e grupos Olá resultados por nome de cidade.**</span><span class="sxs-lookup"><span data-stu-id="afa33-240">**Compute hello average weather delay and groups hello results by city name.**</span></span> <span data-ttu-id="afa33-241">Ele também mostrará armazenamento de tooBlob Olá resultados.</span><span class="sxs-lookup"><span data-stu-id="afa33-241">It will also output hello results tooBlob storage.</span></span> <span data-ttu-id="afa33-242">Observe que consultam Olá Remova dados saudação da apóstrofos e excluirá linhas onde Olá valor para **weather_delay** é nulo.</span><span class="sxs-lookup"><span data-stu-id="afa33-242">Note that hello query will remove apostrophes from hello data and will exclude rows where hello value for **weather_delay** is null.</span></span> <span data-ttu-id="afa33-243">Isso é necessário porque o Sqoop, usado mais adiante neste tutorial, não trata desses valores normalmente por padrão.</span><span class="sxs-lookup"><span data-stu-id="afa33-243">This is necessary because Sqoop, used later in this tutorial, doesn't handle those values gracefully by default.</span></span>

<span data-ttu-id="afa33-244">Para obter uma lista completa de comandos de HiveQL hello, consulte [linguagem de definição de dados Hive][hadoop-hiveql].</span><span class="sxs-lookup"><span data-stu-id="afa33-244">For a full list of hello HiveQL commands, see [Hive Data Definition Language][hadoop-hiveql].</span></span> <span data-ttu-id="afa33-245">Cada comando HiveQL deve terminar com um ponto e vírgula.</span><span class="sxs-lookup"><span data-stu-id="afa33-245">Each HiveQL command must terminate with a semicolon.</span></span>

<span data-ttu-id="afa33-246">**toocreate um arquivo de script HiveQL**</span><span class="sxs-lookup"><span data-stu-id="afa33-246">**toocreate a HiveQL script file**</span></span>

1. <span data-ttu-id="afa33-247">Olá parâmetros de preparação:</span><span class="sxs-lookup"><span data-stu-id="afa33-247">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="afa33-248">Nome de variável</span><span class="sxs-lookup"><span data-stu-id="afa33-248">Variable Name</span></span></th><th><span data-ttu-id="afa33-249">Observações</span><span class="sxs-lookup"><span data-stu-id="afa33-249">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="afa33-250">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="afa33-250">$storageAccountName</span></span></td><td><span data-ttu-id="afa33-251">Olá conta de armazenamento do Azure onde deseja que o script de HiveQL tooupload Olá para.</span><span class="sxs-lookup"><span data-stu-id="afa33-251">hello Azure Storage account where you want tooupload hello HiveQL script to.</span></span></td></tr>
    <tr><td><span data-ttu-id="afa33-252">$blobContainerName</span><span class="sxs-lookup"><span data-stu-id="afa33-252">$blobContainerName</span></span></td><td><span data-ttu-id="afa33-253">Olá contêiner de Blob onde você deseja que o script de HiveQL tooupload Olá para.</span><span class="sxs-lookup"><span data-stu-id="afa33-253">hello Blob container where you want tooupload hello HiveQL script to.</span></span></td></tr>
    </table>
2. <span data-ttu-id="afa33-254">Abra o ISE do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-254">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="afa33-255">3.</span><span class="sxs-lookup"><span data-stu-id="afa33-255">3.</span></span> <span data-ttu-id="afa33-256">Copie e cole Olá script a seguir no painel de script hello:</span><span class="sxs-lookup"><span data-stu-id="afa33-256">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
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

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    <span data-ttu-id="afa33-257">Aqui estão as variáveis Olá usados no script hello:</span><span class="sxs-lookup"><span data-stu-id="afa33-257">Here are hello variables used in hello script:</span></span>

   * <span data-ttu-id="afa33-258">**$hqlLocalFileName** -script hello salva o arquivo de script de HiveQL Olá localmente antes de carregá-lo tooBlob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="afa33-258">**$hqlLocalFileName** - hello script saves hello HiveQL script file locally before uploading it tooBlob storage.</span></span> <span data-ttu-id="afa33-259">Este é o nome do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-259">This is hello file name.</span></span> <span data-ttu-id="afa33-260">valor padrão de saudação é <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span><span class="sxs-lookup"><span data-stu-id="afa33-260">hello default value is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.</span></span>
   * <span data-ttu-id="afa33-261">**$hqlBlobName** -esse é nome hello HiveQL script arquivo blob usado em Olá armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-261">**$hqlBlobName** - This is hello HiveQL script file blob name used in hello Azure Blob storage.</span></span> <span data-ttu-id="afa33-262">valor padrão de saudação é tutorials/flightdelay/flightdelays.hql.</span><span class="sxs-lookup"><span data-stu-id="afa33-262">hello default value is tutorials/flightdelay/flightdelays.hql.</span></span> <span data-ttu-id="afa33-263">Porque o arquivo hello será gravado diretamente tooAzure armazenamento de Blob, não há um "/" no início de saudação do nome do blob hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-263">Because hello file will be written directly tooAzure Blob storage, there is NOT a "/" at hello beginning of hello blob name.</span></span> <span data-ttu-id="afa33-264">Se desejar que o arquivo de saudação do tooaccess do armazenamento de Blob, você precisará tooadd um "/" no início de saudação do nome de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-264">If you want tooaccess hello file from Blob storage, you will need tooadd a "/" at hello beginning of hello file name.</span></span>
   * <span data-ttu-id="afa33-265">**$srcDataFolder** e **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span><span class="sxs-lookup"><span data-stu-id="afa33-265">**$srcDataFolder** and **$dstDataFolder** - = "tutorials/flightdelay/data" = "tutorials/flightdelay/output"</span></span>

- - -
## <span data-ttu-id="afa33-266"><a id="appendix-c"></a>Apêndice C – preparar um banco de dados do SQL Azure para Olá saída do trabalho de Sqoop</span><span class="sxs-lookup"><span data-stu-id="afa33-266"><a id="appendix-c"></a>Appendix C - Prepare an Azure SQL database for hello Sqoop job output</span></span>
<span data-ttu-id="afa33-267">**banco de dados do SQL tooprepare hello (mesclar com hello Sqoop script)**</span><span class="sxs-lookup"><span data-stu-id="afa33-267">**tooprepare hello SQL database (merge this with hello Sqoop script)**</span></span>

1. <span data-ttu-id="afa33-268">Olá parâmetros de preparação:</span><span class="sxs-lookup"><span data-stu-id="afa33-268">Prepare hello parameters:</span></span>

    <table border="1">
    <tr><th><span data-ttu-id="afa33-269">Nome de variável</span><span class="sxs-lookup"><span data-stu-id="afa33-269">Variable Name</span></span></th><th><span data-ttu-id="afa33-270">Observações</span><span class="sxs-lookup"><span data-stu-id="afa33-270">Notes</span></span></th></tr>
    <tr><td><span data-ttu-id="afa33-271">$sqlDatabaseServerName</span><span class="sxs-lookup"><span data-stu-id="afa33-271">$sqlDatabaseServerName</span></span></td><td><span data-ttu-id="afa33-272">nome de saudação do servidor de banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-272">hello name of hello Azure SQL database server.</span></span> <span data-ttu-id="afa33-273">Inserir nada toocreate um novo servidor.</span><span class="sxs-lookup"><span data-stu-id="afa33-273">Enter nothing toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="afa33-274">$sqlDatabaseUsername</span><span class="sxs-lookup"><span data-stu-id="afa33-274">$sqlDatabaseUsername</span></span></td><td><span data-ttu-id="afa33-275">nome de logon Olá para o servidor de banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-275">hello login name for hello Azure SQL database server.</span></span> <span data-ttu-id="afa33-276">Se $sqlDatabaseServerName for um servidor existente, o logon hello e a senha de logon são tooauthenticate usado com o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="afa33-276">If $sqlDatabaseServerName is an existing server, hello login and login password are used tooauthenticate with hello server.</span></span> <span data-ttu-id="afa33-277">Caso contrário, eles são usado toocreate um novo servidor.</span><span class="sxs-lookup"><span data-stu-id="afa33-277">Otherwise they are used toocreate a new server.</span></span></td></tr>
    <tr><td><span data-ttu-id="afa33-278">$sqlDatabasePassword</span><span class="sxs-lookup"><span data-stu-id="afa33-278">$sqlDatabasePassword</span></span></td><td><span data-ttu-id="afa33-279">senha de logon Olá para o servidor de banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-279">hello login password for hello Azure SQL database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="afa33-280">$sqlDatabaseLocation</span><span class="sxs-lookup"><span data-stu-id="afa33-280">$sqlDatabaseLocation</span></span></td><td><span data-ttu-id="afa33-281">Esse valor é usado somente quando você estiver criando um novo servidor de banco de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-281">This value is used only when you're creating a new Azure database server.</span></span></td></tr>
    <tr><td><span data-ttu-id="afa33-282">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="afa33-282">$sqlDatabaseName</span></span></td><td><span data-ttu-id="afa33-283">banco de dados SQL Olá usado tabela AvgDelays a toocreate Olá para o trabalho de Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-283">hello SQL database used toocreate hello AvgDelays table for hello Sqoop job.</span></span> <span data-ttu-id="afa33-284">Deixar em branco criará um banco de dados chamado HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="afa33-284">Leaving it blank will create a database called HDISqoop.</span></span> <span data-ttu-id="afa33-285">nome da tabela Olá Olá saída do trabalho de Sqoop é AvgDelays.</span><span class="sxs-lookup"><span data-stu-id="afa33-285">hello table name for hello Sqoop job output is AvgDelays.</span></span> </td></tr>
    </table>
2. <span data-ttu-id="afa33-286">Abra o ISE do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-286">Open Azure PowerShell ISE.</span></span>
<span data-ttu-id="afa33-287">3.</span><span class="sxs-lookup"><span data-stu-id="afa33-287">3.</span></span> <span data-ttu-id="afa33-288">Copie e cole Olá script a seguir no painel de script hello:</span><span class="sxs-lookup"><span data-stu-id="afa33-288">Copy and paste hello following script into hello script pane:</span></span>

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
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

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
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

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
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

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > <span data-ttu-id="afa33-289">Olá script usa um serviço REST (transferência) de estado representacional, http://bot.whatismyipaddress.com, tooretrieve seu endereço IP externo.</span><span class="sxs-lookup"><span data-stu-id="afa33-289">hello script uses a representational state transfer (REST) service, http://bot.whatismyipaddress.com, tooretrieve your external IP address.</span></span> <span data-ttu-id="afa33-290">endereço IP de saudação é usado para criar uma regra de firewall para o servidor de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="afa33-290">hello IP address is used for creating a firewall rule for your SQL database server.</span></span>

    <span data-ttu-id="afa33-291">Aqui estão algumas variáveis usadas em script hello:</span><span class="sxs-lookup"><span data-stu-id="afa33-291">Here are some variables used in hello script:</span></span>

   * <span data-ttu-id="afa33-292">**$ipAddressRestService** -valor de padrão de saudação é http://bot.whatismyipaddress.com. Trata-se de um serviço REST de endereço IP público para obter seu endereço IP externo.</span><span class="sxs-lookup"><span data-stu-id="afa33-292">**$ipAddressRestService** - hello default value is http://bot.whatismyipaddress.com. It is a public IP address REST service for getting your external IP address.</span></span> <span data-ttu-id="afa33-293">Você pode usar outros serviços se desejar.</span><span class="sxs-lookup"><span data-stu-id="afa33-293">You can use other services if you want.</span></span> <span data-ttu-id="afa33-294">endereço IP externo Olá recuperado por meio do serviço de saudação será usado toocreate uma regra de firewall para o servidor de banco de dados do SQL Azure, para que você pode acessar o banco de dados de saudação de sua estação de trabalho (por meio de um script do Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="afa33-294">hello external IP address retrieved through hello service will be used toocreate a firewall rule for your Azure SQL database server, so that you can access hello database from your workstation (by using a Windows PowerShell script).</span></span>
   * <span data-ttu-id="afa33-295">**$fireWallRuleName** -esse é nome Olá Olá de regra de firewall para o servidor de banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-295">**$fireWallRuleName** - This is hello name of hello firewall rule for hello Azure SQL database server.</span></span> <span data-ttu-id="afa33-296">nome do padrão de saudação é <u>FlightDelay</u>.</span><span class="sxs-lookup"><span data-stu-id="afa33-296">hello default name is <u>FlightDelay</u>.</span></span> <span data-ttu-id="afa33-297">Você pode renomeá-lo se desejar.</span><span class="sxs-lookup"><span data-stu-id="afa33-297">You can rename it if you want.</span></span>
   * <span data-ttu-id="afa33-298">**$sqlDatabaseMaxSizeGB** - Esse valor é usado apenas ao criar um novo servidor de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-298">**$sqlDatabaseMaxSizeGB** - This value is used only when you're creating a new Azure SQL database server.</span></span> <span data-ttu-id="afa33-299">valor padrão de saudação é de 10GB.</span><span class="sxs-lookup"><span data-stu-id="afa33-299">hello default value is 10GB.</span></span> <span data-ttu-id="afa33-300">10GB são suficientes para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="afa33-300">10GB is sufficient for this tutorial.</span></span>
   * <span data-ttu-id="afa33-301">**$sqlDatabaseName** - Esse valor é usado apenas ao criar um novo banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-301">**$sqlDatabaseName** - This value is used only when you're creating a new Azure SQL database.</span></span> <span data-ttu-id="afa33-302">valor padrão de saudação é HDISqoop.</span><span class="sxs-lookup"><span data-stu-id="afa33-302">hello default value is HDISqoop.</span></span> <span data-ttu-id="afa33-303">Se você renomeá-la, você deve atualizar o script do Windows PowerShell de Sqoop Olá adequadamente.</span><span class="sxs-lookup"><span data-stu-id="afa33-303">If you rename it, you must update hello Sqoop Windows PowerShell script accordingly.</span></span>
4. <span data-ttu-id="afa33-304">Pressione **F5** toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="afa33-304">Press **F5** toorun hello script.</span></span>
5. <span data-ttu-id="afa33-305">Valide a saída do script hello.</span><span class="sxs-lookup"><span data-stu-id="afa33-305">Validate hello script output.</span></span> <span data-ttu-id="afa33-306">Verifique se o script hello foi executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="afa33-306">Make sure hello script ran successfully.</span></span>

## <span data-ttu-id="afa33-307"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="afa33-307"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="afa33-308">Se você sabe como tooupload tooAzure um arquivo armazenamento de Blob, como toopopulate uma seção de tabela usando dados de saudação do armazenamento de BLOBs do Azure, como toorun Hive consultas e como toouse Sqoop tooexport dados do banco de dados do HDFS tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="afa33-308">Now you understand how tooupload a file tooAzure Blob storage, how toopopulate a Hive table by using hello data from Azure Blob storage, how toorun Hive queries, and how toouse Sqoop tooexport data from HDFS tooan Azure SQL database.</span></span> <span data-ttu-id="afa33-309">toolearn mais, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="afa33-309">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="afa33-310">[Introdução ao HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="afa33-310">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="afa33-311">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="afa33-311">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="afa33-312">[Usar o Oozie com o HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="afa33-312">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="afa33-313">[Use o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="afa33-313">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="afa33-314">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="afa33-314">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="afa33-315">[Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="afa33-315">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
