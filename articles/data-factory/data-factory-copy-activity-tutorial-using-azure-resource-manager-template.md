---
title: 'Tutorial: criar um pipeline usando o modelo do Resource Manager | Microsoft Docs'
description: "Neste tutorial, você criará um pipeline do Azure Data Factory usando um modelo do Azure Resource Manager. Esse pipeline copia dados de um armazenamento de blobs do Azure para um banco de dados SQL do Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1274e11a-e004-4df5-af07-850b2de7c15e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8a155213ed17e516a5c46abbe3d8a2bcc52268ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-resource-manager-template-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="ee04e-104">Tutorial: usar o Azure Resource Manager para criar um pipeline de Data Factory a fim de copiar dados</span><span class="sxs-lookup"><span data-stu-id="ee04e-104">Tutorial: Use Azure Resource Manager template to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee04e-105">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ee04e-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="ee04e-106">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="ee04e-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="ee04e-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="ee04e-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ee04e-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="ee04e-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee04e-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="ee04e-110">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ee04e-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="ee04e-111">API REST</span><span class="sxs-lookup"><span data-stu-id="ee04e-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="ee04e-112">API do .NET</span><span class="sxs-lookup"><span data-stu-id="ee04e-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="ee04e-113">Este tutorial mostra como usar um modelo do Azure Resource Manager para criar um Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-113">This tutorial shows you how to use an Azure Resource Manager template to create an Azure data factory.</span></span> <span data-ttu-id="ee04e-114">O pipeline de dados neste tutorial copia os dados de um armazenamento de dados de origem para um armazenamento de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="ee04e-114">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="ee04e-115">Ele não transforma dados de entrada para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="ee04e-115">It does not transform input data to produce output data.</span></span> <span data-ttu-id="ee04e-116">Para obter um tutorial sobre como transformar dados usando o Azure Data Factory, veja [Tutorial: Criar um pipeline para transformar dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ee04e-116">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="ee04e-117">Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ee04e-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="ee04e-118">A atividade de cópia copia dados de um armazenamento de dados com suporte para um armazenamento de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="ee04e-118">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="ee04e-119">Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ee04e-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="ee04e-120">A atividade é habilitada por um serviço globalmente disponível que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="ee04e-120">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="ee04e-121">Para saber mais sobre a atividade de cópia, confira [Atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ee04e-121">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="ee04e-122">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="ee04e-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="ee04e-123">E você pode encadear duas atividades (executar uma atividade após a outra) definindo o conjunto de dados de saída de uma atividade como o conjunto de dados de entrada da outra atividade.</span><span class="sxs-lookup"><span data-stu-id="ee04e-123">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="ee04e-124">Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="ee04e-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="ee04e-125">O pipeline de dados neste tutorial copia os dados de um armazenamento de dados de origem para um armazenamento de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="ee04e-125">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="ee04e-126">Para obter um tutorial sobre como transformar dados usando o Azure Data Factory, veja [Tutorial: Criar um pipeline para transformar dados usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ee04e-126">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ee04e-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ee04e-127">Prerequisites</span></span>
* <span data-ttu-id="ee04e-128">Percorra o artigo [Pré-requisitos e Visão Geral do Tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) e conclua as etapas de **pré-requisito**.</span><span class="sxs-lookup"><span data-stu-id="ee04e-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="ee04e-129">Siga as instruções do artigo [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) para instalar a última versão do Azure PowerShell no computador.</span><span class="sxs-lookup"><span data-stu-id="ee04e-129">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="ee04e-130">Neste tutorial, você usa o PowerShell para implantar as entidades de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-130">In this tutorial, you use PowerShell to deploy Data Factory entities.</span></span> 
* <span data-ttu-id="ee04e-131">(opcional) Veja [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) para saber mais sobre os modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee04e-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="ee04e-132">Neste tutorial</span><span class="sxs-lookup"><span data-stu-id="ee04e-132">In this tutorial</span></span>
<span data-ttu-id="ee04e-133">Neste tutorial, você pode criar um data factory com as seguintes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="ee04e-133">In this tutorial, you create a data factory with the following Data Factory entities:</span></span>

| <span data-ttu-id="ee04e-134">Entidade</span><span class="sxs-lookup"><span data-stu-id="ee04e-134">Entity</span></span> | <span data-ttu-id="ee04e-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="ee04e-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ee04e-136">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-136">Azure Storage linked service</span></span> |<span data-ttu-id="ee04e-137">Vincula sua conta do Armazenamento do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-137">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="ee04e-138">O Armazenamento do Azure é o armazenamento de dados de origem e o Banco de Dados SQL do Azure é o armazenamento de dados do coletor para a atividade de cópia descrita no tutorial.</span><span class="sxs-lookup"><span data-stu-id="ee04e-138">Azure Storage is the source data store and Azure SQL database is the sink data store for the copy activity in the tutorial.</span></span> <span data-ttu-id="ee04e-139">Ele especifica a conta de armazenamento que contém os dados de entrada para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ee04e-139">It specifies the storage account that contains the input data for the copy activity.</span></span> |
| <span data-ttu-id="ee04e-140">Serviço vinculado para o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="ee04e-141">Vincula o Banco de Dados SQL do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-141">Links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="ee04e-142">Especifica o Banco de Dados SQL do Azure que contém os dados de saída para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ee04e-142">It specifies the Azure SQL database that holds the output data for the copy activity.</span></span> |
| <span data-ttu-id="ee04e-143">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-143">Azure Blob input dataset</span></span> |<span data-ttu-id="ee04e-144">Refere-se ao serviço vinculado do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-144">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="ee04e-145">O serviço vinculado refere-se a uma conta do Armazenamento do Azure e o conjunto de dados de blob do Azure especifica o contêiner, a pasta e o nome do arquivo no armazenamento que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee04e-145">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="ee04e-146">Conjunto de dados de saída do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-146">Azure SQL output dataset</span></span> |<span data-ttu-id="ee04e-147">Refere-se ao serviço vinculado do SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-147">Refers to the Azure SQL linked service.</span></span> <span data-ttu-id="ee04e-148">O serviço vinculado do SQL do Azure refere-se a um SQL Server do Azure e o conjunto de dados do SQL do Azure Especifica o nome da tabela que contém os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="ee04e-148">The Azure SQL linked service refers to an Azure SQL server and the Azure SQL dataset specifies the name of the table that holds the output data.</span></span> |
| <span data-ttu-id="ee04e-149">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="ee04e-149">Data pipeline</span></span> |<span data-ttu-id="ee04e-150">O pipeline tem uma atividade do tipo Cópia que usa o conjunto de dados de blob do Azure como uma entrada e o conjunto de dados do SQL do Azure como uma saída.</span><span class="sxs-lookup"><span data-stu-id="ee04e-150">The pipeline has one activity of type Copy that takes the Azure blob dataset as an input and the Azure SQL dataset as an output.</span></span> <span data-ttu-id="ee04e-151">A atividade de cópia copia dados de um blob do Azure para uma tabela no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-151">The copy activity copies data from an Azure blob to a table in the Azure SQL database.</span></span> |

<span data-ttu-id="ee04e-152">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="ee04e-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="ee04e-153">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="ee04e-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="ee04e-154">Há dois tipos de atividades: [atividades de movimentação de dados](data-factory-data-movement-activities.md) e [atividades de transformação de dados](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ee04e-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="ee04e-155">Neste tutorial, você criará um pipeline com uma atividade (atividade de cópia).</span><span class="sxs-lookup"><span data-stu-id="ee04e-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Copiar Blob do Azure para o Banco de Dados SQL do Azure](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="ee04e-157">A seção a seguir fornece o modelo do Resource Manager completo para definir entidades de Data Factory de modo que você possa percorrer o tutorial rapidamente e testar o modelo.</span><span class="sxs-lookup"><span data-stu-id="ee04e-157">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="ee04e-158">Para entender como cada entidade de Data Factory é definida, consulte a seção [Entidades de Data Factory no modelo](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="ee04e-158">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="ee04e-159">Modelo de JSON do Data Factory</span><span class="sxs-lookup"><span data-stu-id="ee04e-159">Data Factory JSON template</span></span>
<span data-ttu-id="ee04e-160">O modelo do Resource Manager de nível superior para definir um data factory é:</span><span class="sxs-lookup"><span data-stu-id="ee04e-160">The top-level Resource Manager template for defining a data factory is:</span></span> 

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
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
<span data-ttu-id="ee04e-161">Crie um arquivo JSON denominado **ADFCopyTutorialARM.json** na pasta **C:\ADFGetStarted** com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="ee04e-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the data to be copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of the blob in the container that has the data to be copied to Azure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Server that will hold the output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of the Azure SQL Database in the Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of the user that has access to the Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for the user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in the Azure SQL Database that will hold the copied data." } 
      } 
    },
    "variables": {
      "dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]",
      "azureSqlLinkedServiceName": "AzureSqlLinkedService",
      "azureStorageLinkedServiceName": "AzureStorageLinkedService",
      "blobInputDatasetName": "BlobInputDataset",
      "sqlOutputDatasetName": "SQLOutputDataset",
      "pipelineName": "Blob2SQLPipeline"
    },
    "resources": [
      {
        "name": "[variables('dataFactoryName')]",
        "apiVersion": "2015-10-01",
        "type": "Microsoft.DataFactory/datafactories",
        "location": "West US",
        "resources": [
          {
            "type": "linkedservices",
            "name": "[variables('azureStorageLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureStorage",
              "description": "Azure Storage linked service",
              "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
              }
            }
          },
          {
            "type": "linkedservices",
            "name": "[variables('azureSqlLinkedServiceName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlDatabase",
              "description": "Azure SQL linked service",
              "typeProperties": {
                "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
              }
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobInputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureBlob",
              "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
              "structure": [
                {
                  "name": "Column0",
                  "type": "String"
                },
                {
                  "name": "Column1",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
                "fileName": "[parameters('sourceBlobName')]",
                "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
                }
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              },
              "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('sqlOutputDatasetName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureSqlLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "type": "AzureSqlTable",
              "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
              "structure": [
                {
                  "name": "FirstName",
                  "type": "String"
                },
                {
                  "name": "LastName",
                  "type": "String"
                }
              ],
              "typeProperties": {
                "tableName": "[parameters('targetSQLTable')]"
              },
              "availability": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          {
            "type": "datapipelines",
            "name": "[variables('pipelineName')]",
            "dependsOn": [
              "[variables('dataFactoryName')]",
              "[variables('azureStorageLinkedServiceName')]",
              "[variables('azureSqlLinkedServiceName')]",
              "[variables('blobInputDatasetName')]",
              "[variables('sqlOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
              "activities": [
                {
                  "name": "CopyFromAzureBlobToAzureSQL",
                  "description": "Copy data frm Azure blob to Azure SQL",
                  "type": "Copy",
                  "inputs": [
                    {
                      "name": "[variables('blobInputDatasetName')]"
                    }
                  ],
                  "outputs": [
                    {
                      "name": "[variables('sqlOutputDatasetName')]"
                    }
                  ],
                  "typeProperties": {
                    "source": {
                      "type": "BlobSource"
                    },
                    "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                    },
                    "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                    }
                  },
                  "Policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 3,
                    "timeout": "01:00:00"
                  }
                }
              ],
              "start": "2017-05-11T00:00:00Z",
              "end": "2017-05-12T00:00:00Z"
            }
          }
        ]
      }
    ]
  }
