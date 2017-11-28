---
title: 'Tutorial: criar um pipeline usando o modelo do Resource Manager | Microsoft Docs'
description: "Neste tutorial, você criará um pipeline do Azure Data Factory usando um modelo do Azure Resource Manager. Esse pipeline copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure."
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
ms.openlocfilehash: 1c7567cb0423f7ce3e0cab2d77a4d861b70eb56b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a><span data-ttu-id="88554-104">Tutorial: Uso do Azure Resource Manager modelo toocreate uma fábrica de dados pipeline toocopy de dados</span><span class="sxs-lookup"><span data-stu-id="88554-104">Tutorial: Use Azure Resource Manager template toocreate a Data Factory pipeline toocopy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="88554-105">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="88554-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="88554-106">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="88554-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="88554-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="88554-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88554-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="88554-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="88554-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="88554-110">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88554-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="88554-111">API REST</span><span class="sxs-lookup"><span data-stu-id="88554-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="88554-112">API do .NET</span><span class="sxs-lookup"><span data-stu-id="88554-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="88554-113">Este tutorial mostra como toouse uma toocreate de modelo do Gerenciador de recursos do Azure uma fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-113">This tutorial shows you how toouse an Azure Resource Manager template toocreate an Azure data factory.</span></span> <span data-ttu-id="88554-114">pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa.</span><span class="sxs-lookup"><span data-stu-id="88554-114">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="88554-115">Ela não transforma dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="88554-115">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="88554-116">Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="88554-116">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="88554-117">Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="88554-117">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="88554-118">Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="88554-118">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="88554-119">Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="88554-119">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="88554-120">atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável.</span><span class="sxs-lookup"><span data-stu-id="88554-120">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="88554-121">Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="88554-121">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="88554-122">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="88554-122">A pipeline can have more than one activity.</span></span> <span data-ttu-id="88554-123">E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="88554-123">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="88554-124">Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="88554-124">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="88554-125">pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa.</span><span class="sxs-lookup"><span data-stu-id="88554-125">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="88554-126">Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="88554-126">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="88554-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="88554-127">Prerequisites</span></span>
* <span data-ttu-id="88554-128">Passar [Tutorial visão geral e pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) e hello completa **pré-requisito** etapas.</span><span class="sxs-lookup"><span data-stu-id="88554-128">Go through [Tutorial Overview and Prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="88554-129">Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall versão mais recente do PowerShell do Azure no seu computador.</span><span class="sxs-lookup"><span data-stu-id="88554-129">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span> <span data-ttu-id="88554-130">Neste tutorial, você deve usar entidades do PowerShell toodeploy fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="88554-130">In this tutorial, you use PowerShell toodeploy Data Factory entities.</span></span> 
* <span data-ttu-id="88554-131">(opcional) Consulte [criação de modelos de Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sobre modelos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-131">(optional) See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span>

## <a name="in-this-tutorial"></a><span data-ttu-id="88554-132">Neste tutorial</span><span class="sxs-lookup"><span data-stu-id="88554-132">In this tutorial</span></span>
<span data-ttu-id="88554-133">Neste tutorial, você pode criar uma fábrica de dados com hello entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="88554-133">In this tutorial, you create a data factory with hello following Data Factory entities:</span></span>

| <span data-ttu-id="88554-134">Entidade</span><span class="sxs-lookup"><span data-stu-id="88554-134">Entity</span></span> | <span data-ttu-id="88554-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="88554-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="88554-136">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-136">Azure Storage linked service</span></span> |<span data-ttu-id="88554-137">Vincula sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-137">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="88554-138">Armazenamento do Azure é um repositório de dados de origem hello e banco de dados do SQL Azure é Olá coletor repositório de dados para a atividade de cópia Olá Olá tutorial.</span><span class="sxs-lookup"><span data-stu-id="88554-138">Azure Storage is hello source data store and Azure SQL database is hello sink data store for hello copy activity in hello tutorial.</span></span> <span data-ttu-id="88554-139">Especifica a conta de armazenamento de saudação que contém dados de entrada hello para atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="88554-139">It specifies hello storage account that contains hello input data for hello copy activity.</span></span> |
| <span data-ttu-id="88554-140">Serviço vinculado para o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-140">Azure SQL Database linked service</span></span> |<span data-ttu-id="88554-141">Vincula sua fábrica de dados de toohello de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-141">Links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="88554-142">Ele especifica o banco de dados de SQL do Azure de saudação que armazena dados de saída de hello de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="88554-142">It specifies hello Azure SQL database that holds hello output data for hello copy activity.</span></span> |
| <span data-ttu-id="88554-143">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-143">Azure Blob input dataset</span></span> |<span data-ttu-id="88554-144">Refere-se o serviço de armazenamento do Azure vinculada toohello.</span><span class="sxs-lookup"><span data-stu-id="88554-144">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="88554-145">Olá serviço vinculado refere-se tooan conta de armazenamento do Azure e conjunto de dados de Blob do Azure Olá Especifica contêiner Olá, nome de arquivo e pasta no armazenamento de saudação que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="88554-145">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="88554-146">Conjunto de dados de saída do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="88554-146">Azure SQL output dataset</span></span> |<span data-ttu-id="88554-147">Refere-se o serviço vinculado do SQL Azure de toohello.</span><span class="sxs-lookup"><span data-stu-id="88554-147">Refers toohello Azure SQL linked service.</span></span> <span data-ttu-id="88554-148">Olá vinculado do SQL Azure serviço refere-se tooan Azure SQL server e conjunto de dados de SQL do Azure Olá Especifica o nome de Olá da tabela de saudação que contém dados de saída de saudação.</span><span class="sxs-lookup"><span data-stu-id="88554-148">hello Azure SQL linked service refers tooan Azure SQL server and hello Azure SQL dataset specifies hello name of hello table that holds hello output data.</span></span> |
| <span data-ttu-id="88554-149">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="88554-149">Data pipeline</span></span> |<span data-ttu-id="88554-150">pipeline de saudação tem uma atividade de cópia que usa Olá o conjunto de dados de blob do Azure como uma entrada de tipo e Olá conjunto de dados do SQL Azure como uma saída.</span><span class="sxs-lookup"><span data-stu-id="88554-150">hello pipeline has one activity of type Copy that takes hello Azure blob dataset as an input and hello Azure SQL dataset as an output.</span></span> <span data-ttu-id="88554-151">Olá Copiar atividade copia dados de uma tabela de tooa de BLOBs do Azure no banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="88554-151">hello copy activity copies data from an Azure blob tooa table in hello Azure SQL database.</span></span> |

<span data-ttu-id="88554-152">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="88554-152">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="88554-153">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="88554-153">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="88554-154">Há dois tipos de atividades: [atividades de movimentação de dados](data-factory-data-movement-activities.md) e [atividades de transformação de dados](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="88554-154">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="88554-155">Neste tutorial, você criará um pipeline com uma atividade (atividade de cópia).</span><span class="sxs-lookup"><span data-stu-id="88554-155">In this tutorial, you create a pipeline with one activity (copy activity).</span></span>

![Copiar Blob do Azure tooAzure banco de dados SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

<span data-ttu-id="88554-157">Olá seção a seguir fornece Olá completa Gerenciador de recursos modelo para definir entidades da fábrica de dados para que você possa executar rapidamente por meio do modelo de saudação tutorial e teste hello.</span><span class="sxs-lookup"><span data-stu-id="88554-157">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="88554-158">toounderstand como cada entidade de fábrica de dados é definida, consulte [entidades da fábrica de dados no modelo de saudação](#data-factory-entities-in-the-template) seção.</span><span class="sxs-lookup"><span data-stu-id="88554-158">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="88554-159">Modelo de JSON do Data Factory</span><span class="sxs-lookup"><span data-stu-id="88554-159">Data Factory JSON template</span></span>
<span data-ttu-id="88554-160">Olá modelo de nível superior Gerenciador de recursos para definir uma fábrica de dados é:</span><span class="sxs-lookup"><span data-stu-id="88554-160">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="88554-161">Crie um arquivo JSON chamado **ADFCopyTutorialARM.json** na **C:\ADFGetStarted** pasta com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="88554-161">Create a JSON file named **ADFCopyTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
      "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello data toobe copied." } },
      "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
      "sourceBlobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
      "sourceBlobName": { "type": "string", "metadata": { "description": "Name of hello blob in hello container that has hello data toobe copied tooAzure SQL Database table" } },
      "sqlServerName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Server that will hold hello output/copied data." } },
      "databaseName": { "type": "string", "metadata": { "description": "Name of hello Azure SQL Database in hello Azure SQL server." } },
      "sqlServerUserName": { "type": "string", "metadata": { "description": "Name of hello user that has access toohello Azure SQL server." } },
      "sqlServerPassword": { "type": "securestring", "metadata": { "description": "Password for hello user." } },
      "targetSQLTable": { "type": "string", "metadata": { "description": "Table in hello Azure SQL Database that will hold hello copied data." } 
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
                  "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="parameters-json"></a><span data-ttu-id="88554-162">Parâmetros JSON</span><span class="sxs-lookup"><span data-stu-id="88554-162">Parameters JSON</span></span>
<span data-ttu-id="88554-163">Crie um arquivo JSON chamado **ADFCopyTutorialARM Parameters.json** que contém parâmetros de modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="88554-163">Create a JSON file named **ADFCopyTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="88554-164">Especifique o nome e a chave de sua conta do Armazenamento do Azure nos parâmetros storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="88554-164">Specify name and key of your Azure Storage account for storageAccountName and storageAccountKey parameters.</span></span>  
> 
> <span data-ttu-id="88554-165">Especifique o servidor Azure SQL, o banco de dados, o usuário e a senha para os parâmetros sqlServerName, databaseName, sqlServerUserName e sqlServerPassword.</span><span class="sxs-lookup"><span data-stu-id="88554-165">Specify Azure SQL server, database, user, and password for sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters.</span></span>  

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": { 
        "storageAccountName": { "value": "<Name of hello Azure storage account>"    },
        "storageAccountKey": {
            "value": "<Key for hello Azure storage account>"
        },
        "sourceBlobContainer": { "value": "adftutorial" },
        "sourceBlobName": { "value": "emp.txt" },
        "sqlServerName": { "value": "<Name of hello Azure SQL server>" },
        "databaseName": { "value": "<Name of hello Azure SQL database>" },
        "sqlServerUserName": { "value": "<Name of hello user who has access toohello Azure SQL database>" },
        "sqlServerPassword": { "value": "<password for hello user>" },
        "targetSQLTable": { "value": "emp" }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="88554-166">Você pode ter arquivos JSON de parâmetros separados para desenvolvimento, teste e ambientes de produção que você pode usar com hello mesmo modelo JSON da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="88554-166">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="88554-167">Usando um script do PowerShell, você pode automatizar a implantação de entidades de Data Factory nesses ambientes.</span><span class="sxs-lookup"><span data-stu-id="88554-167">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span>  
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="88554-168">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="88554-168">Create data factory</span></span>
1. <span data-ttu-id="88554-169">Iniciar **Azure PowerShell** e execução Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="88554-169">Start **Azure PowerShell** and run hello following command:</span></span>
   * <span data-ttu-id="88554-170">Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-170">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
   
    ```PowerShell
    Login-AzureRmAccount    
    ```  
   * <span data-ttu-id="88554-171">Execute Olá tooview de comando a seguir todas as assinaturas de saudação para esta conta.</span><span class="sxs-lookup"><span data-stu-id="88554-171">Run hello following command tooview all hello subscriptions for this account.</span></span>
   
    ```PowerShell
    Get-AzureRmSubscription
    ```   
   * <span data-ttu-id="88554-172">Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir.</span><span class="sxs-lookup"><span data-stu-id="88554-172">Run hello following command tooselect hello subscription that you want toowork with.</span></span>
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. <span data-ttu-id="88554-173">Olá execução seguintes entidades de fábrica de dados toodeploy de comando usando o modelo do Gerenciador de recursos de saudação que você criou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="88554-173">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span>

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="88554-174">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="88554-174">Monitor pipeline</span></span>

1. <span data-ttu-id="88554-175">Faça logon no toohello [portal do Azure](https://portal.azure.com) usando sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-175">Log in toohello [Azure portal](https://portal.azure.com) using your Azure account.</span></span>
2. <span data-ttu-id="88554-176">Clique em **fábricas de dados** no hello esquerdo menu (ou) clique **mais serviços** e clique em **fábricas de dados** em **INTELLIGENCE + análise** categoria.</span><span class="sxs-lookup"><span data-stu-id="88554-176">Click **Data factories** on hello left menu (or) click **More services** and click **Data factories** under **INTELLIGENCE + ANALYTICS** category.</span></span>
   
    ![Menu Data factories](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. <span data-ttu-id="88554-178">Em Olá **fábricas de dados** página, pesquisar e localizar sua fábrica de dados (AzureBlobToAzureSQLDatabaseDF).</span><span class="sxs-lookup"><span data-stu-id="88554-178">In hello **Data factories** page, search for and find your data factory (AzureBlobToAzureSQLDatabaseDF).</span></span> 
   
    ![Pesquisar por data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. <span data-ttu-id="88554-180">Clique no seu Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="88554-180">Click your Azure data factory.</span></span> <span data-ttu-id="88554-181">Página de home Olá Olá fábrica de dados é exibida.</span><span class="sxs-lookup"><span data-stu-id="88554-181">You see hello home page for hello data factory.</span></span>
   
    ![Home page do data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. <span data-ttu-id="88554-183">Siga as instruções de [monitorar conjuntos de dados e pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline de saudação toomonitor e conjuntos de dados, você criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="88554-183">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="88554-184">Atualmente, o Visual Studio não dá suporte a monitoramento de pipelines do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="88554-184">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span>
7. <span data-ttu-id="88554-185">Quando uma fatia está em Olá **pronto** de estado, verifique se os dados de saudação copiado toohello **emp** tabela no banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="88554-185">When a slice is in hello **Ready** state, verify that hello data is copied toohello **emp** table in hello Azure SQL database.</span></span>


<span data-ttu-id="88554-186">Para obter mais informações sobre como toouse pipeline de toomonitor de folhas de portal do Azure e conjuntos de dados você tiver criado neste tutorial, consulte [monitorar conjuntos de dados e pipeline](data-factory-monitor-manage-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="88554-186">For more information on how toouse Azure portal blades toomonitor pipeline and datasets you have created in this tutorial, see [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) .</span></span>

<span data-ttu-id="88554-187">Para obter mais informações sobre como toouse Olá monitorar e gerenciar aplicativos toomonitor seus dados pipelines, consulte [monitorar e gerenciar os pipelines de fábrica de dados do Azure usando o monitoramento de aplicativo](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="88554-187">For more information on how toouse hello Monitor & Manage application toomonitor your data pipelines, see [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md).</span></span>

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="88554-188">Entidades da fábrica de dados no modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="88554-188">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="88554-189">Definir Data Factory</span><span class="sxs-lookup"><span data-stu-id="88554-189">Define data factory</span></span>
<span data-ttu-id="88554-190">Você pode definir uma fábrica de dados no modelo do Gerenciador de recursos de saudação conforme Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="88554-190">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```

<span data-ttu-id="88554-191">Olá dataFactoryName é definido como:</span><span class="sxs-lookup"><span data-stu-id="88554-191">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

<span data-ttu-id="88554-192">É uma cadeia de caracteres exclusiva com base no ID do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="88554-192">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="88554-193">Definir entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="88554-193">Defining Data Factory entities</span></span>
<span data-ttu-id="88554-194">Hello seguintes entidades da fábrica de dados estão definidas no modelo JSON hello:</span><span class="sxs-lookup"><span data-stu-id="88554-194">hello following Data Factory entities are defined in hello JSON template:</span></span> 

1. [<span data-ttu-id="88554-195">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-195">Azure Storage linked service</span></span>](#azure-storage-linked-service)
2. [<span data-ttu-id="88554-196">Serviço vinculado do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-196">Azure SQL linked service</span></span>](#azure-sql-database-linked-service)
3. [<span data-ttu-id="88554-197">Conjunto de dados de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-197">Azure blob dataset</span></span>](#azure-blob-dataset)
4. [<span data-ttu-id="88554-198">Conjunto de dados do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-198">Azure SQL dataset</span></span>](#azure-sql-dataset)
5. [<span data-ttu-id="88554-199">Pipeline de dados com a atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="88554-199">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="88554-200">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-200">Azure Storage linked service</span></span>
<span data-ttu-id="88554-201">Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-201">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="88554-202">Você criou um contêiner e carregados conta de armazenamento toothis dados como parte de [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="88554-202">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="88554-203">Especifique o nome hello e a chave da sua conta de armazenamento do Azure nesta seção.</span><span class="sxs-lookup"><span data-stu-id="88554-203">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="88554-204">Consulte [serviço vinculado do armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre o JSON propriedades usadas toodefine um armazenamento do Azure serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="88554-204">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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

<span data-ttu-id="88554-205">Olá connectionString usa parâmetros storageAccountName e storageAccountKey de saudação.</span><span class="sxs-lookup"><span data-stu-id="88554-205">hello connectionString uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="88554-206">valores de saudação para esses parâmetros passados usando um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="88554-206">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="88554-207">definição de saudação também usa variáveis: azureStroageLinkedService e dataFactoryName definido no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="88554-207">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="88554-208">Serviço vinculado para o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-208">Azure SQL Database linked service</span></span>
<span data-ttu-id="88554-209">AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-209">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="88554-210">Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="88554-210">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="88554-211">Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="88554-211">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> <span data-ttu-id="88554-212">Especifique o nome do servidor SQL Azure Olá, nome do banco de dados, nome de usuário e senha de usuário nesta seção.</span><span class="sxs-lookup"><span data-stu-id="88554-212">You specify hello Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="88554-213">Consulte [serviço vinculado do SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um SQL Azure serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="88554-213">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used toodefine an Azure SQL linked service.</span></span>  

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

<span data-ttu-id="88554-214">Olá connectionString usa sqlServerName, databaseName, sqlServerUserName e sqlServerPassword parâmetros cujos valores são passados usando um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="88554-214">hello connectionString uses sqlServerName, databaseName, sqlServerUserName, and sqlServerPassword parameters whose values are passed by using a configuration file.</span></span> <span data-ttu-id="88554-215">Olá definição também usa Olá seguir variáveis de modelo Olá: azureSqlLinkedServiceName, dataFactoryName.</span><span class="sxs-lookup"><span data-stu-id="88554-215">hello definition also uses hello following variables from hello template: azureSqlLinkedServiceName, dataFactoryName.</span></span>

#### <a name="azure-blob-dataset"></a><span data-ttu-id="88554-216">Conjunto de dados de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-216">Azure blob dataset</span></span>
<span data-ttu-id="88554-217">serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-217">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="88554-218">Na definição de conjunto de dados de blob do Azure, você deve especificar nomes de contêiner de blob, a pasta e arquivo que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="88554-218">In Azure blob dataset definition, you specify names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="88554-219">Consulte [propriedades de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-219">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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

#### <a name="azure-sql-dataset"></a><span data-ttu-id="88554-220">Conjunto de dados do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="88554-220">Azure SQL dataset</span></span>
<span data-ttu-id="88554-221">Especifique o nome de saudação da tabela Olá no banco de dados de SQL do Azure de saudação que contém dados Olá copiado da saudação armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-221">You specify hello name of hello table in hello Azure SQL database that holds hello copied data from hello Azure Blob storage.</span></span> <span data-ttu-id="88554-222">Consulte [propriedades de conjunto de dados do SQL Azure](data-factory-azure-sql-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-222">See [Azure SQL dataset properties](data-factory-azure-sql-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure SQL dataset.</span></span> 

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

#### <a name="data-pipeline"></a><span data-ttu-id="88554-223">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="88554-223">Data pipeline</span></span>
<span data-ttu-id="88554-224">Você define um pipeline que copia dados de conjunto de dados do hello BLOBs do Azure dataset toohello SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="88554-224">You define a pipeline that copies data from hello Azure blob dataset toohello Azure SQL dataset.</span></span> <span data-ttu-id="88554-225">Consulte [JSON de Pipeline](data-factory-create-pipelines.md#pipeline-json) para obter descrições dos elementos usados de JSON toodefine um pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="88554-225">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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
              "description": "Copy data frm Azure blob tooAzure SQL",
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

## <a name="reuse-hello-template"></a><span data-ttu-id="88554-226">Reutilizar Olá modelo</span><span class="sxs-lookup"><span data-stu-id="88554-226">Reuse hello template</span></span>
<span data-ttu-id="88554-227">No tutorial de saudação, você criou um modelo de definição de entidades da fábrica de dados e um modelo para passar valores para parâmetros.</span><span class="sxs-lookup"><span data-stu-id="88554-227">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="88554-228">pipeline de saudação copia dados de um armazenamento do Azure conta tooan SQL Azure banco de dados especificado por meio de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="88554-228">hello pipeline copies data from an Azure Storage account tooan Azure SQL database specified via parameters.</span></span> <span data-ttu-id="88554-229">toouse Olá ambientes de toodifferent do mesmo modelo toodeploy Data Factory entidades, crie um arquivo de parâmetro para cada ambiente e usá-lo ao implantar o ambiente toothat.</span><span class="sxs-lookup"><span data-stu-id="88554-229">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="88554-230">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="88554-230">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

<span data-ttu-id="88554-231">Observe que Olá primeiro comando usa o arquivo de parâmetro para o ambiente de desenvolvimento hello, segundo uma para Olá ambiente de teste e Olá um terceiro para o ambiente de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="88554-231">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="88554-232">Também é possível reutilizar Olá modelo tooperform repetido tarefas.</span><span class="sxs-lookup"><span data-stu-id="88554-232">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="88554-233">Por exemplo, você precisa toocreate muitos fábricas de dados com um ou mais pipelines que implementam Olá mesmo lógica, mas cada fábrica de dados usa diferentes contas de armazenamento e o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="88554-233">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Storage and SQL Database accounts.</span></span> <span data-ttu-id="88554-234">Nesse cenário, você usa Olá mesmo modelo em Olá mesmo ambiente (desenvolvimento, teste ou produção) com parâmetros diferentes arquivos toocreate fábricas de dados.</span><span class="sxs-lookup"><span data-stu-id="88554-234">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="88554-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88554-235">Next steps</span></span>
<span data-ttu-id="88554-236">Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="88554-236">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="88554-237">Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação:</span><span class="sxs-lookup"><span data-stu-id="88554-237">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="88554-238">toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="88554-238">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
