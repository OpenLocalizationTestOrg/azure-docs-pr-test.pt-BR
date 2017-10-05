---
title: "Carregar grandes quantidades de dados no Data Lake Store usando métodos offline | Microsoft Docs"
description: Usar a ferramenta AdlCopy para copiar dados dos Azure Storage Blobs para o Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 45321f6a-179f-4ee4-b8aa-efa7745b8eb6
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: b469c0ebe9838a1ea986cff3043e3008941e9aa9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-importexport-service-for-offline-copy-of-data-to-data-lake-store"></a><span data-ttu-id="25c77-103">Usar o Serviço de Importação/Exportação do Azure para uma cópia offline dos dados para o Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="25c77-103">Use the Azure Import/Export service for offline copy of data to Data Lake Store</span></span>
<span data-ttu-id="25c77-104">Nesse artigo, você aprenderá a copiar grandes conjuntos de dados (> 200 GB) para um Azure Data Lake Store usando métodos de cópia offline, como o [Serviço de Importação/Exportação do Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="25c77-104">In this article, you'll learn how to copy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like the [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="25c77-105">Especificamente, o arquivo usado como exemplo nesse artigo tem 339.420.860.416 bytes, ou aproximadamente 319 GB em disco.</span><span class="sxs-lookup"><span data-stu-id="25c77-105">Specifically, the file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="25c77-106">Vamos chamar esse arquivo de 319GB.tsv.</span><span class="sxs-lookup"><span data-stu-id="25c77-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="25c77-107">O Serviço de Importação/Exportação do Azure ajuda você a transferir com segurança grandes quantidades de dados para o Armazenamento de Blobs do Azure por meio do envio de unidades de disco rígido para um data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="25c77-107">The Azure Import/Export service helps you to transfer large amounts of data more securely to Azure Blob storage by shipping hard disk drives to an Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25c77-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="25c77-108">Prerequisites</span></span>
<span data-ttu-id="25c77-109">Antes de começar, você deverá ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="25c77-109">Before you begin, you must have the following:</span></span>

* <span data-ttu-id="25c77-110">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="25c77-110">**An Azure subscription**.</span></span> <span data-ttu-id="25c77-111">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="25c77-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="25c77-112">**Uma conta de armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="25c77-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="25c77-113">**Uma conta do repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="25c77-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="25c77-114">Para obter instruções sobre como criar uma, consulte [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="25c77-114">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-the-data"></a><span data-ttu-id="25c77-115">Preparando os dados</span><span class="sxs-lookup"><span data-stu-id="25c77-115">Preparing the data</span></span>
<span data-ttu-id="25c77-116">Antes de usar o serviço de Importação/Exportação, divida o arquivo de dados a ser transferido **em cópias de menos de 200 GB** de tamanho.</span><span class="sxs-lookup"><span data-stu-id="25c77-116">Before using the Import/Export service, break the data file to be transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="25c77-117">A ferramenta de importação não funciona em arquivos com mais de 200 GB.</span><span class="sxs-lookup"><span data-stu-id="25c77-117">The import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="25c77-118">Nesse tutorial, vamos dividir o arquivo em blocos de 100 GB.</span><span class="sxs-lookup"><span data-stu-id="25c77-118">In this tutorial, we split the file into chunks of 100 GB each.</span></span> <span data-ttu-id="25c77-119">Você pode fazer isso usando o [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="25c77-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="25c77-120">O Cygwin dá suporte a comandos do Linux.</span><span class="sxs-lookup"><span data-stu-id="25c77-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="25c77-121">Nesse caso, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="25c77-121">In this case, use the following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="25c77-122">A operação de divisão cria arquivos com os nomes a seguir.</span><span class="sxs-lookup"><span data-stu-id="25c77-122">The split operation creates files with the following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="25c77-123">Prepare os discos com dados</span><span class="sxs-lookup"><span data-stu-id="25c77-123">Get disks ready with data</span></span>
<span data-ttu-id="25c77-124">Siga as instruções em [Usando o serviço de Importação/Exportação do Azure](../storage/common/storage-import-export-service.md) (na seção **Preparar suas unidades**) para preparar seus discos rígidos.</span><span class="sxs-lookup"><span data-stu-id="25c77-124">Follow the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Prepare your drives** section) to prepare your hard drives.</span></span> <span data-ttu-id="25c77-125">Aqui está a sequência geral:</span><span class="sxs-lookup"><span data-stu-id="25c77-125">Here's the overall sequence:</span></span>

1. <span data-ttu-id="25c77-126">Compre um disco rígido que atenda ao requisito para ser usado no serviço de Importação/Exportação do Azure.</span><span class="sxs-lookup"><span data-stu-id="25c77-126">Procure a hard disk that meets the requirement to be used for the Azure Import/Export service.</span></span>
2. <span data-ttu-id="25c77-127">Identifique uma conta de armazenamento do Azure na qual os dados serão copiados depois que forem enviados para o data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="25c77-127">Identify an Azure storage account where the data will be copied after it is shipped to the Azure datacenter.</span></span>
3. <span data-ttu-id="25c77-128">Use a [Ferramenta de Importação/Exportação do Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), um utilitário de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="25c77-128">Use the [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="25c77-129">Aqui está um trecho de código que mostra como usar a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="25c77-129">Here's a sample snippet that shows how to use the tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="25c77-130">Confira [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (Usando o serviço de Importação/Exportação do Azure) para obter mais trechos de código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="25c77-130">See [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="25c77-131">O comando anterior cria um arquivo de diário no local especificado.</span><span class="sxs-lookup"><span data-stu-id="25c77-131">The preceding command creates a journal file at the specified location.</span></span> <span data-ttu-id="25c77-132">Use esse arquivo de diário para criar um trabalho de importação do [Portal Clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="25c77-132">Use this journal file to create an import job from the [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="25c77-133">Criar um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="25c77-133">Create an import job</span></span>
<span data-ttu-id="25c77-134">Agora, você pode criar um trabalho de importação usando as instruções em [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (Usando o serviço de Importação/Exportação do Azure) (na seção **Criar o trabalho de importação**).</span><span class="sxs-lookup"><span data-stu-id="25c77-134">You can now create an import job by using the instructions in [Using the Azure Import/Export service](../storage/common/storage-import-export-service.md) (under the **Create the Import job** section).</span></span> <span data-ttu-id="25c77-135">Para este trabalho de importação, com outros detalhes, também fornece o arquivo de diário criado durante a preparação de unidades de disco.</span><span class="sxs-lookup"><span data-stu-id="25c77-135">For this import job, with other details, also provide the journal file created while preparing the disk drives.</span></span>

## <a name="physically-ship-the-disks"></a><span data-ttu-id="25c77-136">Enviar fisicamente os discos</span><span class="sxs-lookup"><span data-stu-id="25c77-136">Physically ship the disks</span></span>
<span data-ttu-id="25c77-137">Agora, você pode enviar fisicamente os discos para um datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="25c77-137">You can now physically ship the disks to an Azure datacenter.</span></span> <span data-ttu-id="25c77-138">Lá, os dados são copiados nos Azure Storage Blobs que você forneceu ao criar o trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="25c77-138">There, the data is copied over to the Azure Storage blobs you provided while creating the import job.</span></span> <span data-ttu-id="25c77-139">Além disso, ao criar o trabalho, se tiver optado por fornecer as informações de acompanhamento posteriormente, agora você poderá voltar ao trabalho de importação e atualizar o número de controle.</span><span class="sxs-lookup"><span data-stu-id="25c77-139">Also, while creating the job, if you opted to provide the tracking information later, you can now go back to your import job and update the tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-to-azure-data-lake-store"></a><span data-ttu-id="25c77-140">Copiar dados dos Azure Storage Blobs para o Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="25c77-140">Copy data from Azure Storage blobs to Azure Data Lake Store</span></span>
<span data-ttu-id="25c77-141">Depois que o status do trabalho de importação tiver sido concluído, você poderá verificar se os dados estão disponíveis nos Azure Storage Blobs especificados.</span><span class="sxs-lookup"><span data-stu-id="25c77-141">After the status of the import job shows that it's completed, you can verify whether the data is available in the Azure Storage blobs you had specified.</span></span> <span data-ttu-id="25c77-142">Em seguida, você poderá usar uma variedade de métodos para mover esses dados dos blobs para o Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="25c77-142">You can then use a variety of methods to move that data from the blobs to Azure Data Lake Store.</span></span> <span data-ttu-id="25c77-143">Para todas as opções disponíveis para carregamento de dados, consulte [Ingerindo dados no Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="25c77-143">For all the available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="25c77-144">Nesta seção, fornecemos as definições de JSON que você pode usar para criar um pipeline do Azure Data Factory para copiar dados.</span><span class="sxs-lookup"><span data-stu-id="25c77-144">In this section, we provide you with the JSON definitions that you can use to create an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="25c77-145">Você pode usar essas definições de JSON do [Portal do Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), do [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md) ou do [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="25c77-145">You can use these JSON definitions from the [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="25c77-146">Serviço vinculado de origem (Azure Storage Blob)</span><span class="sxs-lookup"><span data-stu-id="25c77-146">Source linked service (Azure Storage blob)</span></span>
````
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
````

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="25c77-147">Serviço vinculado de destino (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="25c77-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' to allow this data factory and the activities it runs to access this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from the OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="25c77-148">Conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="25c77-148">Input data set</span></span>
````
{
    "name": "InputDataSet",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "importcontainer/vf1/"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
````
### <a name="output-data-set"></a><span data-ttu-id="25c77-149">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="25c77-149">Output data set</span></span>
````
{
"name": "OutputDataSet",
"properties": {
  "published": false,
  "type": "AzureDataLakeStore",
  "linkedServiceName": "AzureDataLakeStoreLinkedService",
  "typeProperties": {
    "folderPath": "/importeddatafeb8job/"
    },
  "availability": {
    "frequency": "Hour",
    "interval": 1
    }
  }
}
````
### <a name="pipeline-copy-activity"></a><span data-ttu-id="25c77-150">Pipeline (atividade de cópia)</span><span class="sxs-lookup"><span data-stu-id="25c77-150">Pipeline (copy activity)</span></span>
````
{
    "name": "CopyImportedData",
    "properties": {
        "description": "Pipeline with copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "AzureDataLakeStoreSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity"
            }
        ],
        "start": "2016-02-08T22:00:00Z",
        "end": "2016-02-08T23:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
````
<span data-ttu-id="25c77-151">Para obter mais informações, confira [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) (Mover dados do Azure Storage Blob para o Azure Data Lake Store usando o Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="25c77-151">For more information, see [Move data from Azure Storage blob to Azure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-the-data-files-in-azure-data-lake-store"></a><span data-ttu-id="25c77-152">Reconstruir os arquivos de dados no Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="25c77-152">Reconstruct the data files in Azure Data Lake Store</span></span>
<span data-ttu-id="25c77-153">Começamos com um arquivo que tinha 319 GB e o dividimos em arquivos de tamanho menor, para que eles pudessem ser transferidos usando o serviço de Importação/Exportação do Azure.</span><span class="sxs-lookup"><span data-stu-id="25c77-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using the Azure Import/Export service.</span></span> <span data-ttu-id="25c77-154">Agora que os dados estão no Azure Data Lake Store, podemos reconstruir o arquivo para o seu tamanho original.</span><span class="sxs-lookup"><span data-stu-id="25c77-154">Now that the data is in Azure Data Lake Store, we can reconstruct the file to its original size.</span></span> <span data-ttu-id="25c77-155">Você pode usar os seguintes cmdlets do Azure PowerShell para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="25c77-155">You can use the following Azure PowerShell cmldts to do so.</span></span>

````
# Login to our account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch to the subscription you want to work with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  the files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="25c77-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25c77-156">Next steps</span></span>
* [<span data-ttu-id="25c77-157">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="25c77-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="25c77-158">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="25c77-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="25c77-159">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="25c77-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
