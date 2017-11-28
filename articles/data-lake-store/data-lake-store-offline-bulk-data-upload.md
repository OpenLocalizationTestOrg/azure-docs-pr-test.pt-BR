---
title: "grandes quantidades de aaaUpload de dados no repositório Data Lake usando métodos offline | Microsoft Docs"
description: "TooData Lake armazenamento de blobs Olá use dados de toocopy ferramenta AdlCopy do armazenamento do Azure"
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
ms.openlocfilehash: 42ef75142a26ebfab05d89614782a54c244c4bcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-importexport-service-for-offline-copy-of-data-toodata-lake-store"></a><span data-ttu-id="545a2-103">Usar serviço de importação/exportação do Azure Olá para uma cópia offline tooData Lake do repositório de dados</span><span class="sxs-lookup"><span data-stu-id="545a2-103">Use hello Azure Import/Export service for offline copy of data tooData Lake Store</span></span>
<span data-ttu-id="545a2-104">Neste artigo, você aprenderá como dados enorme toocopy define (> 200 GB) em um repositório Azure Data Lake usando métodos de cópia offline, como Olá [serviço de importação/exportação do Azure](../storage/common/storage-import-export-service.md).</span><span class="sxs-lookup"><span data-stu-id="545a2-104">In this article, you'll learn how toocopy huge data sets (>200 GB) into an Azure Data Lake Store by using offline copy methods, like hello [Azure Import/Export service](../storage/common/storage-import-export-service.md).</span></span> <span data-ttu-id="545a2-105">Especificamente, o arquivo hello usado como exemplo neste artigo é 339,420,860,416 bytes ou aproximadamente 319 GB no disco.</span><span class="sxs-lookup"><span data-stu-id="545a2-105">Specifically, hello file used as an example in this article is 339,420,860,416 bytes, or about 319 GB on disk.</span></span> <span data-ttu-id="545a2-106">Vamos chamar esse arquivo de 319GB.tsv.</span><span class="sxs-lookup"><span data-stu-id="545a2-106">Let's call this file 319GB.tsv.</span></span>

<span data-ttu-id="545a2-107">Olá serviço de importação/exportação do Azure ajuda a tootransfer grandes quantidades de dados mais segura tooAzure armazenamento de Blob por disco rígido de envio de unidades tooan datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="545a2-107">hello Azure Import/Export service helps you tootransfer large amounts of data more securely tooAzure Blob storage by shipping hard disk drives tooan Azure datacenter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="545a2-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="545a2-108">Prerequisites</span></span>
<span data-ttu-id="545a2-109">Antes de começar, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="545a2-109">Before you begin, you must have hello following:</span></span>

* <span data-ttu-id="545a2-110">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="545a2-110">**An Azure subscription**.</span></span> <span data-ttu-id="545a2-111">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="545a2-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="545a2-112">**Uma conta de armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="545a2-112">**An Azure storage account**.</span></span>
* <span data-ttu-id="545a2-113">**Uma conta do repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="545a2-113">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="545a2-114">Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="545a2-114">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

