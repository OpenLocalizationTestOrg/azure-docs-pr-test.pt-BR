---
title: "Criar clusters Hadoop sob demanda usando o Data Factory – Azure HDInsight | Microsoft Docs"
description: Saiba como criar clusters Hadoop sob demanda usando o Azure Data Factory.
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
ms.openlocfilehash: e68f1d72965d9516e0552c84d03d234c21739390
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="01fc9-103">Criar clusters Hadoop sob demanda usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="01fc9-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="01fc9-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) é um serviço de integração de dados baseado em nuvem que orquestra e automatiza a movimentação e a transformação dos dados.</span><span class="sxs-lookup"><span data-stu-id="01fc9-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="01fc9-105">Ele pode criar um cluster HDInsight Hadoop just-in-time para processar uma fatia de entrada de dados e excluir o cluster quando o processamento for concluído.</span><span class="sxs-lookup"><span data-stu-id="01fc9-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="01fc9-106">Estes são alguns dos benefícios do uso de um cluster HDInsight Hadoop sob demanda:</span><span class="sxs-lookup"><span data-stu-id="01fc9-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="01fc9-107">Você só paga pelo tempo em que o trabalho está em execução no cluster HDInsight Hadoop (além de um curto período ocioso configurável).</span><span class="sxs-lookup"><span data-stu-id="01fc9-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="01fc9-108">A cobrança dos clusters do HDInsight será proporcional por minuto, independentemente de eles estarem sendo usados ou não.</span><span class="sxs-lookup"><span data-stu-id="01fc9-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="01fc9-109">Quando você usa um serviço vinculado do HDInsight sob demanda no Data Factory, os clusters são criados sob demanda.</span><span class="sxs-lookup"><span data-stu-id="01fc9-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="01fc9-110">E os clusters são excluídos automaticamente após a conclusão dos trabalhos.</span><span class="sxs-lookup"><span data-stu-id="01fc9-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="01fc9-111">Portanto, você paga apenas pelo tempo de execução do trabalho e pelo tempo ocioso breve (configuração de vida útil).</span><span class="sxs-lookup"><span data-stu-id="01fc9-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span>
- <span data-ttu-id="01fc9-112">Você pode criar um fluxo de trabalho usando um pipeline do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="01fc9-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="01fc9-113">Por exemplo, você pode ter o pipeline para copiar dados de um SQL Server local para um armazenamento de blobs do Azure, processar os dados executando um script Hive e um script Pig em um cluster Hadoop do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="01fc9-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="01fc9-114">Em seguida, copie os dados de resultado para um Azure SQL Data Warehouse para que aplicativos de BI o consumam.</span><span class="sxs-lookup"><span data-stu-id="01fc9-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="01fc9-115">Você pode agendar o fluxo de trabalho para ser executado periodicamente (por hora, diariamente, semanalmente, mensalmente etc.).</span><span class="sxs-lookup"><span data-stu-id="01fc9-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="01fc9-116">No Azure Data Factory, um data factory pode ter um ou mais pipelines de dados.</span><span class="sxs-lookup"><span data-stu-id="01fc9-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="01fc9-117">Um pipeline de dados tem uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="01fc9-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="01fc9-118">Há dois tipos de atividades: [Atividades de Movimentação de Dados](../data-factory/data-factory-data-movement-activities.md) e [Atividades de Transformação de Dados](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="01fc9-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="01fc9-119">Você pode usar as atividades de movimentação de dados (atualmente, apenas Copiar Atividade) para mover dados de um repositório de dados de origem para um repositório de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="01fc9-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="01fc9-120">Você pode usar as atividades de transformação de dados para transformar/processar dados.</span><span class="sxs-lookup"><span data-stu-id="01fc9-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="01fc9-121">A atividade do HDInsight Hive é uma das atividades de transformação com suporte pelo Data Factory.</span><span class="sxs-lookup"><span data-stu-id="01fc9-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="01fc9-122">Você pode usar a atividade de transformação do Hive neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="01fc9-122">You use the Hive transformation activity in this tutorial.</span></span>

<span data-ttu-id="01fc9-123">Você pode configurar uma atividade hive para usar seu próprio cluster HDInsight Hadoop ou um cluster HDInsight Hadoop sob demanda.</span><span class="sxs-lookup"><span data-stu-id="01fc9-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="01fc9-124">Neste tutorial, a atividade do Hive no pipeline do data factory é configurada para usar um cluster HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="01fc9-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="01fc9-125">Portanto, quando a atividade é executada para processar uma fatia de dados, aqui está o que acontece:</span><span class="sxs-lookup"><span data-stu-id="01fc9-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span>

1. <span data-ttu-id="01fc9-126">Um cluster Hadoop do HDInsight é criado automaticamente para você just-in-time para processar a fatia.</span><span class="sxs-lookup"><span data-stu-id="01fc9-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="01fc9-127">Os dados de entrada são processados executando um script HiveQL no cluster.</span><span class="sxs-lookup"><span data-stu-id="01fc9-127">The input data is processed by running a HiveQL script on the cluster.</span></span>
3. <span data-ttu-id="01fc9-128">O cluster HDInsight Hadoop é excluído depois que o processamento é concluído e o cluster está ocioso pelo período de tempo configurado (configuração timeToLive).</span><span class="sxs-lookup"><span data-stu-id="01fc9-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="01fc9-129">Se a próxima fatia de dados estiver disponível para processamento nesse tempo ocioso timeToLive, o mesmo cluster será usado para processar a fatia.</span><span class="sxs-lookup"><span data-stu-id="01fc9-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  

<span data-ttu-id="01fc9-130">Neste tutorial, o script HiveQL associado à atividade hive executa as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="01fc9-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span>

1. <span data-ttu-id="01fc9-131">Cria uma tabela externa que faz referência a dados de log da Web brutos armazenados em um armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="01fc9-132">Particiona os dados brutos por ano e mês.</span><span class="sxs-lookup"><span data-stu-id="01fc9-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="01fc9-133">Armazena os dados particionados no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-133">Stores the partitioned data in the Azure blob storage.</span></span>

<span data-ttu-id="01fc9-134">Neste tutorial, o script HiveQL associado à atividade hive cria uma tabela externa que faz referência a dados de log da Web brutos armazenados no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="01fc9-135">Veja as linhas de exemplo para cada mês no arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="01fc9-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="01fc9-136">O script HiveQL particiona os dados brutos por ano e mês.</span><span class="sxs-lookup"><span data-stu-id="01fc9-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="01fc9-137">Ele cria três pastas de saída com base na entrada anterior.</span><span class="sxs-lookup"><span data-stu-id="01fc9-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="01fc9-138">Cada pasta contém um arquivo com entradas de cada mês.</span><span class="sxs-lookup"><span data-stu-id="01fc9-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="01fc9-139">Para obter uma lista das atividades de transformação de dados do Data Factory, além da atividade do Hive, confira [Transformar e analisar usando o Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="01fc9-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="01fc9-140">No momento, você só pode criar o cluster HDInsight versão 3.2 do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="01fc9-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01fc9-141">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="01fc9-141">Prerequisites</span></span>
<span data-ttu-id="01fc9-142">Antes de começar a seguir as instruções neste artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="01fc9-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="01fc9-143">[Assinatura do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="01fc9-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="01fc9-144">PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="01fc9-145">Preparar a conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="01fc9-145">Prepare storage account</span></span>
<span data-ttu-id="01fc9-146">Você pode usar até três contas de armazenamento neste cenário:</span><span class="sxs-lookup"><span data-stu-id="01fc9-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="01fc9-147">conta de armazenamento padrão para o cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="01fc9-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="01fc9-148">conta de armazenamento para os dados de entrada</span><span class="sxs-lookup"><span data-stu-id="01fc9-148">storage account for the input data</span></span>
- <span data-ttu-id="01fc9-149">conta de armazenamento para os dados de saída</span><span class="sxs-lookup"><span data-stu-id="01fc9-149">storage account for the output data</span></span>

<span data-ttu-id="01fc9-150">Para simplificar o tutorial, você usará uma conta de armazenamento para atender aos três objetivos.</span><span class="sxs-lookup"><span data-stu-id="01fc9-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="01fc9-151">O exemplo de script do Azure PowerShell encontrado nesta seção executa as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="01fc9-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="01fc9-152">Fazer logon no Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-152">Log in to Azure.</span></span>
2. <span data-ttu-id="01fc9-153">Crie um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="01fc9-154">Criar uma conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="01fc9-155">Criar um contêiner de Blob na conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="01fc9-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="01fc9-156">Copiar os dois arquivos a seguir no contêiner de Blob:</span><span class="sxs-lookup"><span data-stu-id="01fc9-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="01fc9-157">Arquivo de dados de entrada: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="01fc9-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="01fc9-158">Script HiveQL: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="01fc9-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="01fc9-159">Os dois arquivos são armazenados em um contêiner de Blob público.</span><span class="sxs-lookup"><span data-stu-id="01fc9-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="01fc9-160">**Para preparar o armazenamento e copiar os arquivos usando o Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="01fc9-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="01fc9-161">Especifique nomes para o grupo de recursos do Azure e a conta de armazenamento do Azure que será criada pelo script.</span><span class="sxs-lookup"><span data-stu-id="01fc9-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="01fc9-162">Anote o **nome do grupo de recursos**, o **nome da conta de armazenamento**, e a **chave da conta de armazenamento** produzidos pelo script.</span><span class="sxs-lookup"><span data-stu-id="01fc9-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="01fc9-163">Você precisa deles na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="01fc9-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
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

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="01fc9-164">Se você precisar de ajuda com o script do PowerShell, confira [Como usar o Azure PowerShell com o Armazenamento do Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="01fc9-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="01fc9-165">Se quiser usar a CLI do Azure em vez disso, confira a seção [Apêndice](#appendix) do script da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="01fc9-166">**Para examinar a conta de armazenamento e o conteúdo**</span><span class="sxs-lookup"><span data-stu-id="01fc9-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="01fc9-167">Entre no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="01fc9-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="01fc9-168">Clique em **Grupos de recursos** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="01fc9-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="01fc9-169">Clique duas vezes no nome do grupo de recursos criado em seu script da CLI ou do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01fc9-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="01fc9-170">Use o filtro se houver muitos grupos de recursos listados.</span><span class="sxs-lookup"><span data-stu-id="01fc9-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="01fc9-171">No bloco **Recursos** , você deverá ter um recurso listado, a menos que compartilhe o grupo de recursos com outros projetos.</span><span class="sxs-lookup"><span data-stu-id="01fc9-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="01fc9-172">Esse recurso é a conta de armazenamento com o nome especificado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="01fc9-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="01fc9-173">Clique no nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="01fc9-173">Click the storage account name.</span></span>
5. <span data-ttu-id="01fc9-174">Clique nos blocos **Blobs** .</span><span class="sxs-lookup"><span data-stu-id="01fc9-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="01fc9-175">Clique no contêiner **adfgetstarted** .</span><span class="sxs-lookup"><span data-stu-id="01fc9-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="01fc9-176">Você verá duas pastas: **inputdata** e **script**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-176">You see two folders: **inputdata** and **script**.</span></span>
7. <span data-ttu-id="01fc9-177">Abra a pasta e verifique os arquivos nas pastas.</span><span class="sxs-lookup"><span data-stu-id="01fc9-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="01fc9-178">O inputdata contém o arquivo input.log com dados de entrada, e a pasta de script contém o arquivo de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="01fc9-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span>

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="01fc9-179">Criar um data factory usando o modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="01fc9-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="01fc9-180">Com a conta de armazenamento, os dados de entrada e o script HiveQL preparados, você está pronto para criar um data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="01fc9-181">Há vários métodos para criar um data factory.</span><span class="sxs-lookup"><span data-stu-id="01fc9-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="01fc9-182">Neste tutorial, você cria um data factory implantando um modelo do Azure Resource Manager usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="01fc9-183">Você também pode implantar um modelo do Resource Manager usando a [CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) e o [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="01fc9-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span> <span data-ttu-id="01fc9-184">Para conferir outros métodos de criação de data factory, consulte [Tutorial: compilar seu primeiro data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="01fc9-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="01fc9-185">Clique na imagem a seguir para entrar no Azure e abra o modelo do Resource Manager no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="01fc9-186">O modelo está localizado em https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="01fc9-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="01fc9-187">Confira a seção [Entidades de Data Factory no modelo](#data-factory-entities-in-the-template) para obter informações detalhadas sobre as entidades definidas no modelo.</span><span class="sxs-lookup"><span data-stu-id="01fc9-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="./media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="01fc9-188">Selecione a opção **Usar existente** para a configuração **Grupo de recursos** e selecione o nome do grupo de recursos que você criou na etapa anterior (usando o script do PowerShell).</span><span class="sxs-lookup"><span data-stu-id="01fc9-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span>
3. <span data-ttu-id="01fc9-189">Insira um nome para o data factory (**Nome do Data Factory**).</span><span class="sxs-lookup"><span data-stu-id="01fc9-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="01fc9-190">Esse nome deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="01fc9-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="01fc9-191">Insira o **nome da conta de armazenamento** e a **chave da conta de armazenamento** que você anotou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="01fc9-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="01fc9-192">Selecione **Concordo com os termos e condições** indicado acima, após a leitura dos **termos e condições**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="01fc9-193">Selecione a opção **Fixar no painel**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-193">Select **Pin to dashboard** option.</span></span>
6. <span data-ttu-id="01fc9-194">Clique em **Comprar/Criar**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="01fc9-195">Você verá um bloco no Painel chamado **Implantação do Modelo de implantação**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="01fc9-196">Aguarde até que a folha de **Grupo de recursos** para seu grupo de recursos seja aberta.</span><span class="sxs-lookup"><span data-stu-id="01fc9-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="01fc9-197">Você também pode clicar no bloco intitulado como o nome do grupo de recursos para abrir a folha de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="01fc9-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span>
6. <span data-ttu-id="01fc9-198">Clique no bloco para abrir o grupo de recursos, se a folha de grupo de recursos ainda não estiver aberta.</span><span class="sxs-lookup"><span data-stu-id="01fc9-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="01fc9-199">Agora, você verá um recurso do data factory listado, além do recurso da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="01fc9-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="01fc9-200">Clique no nome do data factory (valor especificado para o parâmetro **Nome do Data Factory**).</span><span class="sxs-lookup"><span data-stu-id="01fc9-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="01fc9-201">Na folha Data Factory, clique no bloco **Diagrama**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="01fc9-202">O diagrama mostra uma atividade com um conjunto de dados de entrada, e um conjunto de dados de saída:</span><span class="sxs-lookup"><span data-stu-id="01fc9-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Diagrama de pipeline de atividade do hive HDInsight sob demanda do Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="01fc9-204">Os nomes são definidos no modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01fc9-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="01fc9-205">Clique duas vezes em **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="01fc9-206">Nas **Fatias atualizadas recentemente**, você deverá ver uma fatia.</span><span class="sxs-lookup"><span data-stu-id="01fc9-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="01fc9-207">Se o status for **Em andamento**, aguarde até que ele mude para **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="01fc9-208">Normalmente, a criação de um cluster HDInsight demora cerca de **20 minutos**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span>

### <a name="check-the-data-factory-output"></a><span data-ttu-id="01fc9-209">Verificar a saída do data factory</span><span class="sxs-lookup"><span data-stu-id="01fc9-209">Check the data factory output</span></span>

1. <span data-ttu-id="01fc9-210">Use o mesmo procedimento da última sessão para verificar os contêineres do contêiner adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="01fc9-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="01fc9-211">Há dois novos contêineres além de **adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="01fc9-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="01fc9-212">Um contêiner com nome que segue o padrão: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="01fc9-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="01fc9-213">Esse contêiner é o contêiner padrão para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="01fc9-213">This container is the default container for the HDInsight cluster.</span></span>
   * <span data-ttu-id="01fc9-214">adfjobs: esse é o contêiner para os logs do trabalho do ADF.</span><span class="sxs-lookup"><span data-stu-id="01fc9-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="01fc9-215">A saída do data factory é armazenada em **afgetstarted**, conforme configurado no modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01fc9-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="01fc9-216">Clique em **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="01fc9-217">Clique duas vezes em **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="01fc9-218">Você vê uma pasta **ano=2014** , porque todos os logs da Web têm a data de 2014.</span><span class="sxs-lookup"><span data-stu-id="01fc9-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Saída do pipeline de atividade do hive HDInsight sob demanda do Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="01fc9-220">Se você analisar detalhadamente a lista, deverá ver três pastas para janeiro, fevereiro e março.</span><span class="sxs-lookup"><span data-stu-id="01fc9-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="01fc9-221">E há um log para cada mês.</span><span class="sxs-lookup"><span data-stu-id="01fc9-221">And there is a log for each month.</span></span>

    ![Saída do pipeline de atividade do hive HDInsight sob demanda do Azure Data Factory](./media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="01fc9-223">Entidades do Data Factory no modelo</span><span class="sxs-lookup"><span data-stu-id="01fc9-223">Data Factory entities in the template</span></span>
<span data-ttu-id="01fc9-224">Veja a aparência do modelo de nível superior do Resource Manager para um data factory:</span><span class="sxs-lookup"><span data-stu-id="01fc9-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="01fc9-225">Definir Data Factory</span><span class="sxs-lookup"><span data-stu-id="01fc9-225">Define data factory</span></span>
<span data-ttu-id="01fc9-226">Você pode definir um Data Factory no modelo do Resource Manager, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="01fc9-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="01fc9-227">O dataFactoryName é o nome do data factory que você especifica ao implantar o modelo.</span><span class="sxs-lookup"><span data-stu-id="01fc9-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="01fc9-228">Atualmente, o data factory só tem suporte nas regiões leste dos EUA, oeste dos EUA e Europa Setentrional.</span><span class="sxs-lookup"><span data-stu-id="01fc9-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>

### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="01fc9-229">Definindo entidades no data factory</span><span class="sxs-lookup"><span data-stu-id="01fc9-229">Defining entities within the data factory</span></span>
<span data-ttu-id="01fc9-230">As seguintes entidades de Data Factory são definidas no modelo JSON:</span><span class="sxs-lookup"><span data-stu-id="01fc9-230">The following Data Factory entities are defined in the JSON template:</span></span>

* [<span data-ttu-id="01fc9-231">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="01fc9-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="01fc9-232">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="01fc9-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="01fc9-233">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="01fc9-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="01fc9-234">Conjunto de dados de saída do blob do Azure</span><span class="sxs-lookup"><span data-stu-id="01fc9-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="01fc9-235">Pipeline com a Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="01fc9-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="01fc9-236">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="01fc9-236">Azure Storage linked service</span></span>
<span data-ttu-id="01fc9-237">O serviço vinculado ao Armazenamento do Azure vincula sua conta de armazenamento do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="01fc9-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="01fc9-238">Neste tutorial, a mesma conta de armazenamento é usada como a conta de armazenamento do HDInsight padrão, o armazenamento de dados de entrada e o armazenamento de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="01fc9-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="01fc9-239">Portanto, você define somente um serviço vinculado do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="01fc9-240">Na definição de serviço vinculado, você pode especificar o nome e a chave da conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="01fc9-241">Confira [Serviço vinculado de armazenamento do Azure](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre os elementos JSON para definir um serviço vinculado de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>

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
<span data-ttu-id="01fc9-242">A **connectionString** usa os parâmetros storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="01fc9-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="01fc9-243">Você pode especificar valores para esses parâmetros durante a implantação do modelo.</span><span class="sxs-lookup"><span data-stu-id="01fc9-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="01fc9-244">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="01fc9-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="01fc9-245">Na definição do serviço HDInsight vinculado sob demanda, você deve especificar valores para parâmetros de configuração que são usados pelo serviço Data Factory para criar um cluster HDInsight Hadoop em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="01fc9-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="01fc9-246">Confira o artigo [Serviços vinculados de computação](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes sobre as propriedades JSON usadas para definir um serviço vinculado do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="01fc9-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="01fc9-247">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="01fc9-247">Note the following points:</span></span>

* <span data-ttu-id="01fc9-248">O Data Factory cria um cluster HDInsight **baseado em Linux** para você.</span><span class="sxs-lookup"><span data-stu-id="01fc9-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="01fc9-249">O cluster HDInsight Hadoop é criado na mesma região que a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="01fc9-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="01fc9-250">Perceba a configuração *timeToLive* .</span><span class="sxs-lookup"><span data-stu-id="01fc9-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="01fc9-251">O data factory exclui o cluster automaticamente após ele ficar ocioso por 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="01fc9-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="01fc9-252">O cluster HDInsight cria um **contêiner padrão** no armazenamento de blobs especificado no JSON (**nomeServiçoVinculado**).</span><span class="sxs-lookup"><span data-stu-id="01fc9-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="01fc9-253">O HDInsight não exclui esse contêiner quando o cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="01fc9-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="01fc9-254">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="01fc9-254">This behavior is by design.</span></span> <span data-ttu-id="01fc9-255">Com o serviço vinculado HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia precisa ser processada, a menos que haja um cluster ativo existente (**timeToLive**), e é excluído quando o processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="01fc9-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="01fc9-256">Confira [Serviço vinculado do HDInsight sob demanda](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="01fc9-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01fc9-257">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="01fc9-258">Se você não precisa deles para solução de problemas dos trabalhos, convém excluí-los para reduzir o custo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="01fc9-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="01fc9-259">Os nomes desses contêineres seguem um padrão: "adf**nomeseudatafactory**-**nomeserviçovinculado**- carimbodatahora".</span><span class="sxs-lookup"><span data-stu-id="01fc9-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="01fc9-260">Use ferramentas como o [Gerenciador de Armazenamento da Microsoft](http://storageexplorer.com/) para excluir contêineres do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="01fc9-261">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="01fc9-261">Azure blob input dataset</span></span>
<span data-ttu-id="01fc9-262">Na definição de conjunto de dados de entrada, você especifica os nomes do contêiner de blob, da pasta e do arquivo que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="01fc9-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="01fc9-263">Confira [Propriedades de conjunto de dados de Blob do Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre os propriedades JSON usadas para definir um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>

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

<span data-ttu-id="01fc9-264">Observe as seguintes configurações específicas na definição de JSON:</span><span class="sxs-lookup"><span data-stu-id="01fc9-264">Notice the following specific settings in the JSON definition:</span></span>

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="01fc9-265">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="01fc9-265">Azure Blob output dataset</span></span>
<span data-ttu-id="01fc9-266">Na definição de conjunto de dados de saída, especifique os nomes de contêiner de blob e a pasta que contém os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="01fc9-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="01fc9-267">Confira [Propriedades de conjunto de dados de Blob do Azure](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre os propriedades JSON usadas para definir um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="01fc9-268">FolderPath especifica o caminho para a pasta que contém os dados de saída:</span><span class="sxs-lookup"><span data-stu-id="01fc9-268">The folderPath specifies the path to the folder that holds the output data:</span></span>

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="01fc9-269">A configuração [disponibilidade do conjunto de dados](../data-factory/data-factory-create-datasets.md#dataset-availability) é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="01fc9-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#dataset-availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="01fc9-270">No Azure Data Factory, a disponibilidade do conjunto de dados de saída conduz o pipeline.</span><span class="sxs-lookup"><span data-stu-id="01fc9-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="01fc9-271">Neste exemplo, a fatia é produzida mensalmente no último dia do mês (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="01fc9-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="01fc9-272">Para saber mais, confira [Agendamento e execução do Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="01fc9-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="01fc9-273">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="01fc9-273">Data pipeline</span></span>
<span data-ttu-id="01fc9-274">Você define um pipeline que transforma dados executando o script Hive em um cluster do Azure HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="01fc9-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="01fc9-275">Confira [JSON de Pipeline](../data-factory/data-factory-create-pipelines.md#pipeline-json) para obter descrições dos elementos JSON usados para definir um pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="01fc9-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span>

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

<span data-ttu-id="01fc9-276">O pipeline contém uma atividade, a atividade HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="01fc9-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="01fc9-277">Como as datas de início e término são em janeiro de 2016, os dados de apenas um mês (uma fatia) são processados.</span><span class="sxs-lookup"><span data-stu-id="01fc9-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="01fc9-278">O *início* e o *término* da atividade têm uma data passada; portanto, o Data Factory processa os dados para o mês imediatamente.</span><span class="sxs-lookup"><span data-stu-id="01fc9-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="01fc9-279">Se o valor de fim for uma data futura, o data factory cria outra fatia quando chegar o momento.</span><span class="sxs-lookup"><span data-stu-id="01fc9-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="01fc9-280">Para saber mais, confira [Agendamento e execução do Data Factory](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="01fc9-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="01fc9-281">Limpar o tutorial</span><span class="sxs-lookup"><span data-stu-id="01fc9-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="01fc9-282">Exclua os contêineres de blob criados pelo cluster HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="01fc9-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="01fc9-283">Com o serviço vinculado HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia precisa ser processada, a menos que haja um cluster ativo existente (timeToLive), e o cluster seja excluído após o processamento.</span><span class="sxs-lookup"><span data-stu-id="01fc9-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="01fc9-284">Para cada cluster, o Azure Data Factory cria um contêiner de blob no armazenamento de blobs do Azure usado como a conta de armazenamento padrão para o cluster.</span><span class="sxs-lookup"><span data-stu-id="01fc9-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="01fc9-285">Mesmo que o cluster HDInsight seja excluído, o contêiner de armazenamento de blobs padrão e a conta de armazenamento associados não serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="01fc9-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="01fc9-286">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="01fc9-286">This behavior is by design.</span></span> <span data-ttu-id="01fc9-287">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="01fc9-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="01fc9-288">Se você não precisa deles para solução de problemas dos trabalhos, convém excluí-los para reduzir o custo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="01fc9-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="01fc9-289">Os nomes desses contêineres seguem um padrão: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="01fc9-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="01fc9-290">Exclua as pastas **adfjobs** e **adfyourdatafactoryname-linkedservicename-datetimestamp**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="01fc9-291">O contêiner adfjobs contém logs de trabalho do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="01fc9-291">The adfjobs container contains job logs from Azure Data Factory.</span></span>

### <a name="delete-the-resource-group"></a><span data-ttu-id="01fc9-292">Exclua o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="01fc9-292">Delete the resource group</span></span>
<span data-ttu-id="01fc9-293">O [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) é usado para implantar, gerenciar e monitorar sua solução como um grupo.</span><span class="sxs-lookup"><span data-stu-id="01fc9-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="01fc9-294">A exclusão de um grupo de recursos exclui todos os componentes dentro do grupo.</span><span class="sxs-lookup"><span data-stu-id="01fc9-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="01fc9-295">Entre no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="01fc9-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="01fc9-296">Clique em **Grupos de recursos** no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="01fc9-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="01fc9-297">Clique no nome do grupo de recursos criado em seu script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01fc9-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="01fc9-298">Use o filtro se houver muitos grupos de recursos listados.</span><span class="sxs-lookup"><span data-stu-id="01fc9-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="01fc9-299">Ele abre o grupo de recursos em uma nova folha.</span><span class="sxs-lookup"><span data-stu-id="01fc9-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="01fc9-300">No bloco **Recursos** , a conta de armazenamento padrão e o data factory deverão estar listados, a menos que você compartilhe o grupo de recursos com outros projetos.</span><span class="sxs-lookup"><span data-stu-id="01fc9-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="01fc9-301">Clique em **Excluir** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="01fc9-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="01fc9-302">Isso exclui a conta de armazenamento e os dados armazenados na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="01fc9-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="01fc9-303">Insira o nome do grupo de recursos para confirmar a exclusão e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="01fc9-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="01fc9-304">Caso você não queira excluir a conta de armazenamento ao excluir o grupo de recursos, considere a seguinte arquitetura, separando os dados de negócio da conta de armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="01fc9-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="01fc9-305">Nesse caso, você tem um grupo de recursos para a conta de armazenamento com os dados de negócio, e outro grupo de recursos para a conta de armazenamento padrão para o serviço vinculado do HDInsight e o data factory.</span><span class="sxs-lookup"><span data-stu-id="01fc9-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="01fc9-306">Quando você exclui o segundo grupo de recursos, ele não afeta a conta de armazenamento de dados de negócios.</span><span class="sxs-lookup"><span data-stu-id="01fc9-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="01fc9-307">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="01fc9-307">To do so:</span></span>

* <span data-ttu-id="01fc9-308">Adicione o seguinte ao grupo de recursos de nível superior, juntamente com o recurso Microsoft.DataFactory/datafactories em seu modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01fc9-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="01fc9-309">Ele cria uma conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="01fc9-309">It creates a storage account:</span></span>

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
* <span data-ttu-id="01fc9-310">Adicione um novo ponto de serviço vinculado à nova conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="01fc9-310">Add a new linked service point to the new storage account:</span></span>

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
* <span data-ttu-id="01fc9-311">Configure o serviço vinculado sob demanda do HDInsight com um dependsOn adicional, e um additionalLinkedServiceNames:</span><span class="sxs-lookup"><span data-stu-id="01fc9-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="01fc9-312">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01fc9-312">Next steps</span></span>
<span data-ttu-id="01fc9-313">Neste artigo, você aprendeu a usar o Azure Data Factory para criar o cluster HDInsight sob demanda, a fim de processar trabalhos de Hive.</span><span class="sxs-lookup"><span data-stu-id="01fc9-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="01fc9-314">Para saber mais:</span><span class="sxs-lookup"><span data-stu-id="01fc9-314">To read more:</span></span>

* [<span data-ttu-id="01fc9-315">Tutorial do Hadoop: introdução ao uso do Hadoop baseado em Linux no HDInsight</span><span class="sxs-lookup"><span data-stu-id="01fc9-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="01fc9-316">Criar clusters Hadoop baseados em Linux em HDInsight</span><span class="sxs-lookup"><span data-stu-id="01fc9-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="01fc9-317">Documentação do HDInsight</span><span class="sxs-lookup"><span data-stu-id="01fc9-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="01fc9-318">Documentação do data factory</span><span class="sxs-lookup"><span data-stu-id="01fc9-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="01fc9-319">Apêndice</span><span class="sxs-lookup"><span data-stu-id="01fc9-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="01fc9-320">Script da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="01fc9-320">Azure CLI script</span></span>
<span data-ttu-id="01fc9-321">Você pode usar a CLI do Azure, em vez de usar o Azure PowerShell, para executar o tutorial.</span><span class="sxs-lookup"><span data-stu-id="01fc9-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="01fc9-322">Para usar a CLI do Azure, primeiro instale a CLI do Azure de acordo com as seguintes instruções:</span><span class="sxs-lookup"><span data-stu-id="01fc9-322">To use Azure CLI, first install Azure CLI as per the following instructions:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="01fc9-323">Usar a CLI do Azure para preparar o armazenamento e copiar os arquivos</span><span class="sxs-lookup"><span data-stu-id="01fc9-323">Use Azure CLI to prepare the storage and copy the files</span></span>

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

<span data-ttu-id="01fc9-324">O nome do contêiner é *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="01fc9-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="01fc9-325">Mantenha-o como está.</span><span class="sxs-lookup"><span data-stu-id="01fc9-325">Keep it as it is.</span></span> <span data-ttu-id="01fc9-326">Caso contrário, é necessário atualizar o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="01fc9-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="01fc9-327">Se você precisar de ajuda com esse script da CLI, confira [Como usar a CLI do Azure com o Armazenamento do Azure](../storage/common/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="01fc9-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/common/storage-azure-cli.md).</span></span>
