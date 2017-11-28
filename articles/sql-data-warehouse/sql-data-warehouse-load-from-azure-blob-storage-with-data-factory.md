---
redirect_url: /azure/sql-data-warehouse/sql-data-warehouse-load-with-data-factory
title: Carregar dados do armazenamento de blobs do Azure no Azure SQL Data Warehouse (Azure Data Factory) | Microsoft Docs
description: Saiba como carregar dados com o Azure Data Factory
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 689fb02e-eb98-4f7c-81e6-6c1d22d53901
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: barbkess
ms.custom: loading
ms.openlocfilehash: ca8bdfc21582253e8709a33eb624547fed4461d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-azure-sql-data-warehouse-azure-data-factory"></a><span data-ttu-id="3af53-103">Carregar dados do Armazenamento de Blobs do Azure no Azure SQL Data Warehouse (Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="3af53-103">Load data from Azure blob storage into Azure SQL Data Warehouse (Azure Data Factory)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3af53-104">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="3af53-104">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="3af53-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="3af53-105">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

 <span data-ttu-id="3af53-106">Este tutorial mostra como criar um pipeline no Azure Data Factory para mover dados do Blob de Armazenamento do Azure para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3af53-106">This tutorial shows you how to create a pipeline in Azure Data Factory to move data from Azure Storage Blob to SQL Data Warehouse.</span></span> <span data-ttu-id="3af53-107">Com as etapas a seguir, você vai:</span><span class="sxs-lookup"><span data-stu-id="3af53-107">With the following steps you will:</span></span>