## <a name="preparing-hello-data"></a><span data-ttu-id="545a2-115">Preparando dados Olá</span><span class="sxs-lookup"><span data-stu-id="545a2-115">Preparing hello data</span></span>
<span data-ttu-id="545a2-116">Antes de usar o serviço de importação/exportação hello, transferidos quebra Olá dados arquivo toobe **em cópias de menos de 200 GB** em tamanho.</span><span class="sxs-lookup"><span data-stu-id="545a2-116">Before using hello Import/Export service, break hello data file toobe transferred **into copies that are less than 200 GB** in size.</span></span> <span data-ttu-id="545a2-117">ferramenta de importação de saudação não funciona com arquivos com mais de 200 GB.</span><span class="sxs-lookup"><span data-stu-id="545a2-117">hello import tool does not work with files greater than 200 GB.</span></span> <span data-ttu-id="545a2-118">Neste tutorial, dividiremos arquivo hello em partes de 100 GB.</span><span class="sxs-lookup"><span data-stu-id="545a2-118">In this tutorial, we split hello file into chunks of 100 GB each.</span></span> <span data-ttu-id="545a2-119">Você pode fazer isso usando o [Cygwin](https://cygwin.com/install.html).</span><span class="sxs-lookup"><span data-stu-id="545a2-119">You can do this by using [Cygwin](https://cygwin.com/install.html).</span></span> <span data-ttu-id="545a2-120">O Cygwin dá suporte a comandos do Linux.</span><span class="sxs-lookup"><span data-stu-id="545a2-120">Cygwin supports Linux commands.</span></span> <span data-ttu-id="545a2-121">Nesse caso, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="545a2-121">In this case, use hello following command:</span></span>

    split -b 100m 319GB.tsv

<span data-ttu-id="545a2-122">operação de divisão Olá cria arquivos com hello nomes a seguir.</span><span class="sxs-lookup"><span data-stu-id="545a2-122">hello split operation creates files with hello following names.</span></span>

    319GB.tsv-part-aa

    319GB.tsv-part-ab

    319GB.tsv-part-ac

    319GB.tsv-part-ad

## <a name="get-disks-ready-with-data"></a><span data-ttu-id="545a2-123">Prepare os discos com dados</span><span class="sxs-lookup"><span data-stu-id="545a2-123">Get disks ready with data</span></span>
<span data-ttu-id="545a2-124">Siga as instruções de saudação em [usando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) (em Olá **preparar suas unidades** seção) tooprepare seus discos rígidos.</span><span class="sxs-lookup"><span data-stu-id="545a2-124">Follow hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Prepare your drives** section) tooprepare your hard drives.</span></span> <span data-ttu-id="545a2-125">Eis Olá sequência geral:</span><span class="sxs-lookup"><span data-stu-id="545a2-125">Here's hello overall sequence:</span></span>

1. <span data-ttu-id="545a2-126">Obtenha um disco rígido que atenda Olá requisito toobe usado para Olá serviço de importação/exportação do Azure.</span><span class="sxs-lookup"><span data-stu-id="545a2-126">Procure a hard disk that meets hello requirement toobe used for hello Azure Import/Export service.</span></span>
2. <span data-ttu-id="545a2-127">Identifique uma conta de armazenamento do Azure em que dados hello serão copiados depois que ele toohello fornecido datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="545a2-127">Identify an Azure storage account where hello data will be copied after it is shipped toohello Azure datacenter.</span></span>
3. <span data-ttu-id="545a2-128">Saudação de uso [ferramenta de importação/exportação do Azure](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), um utilitário de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="545a2-128">Use hello [Azure Import/Export Tool](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409), a command-line utility.</span></span> <span data-ttu-id="545a2-129">Aqui está um trecho de código de exemplo que mostra como toouse Olá ferramenta.</span><span class="sxs-lookup"><span data-stu-id="545a2-129">Here's a sample snippet that shows how toouse hello tool.</span></span>

    ````
    WAImportExport PrepImport /sk:<StorageAccountKey> /t: <TargetDriveLetter> /format /encrypt /logdir:e:\myexportimportjob\logdir /j:e:\myexportimportjob\journal1.jrn /id:myexportimportjob /srcdir:F:\demo\ExImContainer /dstdir:importcontainer/vf1/
    ````
    <span data-ttu-id="545a2-130">Consulte [usando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) para mais trechos de código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="545a2-130">See [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) for more sample snippets.</span></span>
