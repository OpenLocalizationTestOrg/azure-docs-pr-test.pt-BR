---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: dados de aaaLoad com o Azure Data Factory | Microsoft Docs
description: Saiba mais dados tooload com o Azure Data Factory
services: sql-data-warehouse
documentationcenter: NA
author: twounder
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: ac7ddaa7-a3a5-4e15-b3cf-c696d2d105df
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 10/31/2016
ms.author: mausher;barbkess
ms.custom: loading
ms.openlocfilehash: 4186bd88d14be33f90130a41e8df06ce1d7cbab2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-azure-data-factory"></a><span data-ttu-id="949cc-103">Carregar dados com o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="949cc-103">Load Data with Azure Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="949cc-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="949cc-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="949cc-105">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="949cc-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="949cc-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="949cc-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="949cc-107">BCP</span><span class="sxs-lookup"><span data-stu-id="949cc-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)  
> 
> 

<span data-ttu-id="949cc-108">Este tutorial mostra como toocreate um pipeline de dados do Azure Data Factory toomove de tooAzure de Blob de armazenamento do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="949cc-108">This tutorial shows you how toocreate a pipeline in Azure Data Factory toomove data from Azure Storage Blob tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="949cc-109">Com hello etapas a seguir, você irá:</span><span class="sxs-lookup"><span data-stu-id="949cc-109">With hello following steps you will:</span></span>