* <span data-ttu-id="3af53-108">Configurar dados de exemplo em um Blob de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af53-108">Set-up sample data in an Azure Storage Blob.</span></span>
* <span data-ttu-id="3af53-109">Conectar recursos ao Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3af53-109">Connect resources to Azure Data Factory.</span></span>
* <span data-ttu-id="3af53-110">Crie um pipeline para mover dados de Blobs de Armazenamento para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3af53-110">Create a pipeline to move data from Storage Blobs to SQL Data Warehouse.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-Azure-SQL-Data-Warehouse-with-Azure-Data-Factory/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="3af53-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="3af53-111">Before you begin</span></span>
<span data-ttu-id="3af53-112">Para se familiarizar com o Azure Data Factory, confira a [Introdução ao Azure Data Factory][Introduction to Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="3af53-112">To familiarize yourself with Azure Data Factory, see [Introduction to Azure Data Factory][Introduction to Azure Data Factory].</span></span>

### <a name="create-or-identify-resources"></a><span data-ttu-id="3af53-113">Criar ou identificar recursos</span><span class="sxs-lookup"><span data-stu-id="3af53-113">Create or identify resources</span></span>
<span data-ttu-id="3af53-114">Antes de iniciar este tutorial, você precisa ter os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="3af53-114">Before starting this tutorial, you need to have the following resources.</span></span>

* <span data-ttu-id="3af53-115">**Blob de Armazenamento do Azure**: este tutorial usa o Blob de Armazenamento do Azure como a fonte de dados para o pipeline do Azure Data Factory. Portanto, você precisa ter um disponível para armazenar os dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="3af53-115">**Azure Storage Blob**: This tutorial uses Azure Storage Blob as the data source for the Azure Data Factory pipeline, and so you need to have one available to store the sample data.</span></span> <span data-ttu-id="3af53-116">Se você não tiver um, saiba como [Criar uma conta de armazenamento][Create a storage account].</span><span class="sxs-lookup"><span data-stu-id="3af53-116">If you don't have one already, learn how to [Create a storage account][Create a storage account].</span></span>
* <span data-ttu-id="3af53-117">**SQL Data Warehouse**: Este tutorial move os dados do Blob de Armazenamento do Azure para o SQL Data Warehouse e, portanto, precisa ter um data warehouse online que é carregado com os dados de exemplo AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="3af53-117">**SQL Data Warehouse**: This tutorial moves the data from Azure Storage Blob to  SQL Data Warehouse and so need to have a data warehouse online that is loaded with the AdventureWorksDW sample data.</span></span> <span data-ttu-id="3af53-118">Se você ainda não tiver um data warehouse, saiba como [provisionar um][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="3af53-118">If you do not already have a data warehouse, learn how to [provision one][Create a SQL Data Warehouse].</span></span> <span data-ttu-id="3af53-119">Se você tiver um data warehouse, mas não o tiver provisionado com os dados de exemplo, poderá [carregá-lo manualmente][Load sample data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="3af53-119">If you have a data warehouse but didn't provision it with the sample data, you can [load it manually][Load sample data into SQL Data Warehouse].</span></span>
* <span data-ttu-id="3af53-120"><seg>
  **Azure Data Factory**: o Azure Data Factory concluirá a carga real e, assim, você precisa garantir que possa usá-lo para criar o pipeline de movimentação de dados. Se você não tiver um, saiba como criá-lo na Etapa 1 da [Introdução ao Azure Data Factory (Editor do Data Factory)][Get started with Azure Data Factory (Data Factory Editor)].</seg></span><span class="sxs-lookup"><span data-stu-id="3af53-120">**Azure Data Factory**: Azure Data Factory will complete the actual load and so you need to have one that you can use to build the data movement pipeline.If you don't have one already, learn how to create one in Step 1 of [Get started with Azure Data Factory (Data Factory Editor)][Get started with Azure Data Factory (Data Factory Editor)].</span></span>
* <span data-ttu-id="3af53-121">**AZCopy**: você precisa do AZCopy para copiar os dados de exemplo do cliente local para o Blob de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af53-121">**AZCopy**: You need AZCopy to copy the sample data from your local client to your Azure Storage Blob.</span></span> <span data-ttu-id="3af53-122">Para obter instruções de instalação, confira a [Documentação do AZCopy][AZCopy documentation].</span><span class="sxs-lookup"><span data-stu-id="3af53-122">For install instructions, see the [AZCopy documentation][AZCopy documentation].</span></span>

## <a name="step-1-copy-sample-data-to-azure-storage-blob"></a><span data-ttu-id="3af53-123">Etapa 1: copiar dados de exemplo para o Blob de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3af53-123">Step 1: Copy sample data to Azure Storage Blob</span></span>
<span data-ttu-id="3af53-124">Depois que todas as partes estiverem prontas, você estará pronto para copiar dados de exemplo para o Blob de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af53-124">Once you have all of the pieces ready, you are ready to copy sample data to your Azure Storage Blob.</span></span>

1. <span data-ttu-id="3af53-125">[Baixe os dados de exemplo][Download sample data].</span><span class="sxs-lookup"><span data-stu-id="3af53-125">[Download sample data][Download sample data].</span></span> <span data-ttu-id="3af53-126">Esses dados adicionarão outros três anos de dados de vendas aos dados de exemplo de AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="3af53-126">This data will add another three years of sales data to your AdventureWorksDW sample data.</span></span>
2. <span data-ttu-id="3af53-127">Use este comando do AZCopy para copiar os três anos de dados para o Blob de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af53-127">Use this AZCopy command to copy the three years of data to your Azure Storage Blob.</span></span>

````
AzCopy /Source:<Sample Data Location>  /Dest:https://<storage account>.blob.core.windows.net/<container name> /DestKey:<storage key> /Pattern:FactInternetSales.csv
````


## <a name="step-2-connect-resources-to-azure-data-factory"></a><span data-ttu-id="3af53-128">Etapa 2: conectar recursos ao Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="3af53-128">Step 2: Connect resources to Azure Data Factory</span></span>
<span data-ttu-id="3af53-129">Agora que os dados estão no lugar certo, podemos criar o pipeline do Azure Data Factory para mover os dados do armazenamento de blob do Azure para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3af53-129">Now that the data is in place we can create the Azure Data Factory pipeline to move the data from Azure blob storage into SQL Data Warehouse.</span></span>

<span data-ttu-id="3af53-130">Para começar, abra o [Portal do Azure][Azure portal] e selecione o data factory no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="3af53-130">To get started, open the [Azure portal][Azure portal] and select your data factory from the left-hand menu.</span></span>

### <a name="step-21-create-linked-service"></a><span data-ttu-id="3af53-131">Etapa 2.1: criar serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="3af53-131">Step 2.1: Create Linked Service</span></span>
<span data-ttu-id="3af53-132">Vincule sua conta de armazenamento do Azure e oi SQL Data Warehouse ao data factory.</span><span class="sxs-lookup"><span data-stu-id="3af53-132">Link your Azure storage account and SQL Data Warehouse to your data factory.</span></span>  

1. <span data-ttu-id="3af53-133">Primeiro, inicie o processo de registro clicando na seção 'Serviços Vinculados' de sua fábrica de dados e clique em 'Novo armazenamento de dados'.</span><span class="sxs-lookup"><span data-stu-id="3af53-133">First, begin the registration process by clicking the 'Linked Services' section of your data factory and then click 'New data store.'</span></span> <span data-ttu-id="3af53-134">Escolha um nome para registrar seu armazenamento do azure, selecione o Armazenamento do Azure como seu tipo e insira o Nome de Conta e a Chave da Conta.</span><span class="sxs-lookup"><span data-stu-id="3af53-134">Choose a name to register your azure storage under, select Azure Storage as your type, and then enter your Account Name and Account Key.</span></span>
2. <span data-ttu-id="3af53-135">Para registrar o SQL Data Warehouse, navegue até a seção 'Criar e Implantar', selecionar 'Novo Armazenamento de Dados' e 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="3af53-135">To register SQL Data Warehouse navigate to the 'Author and Deploy' section, select 'New Data Store', and then 'Azure SQL Data Warehouse'.</span></span> <span data-ttu-id="3af53-136">Copie e cole nesse modelo e, em seguida, preencha as informações específicas.</span><span class="sxs-lookup"><span data-stu-id="3af53-136">Copy and paste in this template, and then fill in your specific information.</span></span>

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

### <a name="step-22-define-the-dataset"></a><span data-ttu-id="3af53-137">Etapa 2.2: definir o conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="3af53-137">Step 2.2: Define the dataset</span></span>
<span data-ttu-id="3af53-138">Depois de criar os serviços vinculados, teremos de definir os conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="3af53-138">After creating the linked services, we will have to define the data sets.</span></span>  <span data-ttu-id="3af53-139">Aqui, isso significa definir a estrutura dos dados que está sendo movida do armazenamento para o data warehouse.</span><span class="sxs-lookup"><span data-stu-id="3af53-139">Here this means defining the structure of the data that is being moved from your storage to your data warehouse.</span></span>  <span data-ttu-id="3af53-140">Ler mais sobre a criação</span><span class="sxs-lookup"><span data-stu-id="3af53-140">You can read more about creating</span></span>

1. <span data-ttu-id="3af53-141">Inicie este processo navegando até a seção 'Criar e Implantar' de sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="3af53-141">Start this process by navigating to the 'Author and Deploy' section of your data factory.</span></span>
2. <span data-ttu-id="3af53-142">Clique em 'Novo conjunto de dados' e em 'Armazenamento de Blob do Azure' para vincular o armazenamento à fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="3af53-142">Click 'New dataset' and then 'Azure Blob storage' to link your storage to your data factory.</span></span>  <span data-ttu-id="3af53-143">Você pode usar o script abaixo para definir os dados no armazenamento de Blob do Azure:</span><span class="sxs-lookup"><span data-stu-id="3af53-143">You can use the below script to define your data in Azure Blob storage:</span></span>

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


1. <span data-ttu-id="3af53-144">Agora, definiremos também nosso conjunto de dados para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3af53-144">Now we will also define our dataset for SQL Data Warehouse.</span></span>  <span data-ttu-id="3af53-145">Começamos da mesma forma, clicando em 'Novo conjunto de dados' e em 'Azure SQL Data Warehouse'.</span><span class="sxs-lookup"><span data-stu-id="3af53-145">We start in the same way, by clicking 'New dataset' and then 'Azure SQL Data Warehouse'.</span></span>

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

## <a name="step-3-create-and-run-your-pipeline"></a><span data-ttu-id="3af53-146">Etapa 3: criar e executar o pipeline</span><span class="sxs-lookup"><span data-stu-id="3af53-146">Step 3: Create and run your pipeline</span></span>
<span data-ttu-id="3af53-147">Por fim, vamos configurar e executar o pipeline no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3af53-147">Finally, we will set-up and run the pipeline in Azure Data Factory.</span></span>  <span data-ttu-id="3af53-148">Esta é a operação que concluirá a movimentação de dados reais.</span><span class="sxs-lookup"><span data-stu-id="3af53-148">This is the operation that will complete the actual data movement.</span></span>  <span data-ttu-id="3af53-149">Você pode encontrar uma exibição completa das operações que podem ser executadas com o SQL Data Warehouse e o Azure Data Factory [aqui][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span><span class="sxs-lookup"><span data-stu-id="3af53-149">You can find a full view of the operations that you can complete with SQL Data Warehouse and Azure Data Factory [here][Move data to and from Azure SQL Data Warehouse using Azure Data Factory].</span></span>

<span data-ttu-id="3af53-150">Na seção 'Criar e Implantar', agora clique em 'Mais Comandos' e em 'Novo Pipeline'.</span><span class="sxs-lookup"><span data-stu-id="3af53-150">In the 'Author and Deploy' section now click 'More Commands' and then 'New Pipeline'.</span></span>  <span data-ttu-id="3af53-151">Depois de criar o pipeline, você poderá usar o código abaixo para transferir os dados para o data warehouse:</span><span class="sxs-lookup"><span data-stu-id="3af53-151">After you create the pipeline, you can use the below code to transfer the data to your data warehouse:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3af53-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3af53-152">Next steps</span></span>
<span data-ttu-id="3af53-153">Para saber mais, comece exibindo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="3af53-153">To learn more, start by viewing:</span></span>

* <span data-ttu-id="3af53-154">[Roteiro de aprendizagem do Azure Data Factory][Azure Data Factory learning path].</span><span class="sxs-lookup"><span data-stu-id="3af53-154">[Azure Data Factory learning path][Azure Data Factory learning path].</span></span>
* <span data-ttu-id="3af53-155">[Conector do SQL Data Warehouse do Azure][Azure SQL Data Warehouse Connector].</span><span class="sxs-lookup"><span data-stu-id="3af53-155">[Azure SQL Data Warehouse Connector][Azure SQL Data Warehouse Connector].</span></span> <span data-ttu-id="3af53-156">Este é o tópico de referência principal para usar o Azure Data Factory com o SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af53-156">This is the core reference topic for using Azure Data Factory with Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="3af53-157">Estes tópicos fornecem informações detalhadas sobre o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3af53-157">These topics provide detailed information about Azure Data Factory.</span></span> <span data-ttu-id="3af53-158">Eles abordam o Banco de Dados SQL do Azure ou o HDinsight, mas as informações também se aplicam ao SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af53-158">They discuss Azure SQL Database or HDinsight, but the information also applies to Azure SQL Data Warehouse.</span></span>

* <span data-ttu-id="3af53-159">[Tutorial: introdução ao Azure Data Factory][Tutorial: Get started with Azure Data Factory] Este é o tutorial principal para processar dados com o Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="3af53-159">[Tutorial: Get started with Azure Data Factory][Tutorial: Get started with Azure Data Factory] This is the core tutorial for processing data with Azure Data Factory.</span></span> <span data-ttu-id="3af53-160">Neste tutorial, você criará seu primeiro pipeline que usa HDInsight para transformar e analisar logs da web mensalmente.</span><span class="sxs-lookup"><span data-stu-id="3af53-160">In this tutorial you will build your first pipeline that uses HDInsight to transform and analyze web logs on a monthly basis.</span></span> <span data-ttu-id="3af53-161">Observe que não há nenhuma atividade de cópia neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3af53-161">Note, there is no copy activity in this tutorial.</span></span>
* <span data-ttu-id="3af53-162">[Tutorial: copiar dados do Blob de Armazenamento do Azure para o Banco de Dados SQL do Azure][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span><span class="sxs-lookup"><span data-stu-id="3af53-162">[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database][Tutorial: Copy data from Azure Storage Blob to Azure SQL Database].</span></span> <span data-ttu-id="3af53-163">Neste tutorial, você criará um pipeline no Azure Data Factory para copiar dados do Blob de Armazenamento do Azure para o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="3af53-163">In this tutorial, you will create a pipeline in Azure Data Factory to copy data from Azure Storage Blob to Azure SQL Database.</span></span>

<!--Image references-->

<!--Article references-->
[AZCopy documentation]: ../storage/storage-use-azcopy.md
[Azure SQL Data Warehouse Connector]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[BCP]: sql-data-warehouse-load-with-bcp.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Create a storage account]: ../storage/storage-create-storage-account.md#create-a-storage-account
[Data Factory]: sql-data-warehouse-get-started-load-with-azure-data-factory.md
[Get started with Azure Data Factory (Data Factory Editor)]: ../data-factory/data-factory-build-your-first-pipeline-using-editor.md
[Introduction to Azure Data Factory]: ../data-factory/data-factory-introduction.md
[Load sample data into SQL Data Warehouse]: sql-data-warehouse-load-sample-databases.md
[Move data to and from Azure SQL Data Warehouse using Azure Data Factory]: ../data-factory/data-factory-azure-sql-data-warehouse-connector.md
[PolyBase]: sql-data-warehouse-get-started-load-with-polybase.md
[Tutorial: Copy data from Azure Storage Blob to Azure SQL Database]: ../data-factory/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[Tutorial: Get started with Azure Data Factory]: ../data-factory/data-factory-build-your-first-pipeline.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory learning path]: https://azure.microsoft.com/documentation/learning-paths/data-factory
[Azure portal]: https://portal.azure.com
[Download sample data]: https://migrhoststorage.blob.core.windows.net/adfsample/FactInternetSales.csv