4. <span data-ttu-id="545a2-131">Olá, comando anterior cria um diário de local do arquivo no hello especificado.</span><span class="sxs-lookup"><span data-stu-id="545a2-131">hello preceding command creates a journal file at hello specified location.</span></span> <span data-ttu-id="545a2-132">Use este arquivo de diário toocreate um trabalho de importação de saudação [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="545a2-132">Use this journal file toocreate an import job from hello [Azure classic portal](https://manage.windowsazure.com).</span></span>

## <a name="create-an-import-job"></a><span data-ttu-id="545a2-133">Criar um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="545a2-133">Create an import job</span></span>
<span data-ttu-id="545a2-134">Agora você pode criar um trabalho de importação usando instruções Olá [usando o serviço de importação/exportação do Azure Olá](../storage/common/storage-import-export-service.md) (em Olá **criar trabalho de importação de saudação** seção).</span><span class="sxs-lookup"><span data-stu-id="545a2-134">You can now create an import job by using hello instructions in [Using hello Azure Import/Export service](../storage/common/storage-import-export-service.md) (under hello **Create hello Import job** section).</span></span> <span data-ttu-id="545a2-135">Para este trabalho de importação, com outros detalhes também fornece Olá diário arquivo criado durante a preparação Olá unidades de disco.</span><span class="sxs-lookup"><span data-stu-id="545a2-135">For this import job, with other details, also provide hello journal file created while preparing hello disk drives.</span></span>

## <a name="physically-ship-hello-disks"></a><span data-ttu-id="545a2-136">Enviar fisicamente os discos de saudação</span><span class="sxs-lookup"><span data-stu-id="545a2-136">Physically ship hello disks</span></span>
<span data-ttu-id="545a2-137">Agora você pode enviar fisicamente Olá discos tooan datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="545a2-137">You can now physically ship hello disks tooan Azure datacenter.</span></span> <span data-ttu-id="545a2-138">Lá, os dados de saudação são copiados em blobs de armazenamento do Azure toohello fornecida ao criar o trabalho de importação de saudação.</span><span class="sxs-lookup"><span data-stu-id="545a2-138">There, hello data is copied over toohello Azure Storage blobs you provided while creating hello import job.</span></span> <span data-ttu-id="545a2-139">Além disso, ao criar o trabalho de hello, se você tiver optado tooprovide hello mais tarde, informações de controle você pode agora voltar produtos de saudação de trabalho e atualização de importação tooyour número de controle.</span><span class="sxs-lookup"><span data-stu-id="545a2-139">Also, while creating hello job, if you opted tooprovide hello tracking information later, you can now go back tooyour import job and update hello tracking number.</span></span>

## <a name="copy-data-from-azure-storage-blobs-tooazure-data-lake-store"></a><span data-ttu-id="545a2-140">Copiar dados do repositório do armazenamento do Azure blobs tooAzure Data Lake</span><span class="sxs-lookup"><span data-stu-id="545a2-140">Copy data from Azure Storage blobs tooAzure Data Lake Store</span></span>
<span data-ttu-id="545a2-141">Depois de status Olá Olá o trabalho de importação mostra que ela é concluída, você pode verificar se os dados de saudação estão disponíveis em blobs de armazenamento do Azure Olá especificadas.</span><span class="sxs-lookup"><span data-stu-id="545a2-141">After hello status of hello import job shows that it's completed, you can verify whether hello data is available in hello Azure Storage blobs you had specified.</span></span> <span data-ttu-id="545a2-142">Você pode usar uma variedade de métodos toomove dados de saudação blobs repositório tooAzure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="545a2-142">You can then use a variety of methods toomove that data from hello blobs tooAzure Data Lake Store.</span></span> <span data-ttu-id="545a2-143">Para todos os hello opções disponíveis para carregamento de dados, consulte [ingestão de dados no repositório Data Lake](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span><span class="sxs-lookup"><span data-stu-id="545a2-143">For all hello available options for uploading data, see [Ingesting data into Data Lake Store](data-lake-store-data-scenarios.md#ingest-data-into-data-lake-store).</span></span>

<span data-ttu-id="545a2-144">Nesta seção, podemos fornecer definições de JSON Olá que você pode usar toocreate um pipeline da fábrica de dados do Azure para copiar dados.</span><span class="sxs-lookup"><span data-stu-id="545a2-144">In this section, we provide you with hello JSON definitions that you can use toocreate an Azure Data Factory pipeline for copying data.</span></span> <span data-ttu-id="545a2-145">Você pode usar essas definições de JSON de saudação [portal do Azure](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), ou [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="545a2-145">You can use these JSON definitions from hello [Azure portal](../data-factory/data-factory-copy-activity-tutorial-using-azure-portal.md), or [Visual Studio](../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](../data-factory/data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

### <a name="source-linked-service-azure-storage-blob"></a><span data-ttu-id="545a2-146">Serviço vinculado de origem (Azure Storage Blob)</span><span class="sxs-lookup"><span data-stu-id="545a2-146">Source linked service (Azure Storage blob)</span></span>
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

### <a name="target-linked-service-azure-data-lake-store"></a><span data-ttu-id="545a2-147">Serviço vinculado de destino (Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="545a2-147">Target linked service (Azure Data Lake Store)</span></span>
````
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "description": "",
        "typeProperties": {
            "authorization": "<Click 'Authorize' tooallow this data factory and hello activities it runs tooaccess this Data Lake Store with your access rights>",
            "dataLakeStoreUri": "https://<adls_account_name>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<OAuth session id from hello OAuth authorization session. Each session id is unique and may only be used once>"
        }
    }
}
````
### <a name="input-data-set"></a><span data-ttu-id="545a2-148">Conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="545a2-148">Input data set</span></span>
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
### <a name="output-data-set"></a><span data-ttu-id="545a2-149">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="545a2-149">Output data set</span></span>
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
### <a name="pipeline-copy-activity"></a><span data-ttu-id="545a2-150">Pipeline (atividade de cópia)</span><span class="sxs-lookup"><span data-stu-id="545a2-150">Pipeline (copy activity)</span></span>
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
<span data-ttu-id="545a2-151">Para obter mais informações, consulte [mover o blob de dados do armazenamento do Azure usando o Azure Data Factory repositório tooAzure Data Lake](../data-factory/data-factory-azure-datalake-connector.md).</span><span class="sxs-lookup"><span data-stu-id="545a2-151">For more information, see [Move data from Azure Storage blob tooAzure Data Lake Store using Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md).</span></span>

## <a name="reconstruct-hello-data-files-in-azure-data-lake-store"></a><span data-ttu-id="545a2-152">Reconstruir os arquivos de dados de saudação no repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="545a2-152">Reconstruct hello data files in Azure Data Lake Store</span></span>
<span data-ttu-id="545a2-153">Começamos com um arquivo que foi 319 GB e rompeu-lo em arquivos de menor tamanho, para que ele foi transferido usando o serviço de importação/exportação do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="545a2-153">We started with a file that was 319 GB, and broke it down into files of smaller size so that it could be transferred by using hello Azure Import/Export service.</span></span> <span data-ttu-id="545a2-154">Agora que os dados de saudação estão no repositório Azure Data Lake, podemos pode reconstruir o tamanho original do arquivo de saudação tooits.</span><span class="sxs-lookup"><span data-stu-id="545a2-154">Now that hello data is in Azure Data Lake Store, we can reconstruct hello file tooits original size.</span></span> <span data-ttu-id="545a2-155">Você pode usar o hello Azure PowerShell cmldts toodo a seguir assim.</span><span class="sxs-lookup"><span data-stu-id="545a2-155">You can use hello following Azure PowerShell cmldts toodo so.</span></span>

````
# Login tooour account
Login-AzureRmAccount

# List your subscriptions
Get-AzureRmSubscription

# Switch toohello subscription you want toowork with
Set-AzureRmContext –SubscriptionId
Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

# Join  hello files
Join-AzureRmDataLakeStoreItem -AccountName "<adls_account_name" -Paths "/importeddatafeb8job/319GB.tsv-part-aa","/importeddatafeb8job/319GB.tsv-part-ab", "/importeddatafeb8job/319GB.tsv-part-ac", "/importeddatafeb8job/319GB.tsv-part-ad" -Destination "/importeddatafeb8job/MergedFile.csv”
````

## <a name="next-steps"></a><span data-ttu-id="545a2-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="545a2-156">Next steps</span></span>
* [<span data-ttu-id="545a2-157">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="545a2-157">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="545a2-158">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="545a2-158">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="545a2-159">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="545a2-159">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
