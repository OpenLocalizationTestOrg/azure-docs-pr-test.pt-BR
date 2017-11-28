---
title: "aaaCreate clusters de Hadoop sob demanda usando a fábrica de dados – HDInsight do Azure | Microsoft Docs"
description: Saiba como toocreate Hadoop sob demanda clusters de HDInsight usando o Azure Data Factory.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: spelluru
ms.openlocfilehash: c869776ac270e37dec710b5fc8d2a792d9263129
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="76190-103">Criar clusters Hadoop sob demanda usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="76190-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="76190-104">[O Azure Data Factory](../data-factory/data-factory-introduction.md) é um serviço de integração de dados com base em nuvem que orquestra e automatiza a movimentação de saudação e a transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="76190-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="76190-105">Ele pode criar um tooprocess de just-in-time do cluster HDInsight Hadoop uma fatia de dados de entrada e excluir o cluster hello quando Olá processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="76190-105">It can create a HDInsight Hadoop cluster just-in-time tooprocess an input data slice and delete hello cluster when hello processing is complete.</span></span> <span data-ttu-id="76190-106">Alguns dos benefícios de saudação do uso de um cluster do Hadoop de HDInsight sob demanda são:</span><span class="sxs-lookup"><span data-stu-id="76190-106">Some of hello benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="76190-107">Pagamento somente para trabalhos de timer hello está em execução Olá cluster HDInsight Hadoop (mais um breve tempo ocioso configurável).</span><span class="sxs-lookup"><span data-stu-id="76190-107">You only pay for hello time job is running on hello HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="76190-108">cobrança Olá para clusters de HDInsight é proporcional por minuto, se você estiver usando ou não.</span><span class="sxs-lookup"><span data-stu-id="76190-108">hello billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="76190-109">Quando você usa um serviço de vinculado do HDInsight sob demanda fábrica de dados, clusters de saudação são criados sob demanda.</span><span class="sxs-lookup"><span data-stu-id="76190-109">When you use an on-demand HDInsight linked service in Data Factory, hello clusters are created on-demand.</span></span> <span data-ttu-id="76190-110">E clusters de saudação são excluídos automaticamente quando Olá trabalhos são concluídos.</span><span class="sxs-lookup"><span data-stu-id="76190-110">And hello clusters are deleted automatically when hello jobs are completed.</span></span> <span data-ttu-id="76190-111">Portanto, você só paga pelo trabalho de saudação tempo e tempo ocioso breve hello (configuração de tempo de vida).</span><span class="sxs-lookup"><span data-stu-id="76190-111">Therefore, you only pay for hello job running time and hello brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="76190-112">Você pode criar um fluxo de trabalho usando um pipeline do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76190-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="76190-113">Por exemplo, você pode ter dados de toocopy de pipeline de saudação de um tooan do SQL Server local armazenamento de BLOBs do Azure, dados de saudação do processo executando um script de Hive e um script do Pig em um cluster do Hadoop de HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="76190-113">For example, you can have hello pipeline toocopy data from an on-premises SQL Server tooan Azure blob storage, process hello data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="76190-114">Em seguida, copie tooan de dados de resultado hello Azure SQL Data Warehouse para tooconsume de aplicativos de BI.</span><span class="sxs-lookup"><span data-stu-id="76190-114">Then, copy hello result data tooan Azure SQL Data Warehouse for BI applications tooconsume.</span></span>
- <span data-ttu-id="76190-115">Você pode agendar Olá fluxo de trabalho toorun periodicamente (por hora, diariamente, semanalmente, mensalmente, etc.).</span><span class="sxs-lookup"><span data-stu-id="76190-115">You can schedule hello workflow toorun periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="76190-116">No Azure Data Factory, um data factory pode ter um ou mais pipelines de dados.</span><span class="sxs-lookup"><span data-stu-id="76190-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="76190-117">Um pipeline de dados tem uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="76190-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="76190-118">Há dois tipos de atividades: [Atividades de Movimentação de Dados](../data-factory/data-factory-data-movement-activities.md) e [Atividades de Transformação de Dados](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="76190-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="76190-119">Você pode usar dados de toomove de atividades (atualmente, apenas copiar atividade) de movimentação de dados de um repositório de dados de destino fonte dados repositório tooa.</span><span class="sxs-lookup"><span data-stu-id="76190-119">You use data movement activities (currently, only Copy Activity) toomove data from a source data store tooa destination data store.</span></span> <span data-ttu-id="76190-120">Você usar dados de processo/tootransform de atividades de transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="76190-120">You use data transformation activities tootransform/process data.</span></span> <span data-ttu-id="76190-121">Atividade de Hive do HDInsight é uma das atividades de transformação Olá suportadas pela fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="76190-121">HDInsight Hive Activity is one of hello transformation activities supported by Data Factory.</span></span> <span data-ttu-id="76190-122">Você pode usar atividades de transformação de Hive Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="76190-122">You use hello Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="76190-123">Você pode configurar um toouse de atividade de hive seu próprio cluster HDInsight Hadoop ou um cluster do Hadoop de HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="76190-123">You can configure a hive activity toouse your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="76190-124">Neste tutorial, hello atividade de Hive no pipeline da fábrica de dados Olá é configurado toouse um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="76190-124">In this tutorial, hello Hive activity in hello data factory pipeline is configured toouse an on-demand HDInsight cluster.</span></span> <span data-ttu-id="76190-125">Portanto, quando a atividade Olá executa tooprocess uma fatia de dados, aqui está o que acontece:</span><span class="sxs-lookup"><span data-stu-id="76190-125">Therefore, when hello activity runs tooprocess a data slice, here is what happens:</span></span>

1. <span data-ttu-id="76190-126">Um cluster HDInsight Hadoop é criado automaticamente para a fatia Olá tooprocess just-in-time.</span><span class="sxs-lookup"><span data-stu-id="76190-126">A HDInsight Hadoop cluster is automatically created for you just-in-time tooprocess hello slice.</span></span>  
2. <span data-ttu-id="76190-127">dados de entrada Hello são processados, executando um script HiveQL no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="76190-127">hello input data is processed by running a HiveQL script on hello cluster.</span></span>
3. <span data-ttu-id="76190-128">Olá cluster HDInsight Hadoop será excluída após Olá processamento é concluído e cluster Olá estiver ocioso por Olá configurado (timeToLive configuração) de tempo.</span><span class="sxs-lookup"><span data-stu-id="76190-128">hello HDInsight Hadoop cluster is deleted after hello processing is complete and hello cluster is idle for hello configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="76190-129">Se a próxima fatia de dados hello está disponível para processamento nesse período ocioso timeToLive, hello mesmo cluster é usado tooprocess Olá fatia.</span><span class="sxs-lookup"><span data-stu-id="76190-129">If hello next data slice is available for processing with in this timeToLive idle time, hello same cluster is used tooprocess hello slice.</span></span>  

<span data-ttu-id="76190-130">Neste tutorial, Olá script HiveQL associada à atividade de hive Olá executa Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="76190-130">In this tutorial, hello HiveQL script associated with hello hive activity performs hello following actions:</span></span>

1. <span data-ttu-id="76190-131">Cria uma tabela externa referências Olá dados de log web bruto armazenados em um armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-131">Creates an external table that references hello raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="76190-132">Dados brutos de saudação de partições por ano e mês.</span><span class="sxs-lookup"><span data-stu-id="76190-132">Partitions hello raw data by year and month.</span></span>
3. <span data-ttu-id="76190-133">Repositórios Olá dados particionados em Olá armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-133">Stores hello partitioned data in hello Azure blob storage.</span></span>

<span data-ttu-id="76190-134">Neste tutorial, Olá script HiveQL associada à atividade de hive Olá cria uma tabela externa referências Olá dados de log de web bruto armazenados em Olá armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-134">In this tutorial, hello HiveQL script associated with hello hive activity creates an external table that references hello raw web log data stored in hello Azure Blob Storage.</span></span> <span data-ttu-id="76190-135">Aqui estão as linhas de exemplo de saudação para cada mês no arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="76190-135">Here are hello sample rows for each month in hello input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="76190-136">partições de script HiveQL Olá Olá dados brutos por ano e mês.</span><span class="sxs-lookup"><span data-stu-id="76190-136">hello HiveQL script partitions hello raw data by year and month.</span></span> <span data-ttu-id="76190-137">Ele cria três pastas de saída com base na entrada de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="76190-137">It creates three output folders based on hello previous input.</span></span> <span data-ttu-id="76190-138">Cada pasta contém um arquivo com entradas de cada mês.</span><span class="sxs-lookup"><span data-stu-id="76190-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="76190-139">Para obter uma lista de atividades de transformação de dados de fábrica de dados na atividade de tooHive de adição, consulte [transformar e analisar o uso do Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="76190-139">For a list of Data Factory data transformation activities in addition tooHive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="76190-140">No momento, você só pode criar o cluster HDInsight versão 3.2 do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76190-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76190-141">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="76190-141">Prerequisites</span></span>
<span data-ttu-id="76190-142">Antes de começar a instruções Olá neste artigo, você deve ter Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="76190-142">Before you begin hello instructions in this article, you must have hello following items:</span></span>

* <span data-ttu-id="76190-143">[Assinatura do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="76190-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="76190-144">PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="76190-145">Preparar a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="76190-145">Prepare storage account</span></span>
<span data-ttu-id="76190-146">Você pode usar as contas de armazenamento toothree neste cenário:</span><span class="sxs-lookup"><span data-stu-id="76190-146">You can use up toothree storage accounts in this scenario:</span></span>

- <span data-ttu-id="76190-147">conta de armazenamento padrão para o cluster do HDInsight Olá</span><span class="sxs-lookup"><span data-stu-id="76190-147">default storage account for hello HDInsight cluster</span></span>
- <span data-ttu-id="76190-148">conta de armazenamento para dados de entrada hello</span><span class="sxs-lookup"><span data-stu-id="76190-148">storage account for hello input data</span></span>
- <span data-ttu-id="76190-149">conta de armazenamento para dados de saída de saudação</span><span class="sxs-lookup"><span data-stu-id="76190-149">storage account for hello output data</span></span>

<span data-ttu-id="76190-150">tutorial de saudação toosimplify, você usar uma conta tooserve Olá três fins de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76190-150">toosimplify hello tutorial, you use one storage account tooserve hello three purposes.</span></span> <span data-ttu-id="76190-151">script de exemplo do PowerShell do Azure Olá encontrado nesta seção executa Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="76190-151">hello Azure PowerShell sample script found in this section performs hello following tasks:</span></span>

1. <span data-ttu-id="76190-152">Faça logon em tooAzure.</span><span class="sxs-lookup"><span data-stu-id="76190-152">Log in tooAzure.</span></span>
2. <span data-ttu-id="76190-153">Crie um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="76190-154">Criar uma conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="76190-155">Criar um contêiner de Blob na conta de armazenamento de saudação</span><span class="sxs-lookup"><span data-stu-id="76190-155">Create a Blob container in hello storage account</span></span>
5. <span data-ttu-id="76190-156">Copie Olá dois contêiner de Blob de toohello arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="76190-156">Copy hello following two files toohello Blob container:</span></span>

   * <span data-ttu-id="76190-157">Arquivo de dados de entrada: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="76190-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="76190-158">Script HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="76190-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="76190-159">Os dois arquivos são armazenados em um contêiner de Blob público.</span><span class="sxs-lookup"><span data-stu-id="76190-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="76190-160">**tooprepare Olá armazenamento e copiar Olá arquivos usando o Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="76190-160">**tooprepare hello storage and copy hello files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="76190-161">Especifique os nomes de grupo de recursos do Azure hello e conta de armazenamento do Azure Olá que será criada pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="76190-161">Specify names for hello Azure resource group and hello Azure storage account that will be created by hello script.</span></span>
> <span data-ttu-id="76190-162">Anote **nome do grupo de recursos**, **nome da conta de armazenamento**, e **chave da conta de armazenamento** gerados por script hello.</span><span class="sxs-lookup"><span data-stu-id="76190-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by hello script.</span></span> <span data-ttu-id="76190-163">Necessário na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="76190-163">You need them in hello next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect tooAzure
####################################
#region - Connect tooAzure subscription
Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use hello following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="76190-164">Se você precisar de ajuda com script do PowerShell hello, consulte [hello usando o PowerShell do Azure com o armazenamento do Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="76190-164">If you need help with hello PowerShell script, see [Using hello Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="76190-165">Se você deseja toouse CLI do Azure em vez disso, consulte Olá [apêndice](#appendix) seção para Olá script CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-165">If you like toouse Azure CLI instead, see hello [Appendix](#appendix) section for hello Azure CLI script.</span></span>

<span data-ttu-id="76190-166">**conteúdo de saudação e de conta de armazenamento de saudação do tooexamine**</span><span class="sxs-lookup"><span data-stu-id="76190-166">**tooexamine hello storage account and hello contents**</span></span>

1. <span data-ttu-id="76190-167">Logon toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="76190-167">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="76190-168">Clique em **grupos de recursos** no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-168">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="76190-169">Clique duas vezes no nome do grupo de recursos Olá criado em seu script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76190-169">Double-click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="76190-170">Use o filtro de saudação se você tiver muitos grupos de recursos listados.</span><span class="sxs-lookup"><span data-stu-id="76190-170">Use hello filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="76190-171">Em Olá **recursos** lado a lado, você deve ter um recurso listado, a menos que você compartilhar o grupo de recursos de saudação com outros projetos.</span><span class="sxs-lookup"><span data-stu-id="76190-171">On hello **Resources** tile, you shall have one resource listed unless you share hello resource group with other projects.</span></span> <span data-ttu-id="76190-172">Esse recurso é a conta de armazenamento de saudação com nome hello especificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="76190-172">That resource is hello storage account with hello name you specified earlier.</span></span> <span data-ttu-id="76190-173">Clique no nome de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="76190-173">Click hello storage account name.</span></span>
5. <span data-ttu-id="76190-174">Clique em Olá **Blobs** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="76190-174">Click hello **Blobs** tiles.</span></span>
6. <span data-ttu-id="76190-175">Clique em Olá **adfgetstarted** contêiner.</span><span class="sxs-lookup"><span data-stu-id="76190-175">Click hello **adfgetstarted** container.</span></span> <span data-ttu-id="76190-176">Você verá duas pastas: **inputdata** e **script**.</span><span class="sxs-lookup"><span data-stu-id="76190-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="76190-177">Abra a pasta de saudação e verifique arquivos Olá Olá das pastas.</span><span class="sxs-lookup"><span data-stu-id="76190-177">Open hello folder and check hello files in hello folders.</span></span> <span data-ttu-id="76190-178">Olá inputdata contém o arquivo de input.log de saudação com dados de entrada e a pasta de scripts Olá contém o arquivo de script hello HiveQL.</span><span class="sxs-lookup"><span data-stu-id="76190-178">hello inputdata contains hello input.log file with input data and hello script folder contains hello HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="76190-179">Criar um data factory usando o modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="76190-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="76190-180">Com conta de armazenamento hello, dados de entrada hello e Olá script HiveQL preparado, você estará pronto toocreate uma fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-180">With hello storage account, hello input data, and hello HiveQL script prepared, you are ready toocreate an Azure data factory.</span></span> <span data-ttu-id="76190-181">Há vários métodos para criar um data factory.</span><span class="sxs-lookup"><span data-stu-id="76190-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="76190-182">Neste tutorial, você pode criar uma fábrica de dados implantando um modelo de Gerenciador de recursos do Azure usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using hello Azure portal.</span></span> <span data-ttu-id="76190-183">Você também pode implantar um modelo do Resource Manager usando a [CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) e o [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="76190-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="76190-184">Para conferir outros métodos de criação de data factory, consulte [Tutorial: compilar seu primeiro data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="76190-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="76190-185">Clique em Olá toosign de imagem no tooAzure e modelo do Gerenciador de recursos de saudação abrir no portal do Azure de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="76190-185">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> <span data-ttu-id="76190-186">modelo de saudação está localizado em https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="76190-186">hello template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="76190-187">Consulte Olá [entidades da fábrica de dados no modelo de saudação](#data-factory-entities-in-the-template) seção para obter informações detalhadas sobre as entidades definidas no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-187">See hello [Data Factory entities in hello template](#data-factory-entities-in-the-template) section for detailed information about entities defined in hello template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="76190-188">Selecione **usar existente** opção Olá **grupo de recursos** configuração e o nome de select Olá Olá do grupo de recursos criado na etapa anterior de saudação (usando o script do PowerShell).</span><span class="sxs-lookup"><span data-stu-id="76190-188">Select **Use existing** option for hello **Resource group** setting, and select hello name of hello resource group you created in hello previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="76190-189">Insira um nome para a fábrica de dados da saudação (**nome da fábrica de dados**).</span><span class="sxs-lookup"><span data-stu-id="76190-189">Enter a name for hello data factory (**Data Factory Name**).</span></span> <span data-ttu-id="76190-190">Esse nome deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="76190-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="76190-191">Digite hello **nome da conta de armazenamento** e **chave da conta de armazenamento** você anotou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="76190-191">Enter hello **storage account name** and **storage account key** you wrote down in hello previous step.</span></span>
5. <span data-ttu-id="76190-192">Selecione **concordo toohello termos e condições** indicado acima, após a leitura por meio de **termos e condições**.</span><span class="sxs-lookup"><span data-stu-id="76190-192">Select **I agree toohello terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="76190-193">Selecione **toodashboard Pin** opção.</span><span class="sxs-lookup"><span data-stu-id="76190-193">Select **Pin toodashboard** option.</span></span>
6. <span data-ttu-id="76190-194">Clique em **Comprar/Criar**.</span><span class="sxs-lookup"><span data-stu-id="76190-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="76190-195">Você vê um bloco na Olá painel chamado **implantação de modelo de implantação**.</span><span class="sxs-lookup"><span data-stu-id="76190-195">You see a tile on hello Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="76190-196">Aguarde até que a saudação **grupo de recursos** folha para seu grupo de recursos é aberto.</span><span class="sxs-lookup"><span data-stu-id="76190-196">Wait until hello **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="76190-197">Você também pode clicar em bloco Olá intitulado como a recurso grupo nome tooopen Olá grupo folha de recursos do.</span><span class="sxs-lookup"><span data-stu-id="76190-197">You can also click hello tile titled as your resource group name tooopen hello resource group blade.</span></span>
6. <span data-ttu-id="76190-198">Clique em grupo de recursos de saudação do hello bloco tooopen se folha de grupo de recursos de saudação não ainda estiver aberta.</span><span class="sxs-lookup"><span data-stu-id="76190-198">Click hello tile tooopen hello resource group if hello resource group blade is not already open.</span></span> <span data-ttu-id="76190-199">Agora você deverá ver que um recurso de fábrica de dados mais além listados toohello recurso de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76190-199">Now you shall see one more data factory resource listed in addition toohello storage account resource.</span></span>
7. <span data-ttu-id="76190-200">Clique em nome de saudação da sua fábrica de dados (valor especificado para Olá **nome da fábrica de dados** parâmetro).</span><span class="sxs-lookup"><span data-stu-id="76190-200">Click hello name of your data factory (value you specified for hello **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="76190-201">Na folha de fábrica de dados de saudação, clique em Olá **diagrama** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="76190-201">In hello Data Factory blade, click hello **Diagram** tile.</span></span> <span data-ttu-id="76190-202">diagrama de saudação mostra uma atividade com um conjunto de dados de entrada e um conjunto de dados de saída:</span><span class="sxs-lookup"><span data-stu-id="76190-202">hello diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Diagrama de pipeline de atividade do hive HDInsight sob demanda do Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="76190-204">Olá nomes são definidos no modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-204">hello names are defined in hello Resource Manager template.</span></span>
9. <span data-ttu-id="76190-205">Clique duas vezes em **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="76190-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="76190-206">Em Olá **recente atualizado fatias**, você deverá ver uma fatia.</span><span class="sxs-lookup"><span data-stu-id="76190-206">On hello **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="76190-207">Se o status de saudação é **em andamento**, aguarde até que seja alterado muito**pronto**.</span><span class="sxs-lookup"><span data-stu-id="76190-207">If hello status is **In progress**, wait until it is changed too**Ready**.</span></span> <span data-ttu-id="76190-208">Geralmente demora cerca de **20 minutos** toocreate um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76190-208">It usually takes about **20 minutes** toocreate an HDInsight cluster.</span></span>

### <a name="check-hello-data-factory-output"></a><span data-ttu-id="76190-209">Verifique a saída de fábrica de dados Olá</span><span class="sxs-lookup"><span data-stu-id="76190-209">Check hello data factory output</span></span>

1. <span data-ttu-id="76190-210">Use Olá mesmo procedimento Olá última sessão toocheck Olá contêiner de saudação adfgetstarted contêiner.</span><span class="sxs-lookup"><span data-stu-id="76190-210">Use hello same procedure in hello last session toocheck hello containers of hello adfgetstarted container.</span></span> <span data-ttu-id="76190-211">Há dois novos contêineres além muito**adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="76190-211">There are two new containers in addition too**adfgetsarted**:</span></span>

   * <span data-ttu-id="76190-212">Um contêiner com o nome que segue o padrão de saudação: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="76190-212">A container with name that follows hello pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="76190-213">Esse contêiner é o contêiner de padrão de Olá para o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="76190-213">This container is hello default container for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="76190-214">adfjobs: este contêiner é o contêiner de saudação para logs de trabalho Olá ADF.</span><span class="sxs-lookup"><span data-stu-id="76190-214">adfjobs: This container is hello container for hello ADF job logs.</span></span>

     <span data-ttu-id="76190-215">Olá saída de fábrica de dados é armazenada em **afgetstarted** conforme configurado no modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-215">hello data factory output is stored in **afgetstarted** as you configured in hello Resource Manager template.</span></span>
2. <span data-ttu-id="76190-216">Clique em **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="76190-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="76190-217">Clique duas vezes em **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="76190-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="76190-218">Você verá um **ano = 2014** pasta porque todos os logs da web hello com data no ano de 2014.</span><span class="sxs-lookup"><span data-stu-id="76190-218">You see a **year=2014** folder because all hello web logs are dated in year 2014.</span></span>

    ![Saída do pipeline de atividade do hive HDInsight sob demanda do Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="76190-220">Se você fazer drill down lista hello, você deverá ver três pastas para janeiro, fevereiro e março.</span><span class="sxs-lookup"><span data-stu-id="76190-220">If you drill down hello list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="76190-221">E há um log para cada mês.</span><span class="sxs-lookup"><span data-stu-id="76190-221">And there is a log for each month.</span></span>

    ![Saída do pipeline de atividade do hive HDInsight sob demanda do Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="76190-223">Entidades da fábrica de dados no modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="76190-223">Data Factory entities in hello template</span></span>
<span data-ttu-id="76190-224">Aqui está como modelo de Gerenciador de recursos nível superior Olá para uma fábrica de dados se parece com:</span><span class="sxs-lookup"><span data-stu-id="76190-224">Here is how hello top-level Resource Manager template for a data factory looks like:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="76190-225">Definir Data Factory</span><span class="sxs-lookup"><span data-stu-id="76190-225">Define data factory</span></span>
<span data-ttu-id="76190-226">Você pode definir uma fábrica de dados no modelo do Gerenciador de recursos de saudação conforme Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="76190-226">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="76190-227">Olá dataFactoryName é o nome de Olá Olá da fábrica de dados que especifique quando você implanta o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-227">hello dataFactoryName is hello name of hello data factory you specify when you deploy hello template.</span></span> <span data-ttu-id="76190-228">Fábrica de dados está atualmente só tem suporte em regiões Leste dos EUA, oeste dos EUA e Europa Setentrional de saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-228">Data factory is currently only supported in hello East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-hello-data-factory"></a><span data-ttu-id="76190-229">Definir entidades dentro de fábrica de dados Olá</span><span class="sxs-lookup"><span data-stu-id="76190-229">Defining entities within hello data factory</span></span>
<span data-ttu-id="76190-230">Hello seguintes entidades da fábrica de dados estão definidas no modelo JSON hello:</span><span class="sxs-lookup"><span data-stu-id="76190-230">hello following Data Factory entities are defined in hello JSON template:</span></span>

* [<span data-ttu-id="76190-231">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="76190-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="76190-232">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="76190-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="76190-233">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="76190-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="76190-234">Conjunto de dados de saída do blob do Azure</span><span class="sxs-lookup"><span data-stu-id="76190-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="76190-235">Pipeline com a Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="76190-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="76190-236">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="76190-236">Azure Storage linked service</span></span>
<span data-ttu-id="76190-237">saudação de armazenamento do Azure vinculada links de serviço sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-237">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="76190-238">Neste tutorial, hello mesma conta de armazenamento é usada como conta de armazenamento de HDInsight saudação padrão, o armazenamento de dados de entrada e o armazenamento de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="76190-238">In this tutorial, hello same storage account is used as hello default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="76190-239">Portanto, você define somente um serviço vinculado do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="76190-240">Na definição de serviço Olá vinculado, você pode especificar nome hello e a chave da sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-240">In hello linked service definition, you specify hello name and key of your Azure storage account.</span></span> <span data-ttu-id="76190-241">Consulte [serviço vinculado do armazenamento do Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre o JSON propriedades usadas toodefine um armazenamento do Azure serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="76190-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span>

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="76190-242">Olá **connectionString** usa Olá parâmetros storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="76190-242">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="76190-243">Você pode especificar valores para esses parâmetros durante a implantação de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-243">You specify values for these parameters while deploying hello template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="76190-244">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="76190-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="76190-245">Olá HDInsight sob demanda vinculado definição de serviço, você especificar valores para parâmetros de configuração que são usados por Olá toocreate de serviço de fábrica de dados um HDInsight Hadoop de cluster em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="76190-245">In hello on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by hello Data Factory service toocreate a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="76190-246">Consulte [serviços vinculados de computação](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artigo para obter detalhes sobre o JSON propriedades usadas toodefine um serviço vinculado do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="76190-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="76190-247">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="76190-247">Note hello following points:</span></span>

* <span data-ttu-id="76190-248">Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você.</span><span class="sxs-lookup"><span data-stu-id="76190-248">hello Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="76190-249">Olá cluster HDInsight Hadoop é criado no hello mesma região da conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="76190-249">hello HDInsight Hadoop cluster is created in hello same region as hello storage account.</span></span>
* <span data-ttu-id="76190-250">Saudação de aviso *timeToLive* configuração.</span><span class="sxs-lookup"><span data-stu-id="76190-250">Notice hello *timeToLive* setting.</span></span> <span data-ttu-id="76190-251">fábrica de dados Olá exclui cluster Olá automaticamente depois que o cluster Olá ficar ocioso por 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="76190-251">hello data factory deletes hello cluster automatically after hello cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="76190-252">Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="76190-252">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="76190-253">HDInsight não exclui esse contêiner quando Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="76190-253">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="76190-254">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="76190-254">This behavior is by design.</span></span> <span data-ttu-id="76190-255">Com o serviço de vinculado do HDInsight sob demanda, um cluster HDInsight é criado sempre que precisa de uma fatia toobe processado a menos que haja um cluster existente de ao vivo (**timeToLive**) e é excluído quando Olá processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="76190-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>

<span data-ttu-id="76190-256">Confira [Serviço vinculado do HDInsight sob demanda](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="76190-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76190-257">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="76190-258">Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="76190-258">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="76190-259">nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="76190-259">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="76190-260">Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="76190-261">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="76190-261">Azure blob input dataset</span></span>
<span data-ttu-id="76190-262">Na definição de conjunto de dados de entrada hello, você deve especificar nomes de saudação do contêiner de blob, a pasta e o arquivo que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="76190-262">In hello input dataset definition, you specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="76190-263">Consulte [propriedades de conjunto de dados de Blob do Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="76190-264">Observe Olá configurações específicas na definição do hello JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="76190-264">Notice hello following specific settings in hello JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="76190-265">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="76190-265">Azure Blob output dataset</span></span>
<span data-ttu-id="76190-266">Na definição de conjunto de dados de saída de hello, você especificar nomes de saudação do contêiner de blob e a pasta que contém os dados de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="76190-266">In hello output dataset definition, you specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="76190-267">Consulte [propriedades de conjunto de dados de Blob do Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="76190-268">Olá folderPath Especifica a pasta de toohello de caminho de saudação que mantém os dados de saída de hello:</span><span class="sxs-lookup"><span data-stu-id="76190-268">hello folderPath specifies hello path toohello folder that holds hello output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="76190-269">Olá [conjunto de dados disponibilidade](../data-factory/data-factory-create-datasets.md#dataset-availability) configuração é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="76190-269">hello [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="76190-270">Fábrica de dados do Azure, saída do pipeline de saudação de unidades de disponibilidade de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="76190-270">In Azure Data Factory, output dataset availability drives hello pipeline.</span></span> <span data-ttu-id="76190-271">Neste exemplo, a fatia de saudação é produzida mensal no Olá último dia do mês (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="76190-271">In this example, hello slice is produced monthly on hello last day of month (EndOfInterval).</span></span> <span data-ttu-id="76190-272">Para saber mais, confira [Agendamento e execução do Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="76190-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="76190-273">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="76190-273">Data pipeline</span></span>
<span data-ttu-id="76190-274">Você define um pipeline que transforma dados executando o script Hive em um cluster do Azure HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="76190-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="76190-275">Consulte [JSON de Pipeline](../data-factory/data-factory-create-pipelines.md#pipeline-json) para obter descrições dos elementos usados de JSON toodefine um pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="76190-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span>

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="76190-276">pipeline de saudação contém uma atividade, atividade de HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="76190-276">hello pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="76190-277">Como as datas de início e término são em janeiro de 2016, os dados de apenas um mês (uma fatia) são processados.</span><span class="sxs-lookup"><span data-stu-id="76190-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="76190-278">Ambos *iniciar* e *final* de atividade de saudação têm uma data passada, portanto Olá fábrica de dados processa os dados para o mês de saudação imediatamente.</span><span class="sxs-lookup"><span data-stu-id="76190-278">Both *start* and *end* of hello activity have a past date, so hello Data Factory processes data for hello month immediately.</span></span> <span data-ttu-id="76190-279">Se a fim de saudação é uma data futura, fábrica de dados Olá cria outra fatia quando chegar a hora da saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-279">If hello end is a future date, hello data factory creates another slice when hello time comes.</span></span> <span data-ttu-id="76190-280">Para saber mais, confira [Agendamento e execução do Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="76190-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-hello-tutorial"></a><span data-ttu-id="76190-281">Limpar tutorial Olá</span><span class="sxs-lookup"><span data-stu-id="76190-281">Clean up hello tutorial</span></span>

### <a name="delete-hello-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="76190-282">Exclua os contêineres de blob Olá criados pelo cluster do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="76190-282">Delete hello blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="76190-283">Com o serviço de vinculado do HDInsight sob demanda, um cluster HDInsight é criado sempre que precisa de uma fatia toobe processado a menos que haja um cluster existente ao vivo (timeToLive); e cluster Olá é excluído quando Olá processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="76190-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (timeToLive); and hello cluster is deleted when hello processing is done.</span></span> <span data-ttu-id="76190-284">Para cada cluster, o Azure Data Factory cria um contêiner de blob no hello usado como conta de armazenamento padrão Olá para cluster Olá de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-284">For each cluster, Azure Data Factory creates a blob container in hello Azure blob storage used as hello default stroage account for hello cluster.</span></span> <span data-ttu-id="76190-285">Mesmo que o cluster HDInsight é excluído, contêiner de armazenamento de blob saudação padrão e a conta de armazenamento de saudação associada não são excluídos.</span><span class="sxs-lookup"><span data-stu-id="76190-285">Even though HDInsight cluster is deleted, hello default blob storage container and hello associated storage account are not deleted.</span></span> <span data-ttu-id="76190-286">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="76190-286">This behavior is by design.</span></span> <span data-ttu-id="76190-287">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="76190-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="76190-288">Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="76190-288">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="76190-289">nomes de saudação desses contêineres seguem um padrão: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="76190-289">hello names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="76190-290">Excluir Olá **adfjobs** e **adfyourdatafactoryname-linkedservicename-datetimestamp** pastas.</span><span class="sxs-lookup"><span data-stu-id="76190-290">Delete hello **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="76190-291">contêiner de adfjobs Olá contém logs de trabalho do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76190-291">hello adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-hello-resource-group"></a><span data-ttu-id="76190-292">Excluir grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="76190-292">Delete hello resource group</span></span>
<span data-ttu-id="76190-293">[Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md) é usado toodeploy, gerenciar e monitorar sua solução como um grupo.</span><span class="sxs-lookup"><span data-stu-id="76190-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used toodeploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="76190-294">Excluir um grupo de recursos exclui todos os componentes de Olá Olá grupo.</span><span class="sxs-lookup"><span data-stu-id="76190-294">Deleting a resource group deletes all hello components inside hello group.</span></span>  

1. <span data-ttu-id="76190-295">Logon toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="76190-295">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="76190-296">Clique em **grupos de recursos** no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-296">Click **Resource groups** on hello left pane.</span></span>
3. <span data-ttu-id="76190-297">Clique no nome de grupo de recursos Olá criado em seu script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="76190-297">Click hello resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="76190-298">Use o filtro de saudação se você tiver muitos grupos de recursos listados.</span><span class="sxs-lookup"><span data-stu-id="76190-298">Use hello filter if you have too many resource groups listed.</span></span> <span data-ttu-id="76190-299">Ele abre o grupo de recursos de saudação em uma nova folha.</span><span class="sxs-lookup"><span data-stu-id="76190-299">It opens hello resource group in a new blade.</span></span>
4. <span data-ttu-id="76190-300">Em Olá **recursos** lado a lado, você deverá ter conta de armazenamento padrão hello e Olá data factory listado, a menos que você compartilhar o grupo de recursos de saudação com outros projetos.</span><span class="sxs-lookup"><span data-stu-id="76190-300">On hello **Resources** tile, you shall have hello default storage account and hello data factory listed unless you share hello resource group with other projects.</span></span>
5. <span data-ttu-id="76190-301">Clique em **excluir** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-301">Click **Delete** on hello top of hello blade.</span></span> <span data-ttu-id="76190-302">Isso exclui a conta de armazenamento hello e dados de Olá armazenados na conta de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-302">Doing so deletes hello storage account and hello data stored in hello storage account.</span></span>
6. <span data-ttu-id="76190-303">Insira a exclusão de tooconfirm nome do grupo de recursos hello e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="76190-303">Enter hello resource group name tooconfirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="76190-304">Caso você não quiser conta de armazenamento toodelete hello quando você excluir o grupo de recursos hello, considere Olá seguir arquitetura separando dados de negócios Olá Olá padrão da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="76190-304">In case you don't want toodelete hello storage account when you delete hello resource group, consider hello following architecture by separating hello business data from hello default storage account.</span></span> <span data-ttu-id="76190-305">Nesse caso, ter um grupo de recursos para conta de armazenamento Olá com dados de negócios hello e Olá outro grupo de recursos para conta de armazenamento padrão Olá HDInsight vinculado hello e serviço de fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="76190-305">In this case, you have one resource group for hello storage account with hello business data, and hello other resource group for hello default storage account for HDInsight linked service and hello data factory.</span></span> <span data-ttu-id="76190-306">Quando você exclui um segundo grupo de recursos hello, ele não afeta o conta de armazenamento de dados de negócios de saudação.</span><span class="sxs-lookup"><span data-stu-id="76190-306">When you delete hello second resource group, it does not impact hello business data storage account.</span></span> <span data-ttu-id="76190-307">toodo para:</span><span class="sxs-lookup"><span data-stu-id="76190-307">toodo so:</span></span>

* <span data-ttu-id="76190-308">Adicione Olá toohello grupo de recursos de nível superior com hello Microsoft.DataFactory/datafactories recursos em seu modelo do Gerenciador de recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="76190-308">Add hello following toohello top-level resource group along with hello Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="76190-309">Ele cria uma conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="76190-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="76190-310">Adicione uma novo serviço vinculado toohello de ponto de nova conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="76190-310">Add a new linked service point toohello new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="76190-311">Configure Olá HDInsight sob demanda vinculado serviço com um dependsOn adicional e um additionalLinkedServiceNames:</span><span class="sxs-lookup"><span data-stu-id="76190-311">Configure hello HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="76190-312">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="76190-312">Next steps</span></span>
<span data-ttu-id="76190-313">Neste artigo, você aprendeu como toouse toocreate de fábrica de dados do Azure sob demanda HDInsight cluster tooprocess trabalhos Hive.</span><span class="sxs-lookup"><span data-stu-id="76190-313">In this article, you have learned how toouse Azure Data Factory toocreate on-demand HDInsight cluster tooprocess Hive jobs.</span></span> <span data-ttu-id="76190-314">tooread mais:</span><span class="sxs-lookup"><span data-stu-id="76190-314">tooread more:</span></span>

* [<span data-ttu-id="76190-315">Tutorial do Hadoop: introdução ao uso do Hadoop baseado em Linux no HDInsight</span><span class="sxs-lookup"><span data-stu-id="76190-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="76190-316">Criar clusters Hadoop baseados em Linux em HDInsight</span><span class="sxs-lookup"><span data-stu-id="76190-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="76190-317">Documentação do HDInsight</span><span class="sxs-lookup"><span data-stu-id="76190-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="76190-318">Documentação do data factory</span><span class="sxs-lookup"><span data-stu-id="76190-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="76190-319">Apêndice</span><span class="sxs-lookup"><span data-stu-id="76190-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="76190-320">Script da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="76190-320">Azure CLI script</span></span>
<span data-ttu-id="76190-321">Você pode usar a CLI do Azure em vez de usar o tutorial do Azure PowerShell toodo hello.</span><span class="sxs-lookup"><span data-stu-id="76190-321">You can use Azure CLI instead of using Azure PowerShell toodo hello tutorial.</span></span> <span data-ttu-id="76190-322">toouse CLI do Azure, primeiro instale CLI do Azure de acordo com a saudação instruções a seguir:</span><span class="sxs-lookup"><span data-stu-id="76190-322">toouse Azure CLI, first install Azure CLI as per hello following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-tooprepare-hello-storage-and-copy-hello-files"></a><span data-ttu-id="76190-323">Usar o armazenamento do Azure CLI tooprepare hello e copiar arquivos de saudação</span><span class="sxs-lookup"><span data-stu-id="76190-323">Use Azure CLI tooprepare hello storage and copy hello files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="76190-324">nome de contêiner de saudação é *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="76190-324">hello container name is *adfgetstarted*.</span></span> <span data-ttu-id="76190-325">Mantenha-o como está.</span><span class="sxs-lookup"><span data-stu-id="76190-325">Keep it as it is.</span></span> <span data-ttu-id="76190-326">Caso contrário, será necessário o modelo do tooupdate Olá Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="76190-326">Otherwise you need tooupdate hello Resource Manager template.</span></span> <span data-ttu-id="76190-327">Se você precisar de ajuda com esse script CLI, consulte [hello usando a CLI do Azure com o armazenamento do Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="76190-327">If you need help with this CLI script, see [Using hello Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