* <span data-ttu-id="949cc-110">Configurar dados de exemplo em um Blob de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="949cc-110">Set up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="949cc-111">Conecte-se recursos tooAzure fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="949cc-111">Connect resources tooAzure Data Factory.</span></span>
* <span data-ttu-id="949cc-112">Crie um pipeline de dados de toomove de tooSQL de Blobs de armazenamento do Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="949cc-112">Create a pipeline toomove data from Storage Blobs tooSQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="949cc-113">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="949cc-113">Before you begin</span></span>
<span data-ttu-id="949cc-114">toofamiliarize-se com a fábrica de dados do Azure, consulte [tooAzure Introdução fábrica de dados][Introduction tooAzure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="949cc-114">toofamiliarize yourself with Azure Data Factory, see [Introduction tooAzure Data Factory][Introduction tooAzure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="949cc-115">Criar ou identificar recursos</span><span class="sxs-lookup"><span data-stu-id="949cc-115">Create or identify resources</span></span>
<span data-ttu-id="949cc-116">Antes de iniciar este tutorial, você precisa toohave Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="949cc-116">Before starting this tutorial, you need toohave hello following resources:</span></span>

* <span data-ttu-id="949cc-117">**Blob de armazenamento do Azure**: Este tutorial usa blobs de armazenamento do Azure como fonte de dados Olá para o pipeline do Azure Data Factory hello e, portanto você precisa de dados de exemplo de saudação do toohave um toostore disponíveis.</span><span class="sxs-lookup"><span data-stu-id="949cc-117">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as hello data source for hello Azure Data Factory pipeline, and so you need toohave one available toostore hello sample data.</span></span> <span data-ttu-id="949cc-118">Se você não tiver um já, saiba como muito[criar uma conta de armazenamento][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="949cc-118">If you don't have one already, learn how too[Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="949cc-119">**SQL Data Warehouse**: estes tutorial move Olá dados de Blob de armazenamento do Azure muito SQL Data Warehouse e, portanto precisam de toohave um data warehouse online que é carregado com hello dados de exemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="949cc-119">**SQL Data Warehouse**: This tutorial moves hello data from Azure Storage Blob too SQL Data Warehouse and so need toohave a data warehouse online that is loaded with hello AdventureWorksDW sample data.</span></span> <span data-ttu-id="949cc-120">Se você ainda não tiver um data warehouse, saiba como muito[provisionar um][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="949cc-120">If you do not already have a data warehouse, learn how too[provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="949cc-121">Se você tiver um data warehouse, mas não foi provisionada com dados de exemplo hello, você pode [carregá-lo manualmente][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="949cc-121">If you have a data warehouse but didn't provision it with hello sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="949cc-122">**O Azure Data Factory**: Azure Data Factory conclui a carga real hello e portanto, você precisa toohave um que você pode usar o pipeline de movimentação de dados toobuild hello.</span><span class="sxs-lookup"><span data-stu-id="949cc-122">**Azure Data Factory**: Azure Data Factory completes hello actual load and so you need toohave one that you can use toobuild hello data movement pipeline.</span></span> <span data-ttu-id="949cc-123">Se você não tiver um já, saiba como toocreate uma etapa 1 de [Introdução ao Azure Data Factory (Editor de fábrica de dados)][Get started with Azure Data Factory (Data Factory Editor)].</span><span class="sxs-lookup"><span data-stu-id="949cc-123">If you don't have one already, learn how toocreate one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="949cc-124">**AZCopy**: você precisa os dados de exemplo hello AZCopy toocopy do tooyour seu cliente local Blob de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="949cc-124">**AZCopy**: You need AZCopy toocopy hello sample data from your local client tooyour Azure Storage Blob.</span></span> <span data-ttu-id="949cc-125">Para obter instruções de instalação, consulte Olá [AZCopy documentação][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="949cc-125">For install instructions, see hello [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-tooazure-storage-blob"></a><span data-ttu-id="949cc-126">Etapa 1: Copiar dados de exemplo tooAzure Blob de armazenamento</span><span class="sxs-lookup"><span data-stu-id="949cc-126">Step 1: Copy sample data tooAzure Storage Blob</span></span>
<span data-ttu-id="949cc-127">Uma vez que todas as partes da saudação prontas, você está pronto toocopy exemplo dados tooyour Blob de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="949cc-127">Once you have all hello pieces ready, you are ready toocopy sample data tooyour Azure Storage Blob.</span></span>

1. <span data-ttu-id="949cc-128">[Baixe os dados de exemplo][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="949cc-128">[Download sample data][Download sample data].</span></span> <span data-ttu-id="949cc-129">Esses dados adiciona outro três anos de dados de vendas tooyour dados de exemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="949cc-129">This data adds another three years of sales data tooyour AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="949cc-130">Use esta saudação do AZCopy comando toocopy três anos de dados tooyour Blob de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="949cc-130">Use this AZCopy command toocopy hello three years of data tooyour Azure Storage Blob.</span></span>
   
    ````
    AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
    ````

## <a name="step-2-connect-resources-tooazure-data-factory"></a><span data-ttu-id="949cc-131">Etapa 2: Conectar recursos tooAzure fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="949cc-131">Step 2: Connect resources tooAzure Data Factory</span></span>
<span data-ttu-id="949cc-132">Agora que os dados de saudação estão em vigor podemos criar dados de saudação do hello Azure Data Factory pipeline toomove do armazenamento de BLOBs do Azure no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="949cc-132">Now that hello data is in place we can create hello Azure Data Factory pipeline toomove hello data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="949cc-133">tooget iniciado, abra Olá [portal do Azure] [ Azure portal] e selecione sua fábrica de dados no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="949cc-133">tooget started, open hello [Azure portal][Azure portal] and select your data factory from hello left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="949cc-134">Etapa 2.1: criar serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="949cc-134">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="949cc-135">Vincule sua conta de armazenamento do Azure e a fábrica de dados do SQL Data Warehouse tooyour.</span><span class="sxs-lookup"><span data-stu-id="949cc-135">Link your Azure storage account and SQL Data Warehouse tooyour data factory.</span></span>  

1. <span data-ttu-id="949cc-136">Primeiro, iniciar o processo de registro de saudação clicando seção 'Serviços vinculados' hello sua fábrica de dados e, em seguida, clique em 'Novo repositório de dados.'</span><span class="sxs-lookup"><span data-stu-id="949cc-136">First, begin hello registration process by clicking hello 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="949cc-137">Escolha um nome tooregister o armazenamento do azure no armazenamento do Azure selecione como o tipo e, em seguida, insira o nome da conta e chave de conta.</span><span class="sxs-lookup"><span data-stu-id="949cc-137">Choose a name tooregister your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="949cc-138">tooregister SQL Data Warehouse navegue toohello seção de 'Criar e implantar', selecione 'Novo repositório de dados' e 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="949cc-138">tooregister SQL Data Warehouse navigate toohello 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="949cc-139">Copie e cole nesse modelo e, em seguida, preencha as informações específicas.</span><span class="sxs-lookup"><span data-stu-id="949cc-139">Copy and paste in this template, and then fill in your specific information.</span></span>
   
    ```JSON
    {
        "name": "<Linked Service Name>",
        "properties": {
            "description": "",
            "type": "AzureSqlDW",
            "typeProperties": {
                 "connectionString": "Data Source=tcp:<server name>.database.windows.net,1433;Initial Catalog=<server name>;Integrated Security=False;User ID=<user>@<servername>;Password=<password>;Connect Timeout=30;Encrypt=True"
             }
        }
    }
    ```

### <a name="step-22-define-hello-dataset"></a><span data-ttu-id="949cc-140">Etapa 2.2: Definir o conjunto de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="949cc-140">Step 2.2: Define hello dataset</span></span>
<span data-ttu-id="949cc-141">Depois de criar hello serviços vinculados, temos toodefine Olá os conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="949cc-141">After creating hello linked services, we will have toodefine hello data sets.</span></span>  <span data-ttu-id="949cc-142">Aqui, isso significa definir Olá estrutura de dados de saudação que está sendo movidos de seu data warehouse de tooyour de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="949cc-142">Here this means defining hello structure of hello data that is being moved from your storage tooyour data warehouse.</span></span>  <span data-ttu-id="949cc-143">Ler mais sobre a criação</span><span class="sxs-lookup"><span data-stu-id="949cc-143">You can read more about creating</span></span>

1. <span data-ttu-id="949cc-144">Inicie esse processo navegando seção 'Criar e implantar' toohello sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="949cc-144">Start this process by navigating toohello 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="949cc-145">Clique em 'Novo conjunto de dados' e 'Armazenamento de BLOBs do Azure' toolink sua fábrica de dados do armazenamento tooyour.</span><span class="sxs-lookup"><span data-stu-id="949cc-145">Click 'New dataset' and then 'Azure Blob storage' toolink your storage tooyour data factory.</span></span>  <span data-ttu-id="949cc-146">Você pode usar o hello abaixo script toodefine seus dados no armazenamento de BLOBs do Azure:</span><span class="sxs-lookup"><span data-stu-id="949cc-146">You can use hello below script toodefine your data in Azure Blob storage:</span></span>
   
    ```JSON
    {
        "name": "<Dataset Name>",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "<linked storage name>",
            "typeProperties": {
                "folderPath": "<containter name>",
                "fileName": "FactInternetSales.csv",
                "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
                }
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }
    ```
3. <span data-ttu-id="949cc-147">Agora, definiremos nosso conjunto de dados para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="949cc-147">Now we define our dataset for SQL Data Warehouse.</span></span> <span data-ttu-id="949cc-148">Começamos Olá mesma forma, clicando em 'Novo conjunto de dados' e, em seguida, 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="949cc-148">We start in hello same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>
   
    ```JSON
    {
        "name": "DWDataset",
        "properties": {
            "type": "AzureSqlDWTable",
            "linkedServiceName": "AzureSqlDWLinkedService",
            "typeProperties": {
                "tableName": "FactInternetSales"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="949cc-149">Etapa 3: criar e executar o pipeline</span><span class="sxs-lookup"><span data-stu-id="949cc-149">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="949cc-150">Finalmente, configurar e executar o pipeline de saudação do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="949cc-150">Finally, we set up and run hello pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="949cc-151">Essa é a operação de saudação que conclui a movimentação de dados reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="949cc-151">This is hello operation that completes hello actual data movement.</span></span>  <span data-ttu-id="949cc-152">Você pode encontrar uma exibição completa de operações de saudação que pode ser concluída com o SQL Data Warehouse e o Azure Data Factory [aqui][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="949cc-152">You can find a full view of hello operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data tooand from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="949cc-153">Na seção 'Criar e implantar' do hello, clique em 'Mais comandos' e, em seguida, 'Novo Pipeline'.</span><span class="sxs-lookup"><span data-stu-id="949cc-153">In hello 'Author and Deploy' section, click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="949cc-154">Depois de criar o pipeline hello, você pode usar o hello abaixo código tootransfer Olá dados tooyour do data warehouse:</span><span class="sxs-lookup"><span data-stu-id="949cc-154">After you create hello pipeline, you can use hello below code tootransfer hello data tooyour data warehouse:</span></span>

```JSON
{
    "name": "<Pipeline Name>",
    "properties": {
        "description": "<Description>",
        "activities": [
          {
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "skipHeaderLineCount": 1
                },
                "sink": {
                    "type": "SqlDWSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:10"
                }
            },
            "inputs": [
              {
                "name": "<Storage Dataset>"
              }
            ],
            "outputs": [
              {
                "name": "<Data Warehouse Dataset>"
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
            "name": "Sample Copy",
            "description": "Copy Activity"
          }
        ],
        "start": "<Date YYYY-MM-DD>",
        "end": "<Date YYYY-MM-DD>",
        "isPaused": false
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="949cc-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="949cc-155">Next steps</span></span>
<span data-ttu-id="949cc-156">Além disso, inicie toolearn exibindo:</span><span class="sxs-lookup"><span data-stu-id="949cc-156">toolearn more, start by viewing:</span></span>

* <span data-ttu-id="949cc-157">[Roteiro de aprendizagem do Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="949cc-157">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="949cc-158">[Conector do SQL Data Warehouse do Azure][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="949cc-158">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="949cc-159">Este é um tópico de referência principal Olá para o uso do Azure Data Factory do Azure SQL Data warehouse.</span><span class="sxs-lookup"><span data-stu-id="949cc-159">This is hello core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="949cc-160">Estes tópicos fornecem informações detalhadas sobre o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="949cc-160">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="949cc-161">Discussão de banco de dados do SQL Azure ou HDInsight, mas Olá informações também se aplicam a tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="949cc-161">They discuss Azure SQL Database or HDInsight, but hello information also applies tooAzure SQL Data Warehouse.</span></span>

* <span data-ttu-id="949cc-162">[Tutorial: Introdução ao Azure Data Factory] [ Tutorial: Get started with Azure Data Factory] este é Olá tutorial de núcleo para processamento de dados com o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="949cc-162">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is hello core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="949cc-163">Neste tutorial, você criará seu pipeline primeiro que usa tootransform HDInsight e analise logs da web mensalmente.</span><span class="sxs-lookup"><span data-stu-id="949cc-163">In this tutorial, you will build your first pipeline that uses HDInsight tootransform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="949cc-164">Observe que não há nenhuma atividade de cópia neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="949cc-164">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="949cc-165">[Tutorial: Copiar dados de Blob de armazenamento do Azure tooAzure banco de dados SQL][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="949cc-165">[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database][Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database].</span></span> <span data-ttu-id="949cc-166">Neste tutorial, você pode criar um pipeline de dados do Azure Data Factory toocopy de Blob de armazenamento do Azure tooAzure banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="949cc-166">In this tutorial, you create a pipeline in Azure Data Factory toocopy data from Azure Storage Blob tooAzure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction tooAzure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data tooand from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob tooAzure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