```

## <a name="parameters-json"></a><span data-ttu-id="ee04e-162">Parâmetros JSON</span><span class="sxs-lookup"><span data-stu-id="ee04e-162">Parameters JSON</span></span>
<span data-ttu-id="ee04e-163">Crie um arquivo JSON chamado **ADFCopyTutorialARM-Parameters.json** que contenha os parâmetros para o modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee04e-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ee04e-164">Especifique o nome e a chave de sua conta do Armazenamento do Azure nos parâmetros storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="ee04e-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="ee04e-165">Especifique o servidor Azure SQL, o banco de dados, o usuário e a senha para os parâmetros sqlServerName, databaseName, sqlServerUserName e sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="ee04e-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of the Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for the Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of the Azure SQL server>" },
        "databaseName": { "value": "<Name of the Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of the user who has access to the Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for the user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="ee04e-166">Você pode ter arquivos JSON de parâmetros separados para desenvolvimento, teste e ambientes de produção que pode usar com o mesmo modelo JSON do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="ee04e-167">Usando um script do PowerShell, você pode automatizar a implantação de entidades de Data Factory nesses ambientes.</span><span class="sxs-lookup"><span data-stu-id="ee04e-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="ee04e-168">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="ee04e-168">Create data factory</span></span>
1. <span data-ttu-id="ee04e-169">Inicie o **Azure PowerShell** e execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee04e-169">Start **Azure PowerShell** and run the following command:</span></span>
   * <span data-ttu-id="ee04e-170">Execute o comando a seguir e insira o nome de usuário e a senha que você usa para entrar no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-170">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="ee04e-171">Execute o comando a seguir para exibir todas as assinaturas dessa conta.</span><span class="sxs-lookup"><span data-stu-id="ee04e-171">Run the following command to view all the subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="ee04e-172">Execute o comando a seguir para selecionar a assinatura com a qual deseja trabalhar.</span><span class="sxs-lookup"><span data-stu-id="ee04e-172">Run the following command to select the subscription that you want to work with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="ee04e-173">Execute o comando a seguir para implantar entidades do Data Factory usando o modelo do Resource Manager criado na Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="ee04e-173">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="ee04e-174">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="ee04e-174">Monitor pipeline</span></span>

1. <span data-ttu-id="ee04e-175">Faça logon no [Portal do Azure](https://portal.azure.com) usando sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-175">Log in to the [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="ee04e-176">Clique em **Data factories** no menu esquerdo ou clique em **Mais serviços** e clique em **Data factories** na categoria **INTELIGÊNCIA + ANÁLISE**.</span><span class="sxs-lookup"><span data-stu-id="ee04e-176">Click **Data factories** on the left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Menu Data factories](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="ee04e-178">Na página **Data factories**, pesquise e localize o data factory (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="ee04e-178">In the **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Pesquisar por data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="ee04e-180">Clique no seu Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-180">Click your Azure data factory.</span></span> <span data-ttu-id="ee04e-181">Você verá a home page do data factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-181">You see the home page for the data factory.</span></span>
   
    ![Home page do data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="ee04e-183">Siga as instruções de [Monitorar conjuntos de dados e pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) para monitorar o pipeline e os conjuntos de dados criados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="ee04e-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) to monitor the pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="ee04e-184">Atualmente, o Visual Studio não dá suporte a monitoramento de pipelines do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="ee04e-185">Quando a fatia estiver no estado **Pronto**, verifique se que os dados são copiados para a tabela **emp** no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-185">When a slice is in the **Ready** state, verify that the data is copied to the **emp** table in the Azure SQL database.</span></span>


<span data-ttu-id="ee04e-186">Para obter instruções sobre como usar as folhas do portal do Azure para monitorar o pipeline e os conjuntos de dados que você criou neste tutorial, confira [Monitorar os conjuntos de dados e o pipeline](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ee04e-186">For more information on how to use Azure portal blades to monitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="ee04e-187">Para saber mais sobre como usar o aplicativo Monitorar e gerenciar para monitorar os pipelines de dados, confira [Monitorar e gerenciar pipelines do Azure Data Factory usando o aplicativo de monitoramento](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="ee04e-187">For more information on how to use the Monitor & Manage application to monitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="ee04e-188">Entidades do Data Factory no modelo</span><span class="sxs-lookup"><span data-stu-id="ee04e-188">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="ee04e-189">Definir Data Factory</span><span class="sxs-lookup"><span data-stu-id="ee04e-189">Define data factory</span></span>
<span data-ttu-id="ee04e-190">Você pode definir um Data Factory no modelo do Resource Manager, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee04e-190">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="ee04e-191">O dataFactoryName é definido como:</span><span class="sxs-lookup"><span data-stu-id="ee04e-191">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="ee04e-192">É uma cadeia de caracteres exclusiva com base na ID de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ee04e-192">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="ee04e-193">Definir entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="ee04e-193">Defining Data Factory entities</span></span>
<span data-ttu-id="ee04e-194">As seguintes entidades de Data Factory são definidas no modelo JSON:</span><span class="sxs-lookup"><span data-stu-id="ee04e-194">The following Data Factory entities are defined in the JSON template:</span></span> 

1. [<span data-ttu-id="ee04e-195">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="ee04e-196">Serviço vinculado do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="ee04e-197">Conjunto de dados de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="ee04e-198">Conjunto de dados do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="ee04e-199">Pipeline de dados com a atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="ee04e-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="ee04e-200">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-200">Azure Storage linked service</span></span>
<span data-ttu-id="ee04e-201">O AzureStorageLinkedService vincula sua conta do armazenamento do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-201">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="ee04e-202">Você criou um contêiner e carregou dados nessa conta de armazenamento como parte dos [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ee04e-202">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="ee04e-203">Especifique o nome e a chave da sua conta de armazenamento do Azure nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ee04e-203">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="ee04e-204">Consulte [Serviço vinculado de Armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre os propriedades JSON usadas para definir um serviço vinculado de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

```json
{
    "type": "linkedservices",
    "name": "[variables('azureStorageLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureStorage",
        "description": "Azure Storage linked service",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```

<span data-ttu-id="ee04e-205">A connectionString usa os parâmetros storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="ee04e-205">The connectionString uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="ee04e-206">Os valores para esses parâmetros são passados pelo uso de um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="ee04e-206">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="ee04e-207">A definição também usa variáveis: azureStroageLinkedService e dataFactoryName definidos no modelo.</span><span class="sxs-lookup"><span data-stu-id="ee04e-207">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="ee04e-208">Serviço vinculado para o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="ee04e-209">O AzureSqlLinkedService vincula seu banco de dados SQL do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="ee04e-209">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="ee04e-210">Os dados copiados do armazenamento de blobs são armazenados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ee04e-210">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="ee04e-211">Você criou a tabela emp no banco de dados como parte dos [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="ee04e-211">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="ee04e-212">Especifique o nome do SQL Server do Azure, nome do banco de dados, nome de usuário e senha de usuário nesta seção.</span><span class="sxs-lookup"><span data-stu-id="ee04e-212">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="ee04e-213">Consulte [Serviço vinculado do SQL do Azure](data-factory-azure-sql-connector.md#linked-service-properties) para obter detalhes sobre os propriedades JSON usadas para definir um serviço vinculado do SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('azureSqlLinkedServiceName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlDatabase",
          "description": "Azure SQL linked service",
          "typeProperties": {
            "connectionString": "[concat('Server=tcp:',parameters('sqlServerName'),'.database.windows.net,1433;Database=', parameters('databaseName'), ';User ID=',parameters('sqlServerUserName'),';Password=',parameters('sqlServerPassword'),';Trusted_Connection=False;Encrypt=True;Connection Timeout=30')]"
          }
    }
}
```

<span data-ttu-id="ee04e-214">connectionString usa os parâmetros sqlServerName, databaseName, sqlServerUserName e sqlServerPassword, cujos valores são passados por meio de um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="ee04e-214">The connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="ee04e-215">A definição também usa as seguintes variáveis do modelo: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="ee04e-215">The definition also uses the following variables from the template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="ee04e-216">Conjunto de dados de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-216">Azure blob dataset</span></span>
<span data-ttu-id="ee04e-217">O serviço vinculado do Armazenamento do Azure especifica a cadeia de conexão que o serviço Data Factory usa no tempo de execução para se conectar à sua conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-217">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="ee04e-218">Na definição de conjunto de dados do blob do Azure, especifique os nomes do contêiner de blob, da pasta e do arquivo que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ee04e-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="ee04e-219">Confira [Propriedades de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre os propriedades JSON usadas para definir um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
      "[variables('dataFactoryName')]",
      "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
          "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "structure": [
        {
              "name": "Column0",
              "type": "String"
        },
        {
              "name": "Column1",
              "type": "String"
        }
          ],
          "typeProperties": {
            "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
            "fileName": "[parameters('sourceBlobName')]",
            "format": {
                  "type": "TextFormat",
                  "columnDelimiter": ","
            }
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          },
          "external": true
    }
}
```

#### <a name="azure-sql-dataset"></a><span data-ttu-id="ee04e-220">Conjunto de dados do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ee04e-220">Azure SQL dataset</span></span>
<span data-ttu-id="ee04e-221">Você pode especificar o nome da tabela no Banco de Dados SQL do Azure que contém os dados copiados do Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-221">You specify the name of the table in the Azure SQL database that holds the copied data from the Azure Blob storage.</span></span> <span data-ttu-id="ee04e-222">Veja [Propriedades de conjunto de dados do SQL do Azure](data-factory-azure-sql-connector.md#dataset-properties) para obter detalhes sobre os propriedades JSON usadas para definir um conjunto de dados do SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used to define an Azure SQL dataset.</span></span> 

```json
{
    "type": "datasets",
    "name": "[variables('sqlOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureSqlLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "type": "AzureSqlTable",
          "linkedServiceName": "[variables('azureSqlLinkedServiceName')]",
          "structure": [
        {
              "name": "FirstName",
              "type": "String"
        },
        {
              "name": "LastName",
              "type": "String"
        }
          ],
          "typeProperties": {
            "tableName": "[parameters('targetSQLTable')]"
          },
          "availability": {
            "frequency": "Hour",
            "interval": 1
          }
    }
}
```

#### <a name="data-pipeline"></a><span data-ttu-id="ee04e-223">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="ee04e-223">Data pipeline</span></span>
<span data-ttu-id="ee04e-224">Definir um pipeline que copia dados do conjunto de dados de blob do Azure para o conjunto de dados do SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee04e-224">You define a pipeline that copies data from the Azure blob dataset to the Azure SQL dataset.</span></span> <span data-ttu-id="ee04e-225">Consulte [JSON de Pipeline](data-factory-create-pipelines.md#pipeline-json) para obter descrições dos elementos JSON usados para definir um pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="ee04e-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
          "[variables('azureStorageLinkedServiceName')]",
          "[variables('azureSqlLinkedServiceName')]",
          "[variables('blobInputDatasetName')]",
          "[variables('sqlOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
          "activities": [
        {
              "name": "CopyFromAzureBlobToAzureSQL",
              "description": "Copy data frm Azure blob to Azure SQL",
              "type": "Copy",
              "inputs": [
            {
                  "name": "[variables('blobInputDatasetName')]"
            }
              ],
              "outputs": [
            {
                  "name": "[variables('sqlOutputDatasetName')]"
            }
              ],
              "typeProperties": {
                "source": {
                      "type": "BlobSource"
                },
                "sink": {
                      "type": "SqlSink",
                      "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM {0}', 'emp')"
                },
                "translator": {
                      "type": "TabularTranslator",
                      "columnMappings": "Column0:FirstName,Column1:LastName"
                }
              },
              "Policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 3,
                "timeout": "01:00:00"
              }
        }
          ],
          "start": "2017-05-11T00:00:00Z",
          "end": "2017-05-12T00:00:00Z"
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="ee04e-226">Reutilizar o modelo</span><span class="sxs-lookup"><span data-stu-id="ee04e-226">Reuse the template</span></span>
<span data-ttu-id="ee04e-227">No tutorial, você criou um modelo para definir entidades de Data Factory e um modelo para passar valores para parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ee04e-227">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="ee04e-228">O pipeline copia dados de uma conta do Armazenamento do Azure para um Banco de Dados SQL do Azure especificado por meio de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ee04e-228">The pipeline copies data from an Azure Storage account to an Azure SQL database specified via parameters.</span></span> <span data-ttu-id="ee04e-229">Para usar o mesmo modelo para implantar as entidades de Data Factory em ambientes diferentes, você cria um arquivo de parâmetro para cada ambiente e usa-o ao implantar esse ambiente.</span><span class="sxs-lookup"><span data-stu-id="ee04e-229">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="ee04e-230">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="ee04e-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="ee04e-231">Observe que o primeiro comando usa o arquivo de parâmetro para o ambiente de desenvolvimento, outro para o ambiente de teste e um terceiro para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ee04e-231">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="ee04e-232">Também é possível reutilizar o modelo para executar tarefas repetidas.</span><span class="sxs-lookup"><span data-stu-id="ee04e-232">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="ee04e-233">Por exemplo, você precisa criar vários data factories com um ou mais pipelines que implementam a mesma lógica, mas cada data factory usa contas de Armazenamento e do Banco de Dados SQL diferentes.</span><span class="sxs-lookup"><span data-stu-id="ee04e-233">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="ee04e-234">Nesse cenário, você usa o mesmo modelo no mesmo ambiente (desenvolvimento, teste ou produção) com arquivos de parâmetros diferentes para criar data factories.</span><span class="sxs-lookup"><span data-stu-id="ee04e-234">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="ee04e-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee04e-235">Next steps</span></span>
<span data-ttu-id="ee04e-236">Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="ee04e-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="ee04e-237">A tabela a seguir fornece uma lista de armazenamentos de dados com suporte como origens ou destinos na atividade de cópia:</span><span class="sxs-lookup"><span data-stu-id="ee04e-237">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="ee04e-238">Para saber mais sobre como copiar dados de/para um armazenamento de dados, clique no link para o armazenamento de dados na tabela.</span><span class="sxs-lookup"><span data-stu-id="ee04e-238">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
