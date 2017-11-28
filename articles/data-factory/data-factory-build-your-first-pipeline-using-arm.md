---
title: Criar seu primeiro data factory (modelo do Resource Manager) | Microsoft Docs
description: "Neste tutorial, você criará um pipeline de exemplo do Azure Data Factory usando um modelo do Azure Resource Manager."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: eb9e70b9-a13a-4a27-8256-2759496be470
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: c67169f296f2f13b9ee87180f126fb1dcf10fbea
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="baa32-103">Tutorial: Criar a sua primeira Azure Data Factory usando o modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="baa32-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="baa32-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="baa32-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="baa32-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="baa32-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="baa32-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="baa32-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="baa32-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="baa32-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="baa32-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="baa32-109">API REST</span><span class="sxs-lookup"><span data-stu-id="baa32-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="baa32-110">Neste artigo, você usa os modelos do Azure Resource Manager para criar seu primeiro data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-110">In this article, you use an Azure Resource Manager template to create your first Azure data factory.</span></span> <span data-ttu-id="baa32-111">Para fazer o tutorial usando outras ferramentas/SDKs, selecione uma das opções da lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="baa32-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="baa32-112">O pipeline neste tutorial tem uma atividade: **atividade hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="baa32-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="baa32-113">Esta atividade executa um script de hive em um cluster do HDInsight do Azure que transforma os dados de entrada para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="baa32-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="baa32-114">O pipeline é agendado para ser executado uma vez por mês entre os horários de início e término especificados.</span><span class="sxs-lookup"><span data-stu-id="baa32-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="baa32-115">O pipeline de dados neste tutorial transforma os dados de entrada para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="baa32-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="baa32-116">Para obter um tutorial sobre como copiar dados usando o Azure Data Factory, confira [Tutorial: copiar dados do armazenamento de blobs para um banco de dados SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="baa32-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="baa32-117">O pipeline neste tutorial tem apenas uma atividade do tipo: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="baa32-117">The pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="baa32-118">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="baa32-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="baa32-119">E você pode encadear duas atividades (executar uma atividade após a outra) definindo o conjunto de dados de saída de uma atividade como o conjunto de dados de entrada da outra atividade.</span><span class="sxs-lookup"><span data-stu-id="baa32-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="baa32-120">Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="baa32-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="baa32-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="baa32-121">Prerequisites</span></span>
* <span data-ttu-id="baa32-122">Leia o artigo [Visão geral do tutorial](data-factory-build-your-first-pipeline.md) e concluir as etapas de **pré-requisito** .</span><span class="sxs-lookup"><span data-stu-id="baa32-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="baa32-123">Siga as instruções do artigo [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) para instalar a última versão do Azure PowerShell no computador.</span><span class="sxs-lookup"><span data-stu-id="baa32-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="baa32-124">Veja [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) para saber mais sobre os modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="baa32-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="baa32-125">Neste tutorial</span><span class="sxs-lookup"><span data-stu-id="baa32-125">In this tutorial</span></span>
| <span data-ttu-id="baa32-126">Entidade</span><span class="sxs-lookup"><span data-stu-id="baa32-126">Entity</span></span> | <span data-ttu-id="baa32-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="baa32-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="baa32-128">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-128">Azure Storage linked service</span></span> |<span data-ttu-id="baa32-129">Vincula sua conta de Armazenamento do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="baa32-129">Links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="baa32-130">A conta do Armazenamento do Azure manterá os dados de entrada e de saída para o pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="baa32-130">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> |
| <span data-ttu-id="baa32-131">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="baa32-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="baa32-132">Vincula um cluster HDInsight sob demanda ao data factory.</span><span class="sxs-lookup"><span data-stu-id="baa32-132">Links an on-demand HDInsight cluster to the data factory.</span></span> <span data-ttu-id="baa32-133">O cluster é criado automaticamente para você para processar dados e é excluído depois que o processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="baa32-133">The cluster is automatically created for you to process data and is deleted after the processing is done.</span></span> |
| <span data-ttu-id="baa32-134">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-134">Azure Blob input dataset</span></span> |<span data-ttu-id="baa32-135">Refere-se ao serviço vinculado do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-135">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="baa32-136">O serviço vinculado refere-se a uma conta de Armazenamento do Azure e o conjunto de dados de Blob do Azure especifica o contêiner, a pasta e o nome do arquivo no armazenamento que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="baa32-136">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the input data.</span></span> |
| <span data-ttu-id="baa32-137">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-137">Azure Blob output dataset</span></span> |<span data-ttu-id="baa32-138">Refere-se ao serviço vinculado do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-138">Refers to the Azure Storage linked service.</span></span> <span data-ttu-id="baa32-139">O serviço vinculado refere-se a uma conta de Armazenamento do Azure e o conjunto de dados de Blob do Azure especifica o contêiner, a pasta e o nome do arquivo no armazenamento que contém os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="baa32-139">The linked service refers to an Azure Storage account and the Azure Blob dataset specifies the container, folder, and file name in the storage that holds the output data.</span></span> |
| <span data-ttu-id="baa32-140">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="baa32-140">Data pipeline</span></span> |<span data-ttu-id="baa32-141">O pipeline tem uma atividade do tipo HDInsightHive, que consome o conjunto de dados de entrada e produz o conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="baa32-141">The pipeline has one activity of type HDInsightHive, which consumes the input dataset and produces the output dataset.</span></span> |

<span data-ttu-id="baa32-142">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="baa32-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="baa32-143">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="baa32-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="baa32-144">Há dois tipos de atividades: [atividades de movimentação de dados](data-factory-data-movement-activities.md) e [atividades de transformação de dados](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="baa32-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="baa32-145">Neste tutorial, você criará um pipeline com uma atividade (atividade do Hive).</span><span class="sxs-lookup"><span data-stu-id="baa32-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="baa32-146">A seção a seguir fornece o modelo do Resource Manager completo para definir entidades de Data Factory de modo que você possa percorrer o tutorial rapidamente e testar o modelo.</span><span class="sxs-lookup"><span data-stu-id="baa32-146">The following section provides the complete Resource Manager template for defining Data Factory entities so that you can quickly run through the tutorial and test the template.</span></span> <span data-ttu-id="baa32-147">Para entender como cada entidade de Data Factory é definida, consulte a seção [Entidades de Data Factory no modelo](#data-factory-entities-in-the-template).</span><span class="sxs-lookup"><span data-stu-id="baa32-147">To understand how each Data Factory entity is defined, see [Data Factory entities in the template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="baa32-148">Modelo de JSON do Data Factory</span><span class="sxs-lookup"><span data-stu-id="baa32-148">Data Factory JSON template</span></span>
<span data-ttu-id="baa32-149">O modelo do Resource Manager de nível superior para definir um data factory é:</span><span class="sxs-lookup"><span data-stu-id="baa32-149">The top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="baa32-150">Crie um arquivo JSON denominado **ADFTutorialARM.json** na pasta **C:\ADFGetStarted** com este conteúdo:</span><span class="sxs-lookup"><span data-stu-id="baa32-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with the following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of the Azure storage account that contains the input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for the Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of the blob container in the Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that has the input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of the input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that will hold the transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "The folder in the blob container that contains the Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of the hive query (HQL) file." } }
    },
    "variables": {
          "dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
          "azureStorageLinkedServiceName": "AzureStorageLinkedService",
          "hdInsightOnDemandLinkedServiceName": "HDInsightOnDemandLinkedService",
          "blobInputDatasetName": "AzureBlobInput",
          "blobOutputDatasetName": "AzureBlobOutput",
          "pipelineName": "HiveTransformPipeline"
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
            "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "HDInsightOnDemand",
                  "typeProperties": {
                    "version": "3.5",
                    "clusterSize": 1,
                    "timeToLive": "00:05:00",
                    "osType": "Linux",
                    "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
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
                  "typeProperties": {
                    "fileName": "[parameters('inputBlobName')]",
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
                    "interval": 1
                  },
                  "external": true
            }
          },
          {
            "type": "datasets",
            "name": "[variables('blobOutputDatasetName')]",
            "dependsOn": [
                  "[variables('dataFactoryName')]",
                  "[variables('azureStorageLinkedServiceName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "type": "AzureBlob",
                  "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
                  "typeProperties": {
                    "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
                    "format": {
                          "type": "TextFormat",
                          "columnDelimiter": ","
                    }
                  },
                  "availability": {
                    "frequency": "Month",
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
                  "[variables('hdInsightOnDemandLinkedServiceName')]",
                  "[variables('blobInputDatasetName')]",
                  "[variables('blobOutputDatasetName')]"
            ],
            "apiVersion": "2015-10-01",
            "properties": {
                  "description": "Pipeline that transforms data using Hive script.",
                  "activities": [
                {
                      "type": "HDInsightHive",
                      "typeProperties": {
                        "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                        "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                        "defines": {
                              "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                              "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                        }
                      },
                      "inputs": [
                        {
                              "name": "[variables('blobInputDatasetName')]"
                        }
                      ],
                      "outputs": [
                        {
                              "name": "[variables('blobOutputDatasetName')]"
                        }
                      ],
                      "policy": {
                        "concurrency": 1,
                        "retry": 3
                      },
                      "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                      },
                      "name": "RunSampleHiveActivity",
                      "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
                }
                  ],
                  "start": "2017-07-01T00:00:00Z",
                  "end": "2017-07-02T00:00:00Z",
                  "isPaused": false
              }
          }
        ]
      }
    ]
}
```

> [!NOTE]
> <span data-ttu-id="baa32-151">Você pode encontrar outro exemplo de modelo do Gerenciador de Recursos para criar um Azure data factory em [Tutorial: criar um pipeline com atividade de cópia usando um modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="baa32-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="baa32-152">Parâmetros JSON</span><span class="sxs-lookup"><span data-stu-id="baa32-152">Parameters JSON</span></span>
<span data-ttu-id="baa32-153">Crie um arquivo JSON chamado **ADFTutorialARM-Parameters.json** que contenha os parâmetros para o modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="baa32-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for the Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="baa32-154">Especifique o nome e a chave da conta de armazenamento do Azure para os parâmetros **storageAccountName** e **storageAccountKey** nesse arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="baa32-154">Specify the name and key of your Azure Storage account for the **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
> 
> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "value": "<Name of your Azure Storage account>"
        },
        "storageAccountKey": {
            "value": "<Key of your Azure Storage account>"
        },
        "blobContainer": {
            "value": "adfgetstarted"
        },
        "inputBlobFolder": {
            "value": "inputdata"
        },
        "inputBlobName": {
            "value": "input.log"
        },
        "outputBlobFolder": {
            "value": "partitioneddata"
        },
        "hiveScriptFolder": {
              "value": "script"
        },
        "hiveScriptFile": {
              "value": "partitionweblogs.hql"
        }
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="baa32-155">Você pode ter arquivos JSON de parâmetros separados para desenvolvimento, teste e ambientes de produção que pode usar com o mesmo modelo JSON do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="baa32-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with the same Data Factory JSON template.</span></span> <span data-ttu-id="baa32-156">Usando um script do PowerShell, você pode automatizar a implantação de entidades de Data Factory nesses ambientes.</span><span class="sxs-lookup"><span data-stu-id="baa32-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="baa32-157">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="baa32-157">Create data factory</span></span>
1. <span data-ttu-id="baa32-158">Inicie o **Azure PowerShell** e execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="baa32-158">Start **Azure PowerShell** and run the following command:</span></span> 
   * <span data-ttu-id="baa32-159">Execute o comando a seguir e insira o nome de usuário e a senha que você usa para entrar no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-159">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="baa32-160">Execute o comando a seguir para exibir todas as assinaturas dessa conta.</span><span class="sxs-lookup"><span data-stu-id="baa32-160">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="baa32-161">Execute o comando a seguir para selecionar a assinatura com a qual deseja trabalhar.</span><span class="sxs-lookup"><span data-stu-id="baa32-161">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="baa32-162">Esta assinatura deve ser igual à que você usou no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-162">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="baa32-163">Execute o comando a seguir para implantar entidades do Data Factory usando o modelo do Resource Manager criado na Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="baa32-163">Run the following command to deploy Data Factory entities using the Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="baa32-164">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="baa32-164">Monitor pipeline</span></span>
1. <span data-ttu-id="baa32-165">Depois de fazer logon no [portal do Azure](https://portal.azure.com/), clique em **Procurar** e selecione **Data factories**.</span><span class="sxs-lookup"><span data-stu-id="baa32-165">After logging in to the [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="baa32-166">![Procurar->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="baa32-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="baa32-167">Na folha **Data Factories**, clique no data factory (**TutorialFactoryARM**) que você criou.</span><span class="sxs-lookup"><span data-stu-id="baa32-167">In the **Data Factories** blade, click the data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="baa32-168">Na folha **Data Factory** do seu data factory, clique em **Diagrama**.</span><span class="sxs-lookup"><span data-stu-id="baa32-168">In the **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Bloco Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="baa32-170">Na **Exibição de Diagrama**, você tem uma visão geral dos pipelines e dos conjuntos de dados usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="baa32-170">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>
   
   ![Exibição de Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="baa32-172">Na Exibição de diagrama, clique duas vezes no conjunto de dados **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="baa32-172">In the Diagram View, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="baa32-173">Você verá a fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="baa32-173">You see that the slice that is currently being processed.</span></span>
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="baa32-175">Quando o processamento for concluído, você verá a fatia no estado **Pronto** .</span><span class="sxs-lookup"><span data-stu-id="baa32-175">When processing is done, you see the slice in **Ready** state.</span></span> <span data-ttu-id="baa32-176">A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="baa32-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="baa32-177">Portanto, espere que o pipeline demore **cerca de 30 minutos** para processar a fatia.</span><span class="sxs-lookup"><span data-stu-id="baa32-177">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="baa32-179">Quando a fatia estiver no estado **Pronto**, verifique a pasta **partitioneddata** no contêiner **adfgetstarted** em seu armazenamento de blobs para os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="baa32-179">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

<span data-ttu-id="baa32-180">Confira [Monitorar os conjuntos de dados e o pipeline](data-factory-monitor-manage-pipelines.md) para obter instruções sobre como usar as folhas do portal do Azure para monitorar o pipeline e os conjuntos de dados que você criou neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="baa32-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal blades to monitor the pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="baa32-181">Você também pode usar Monitorar e gerenciar aplicativos para monitorar os pipelines de dados.</span><span class="sxs-lookup"><span data-stu-id="baa32-181">You can also use Monitor and Manage App to monitor your data pipelines.</span></span> <span data-ttu-id="baa32-182">Veja [Monitorar e gerenciar os pipelines do Azure Data Factory usando o Aplicativo de Monitoramento](data-factory-monitor-manage-app.md) para obter detalhes sobre a utilização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="baa32-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using the application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="baa32-183">O arquivo de entrada é excluído quando a fatia é processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="baa32-183">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="baa32-184">Portanto, se você quiser executar novamente a fatia ou fazer o tutorial novamente, carregue o arquivo de entrada (input.log) na pasta inputdata do contêiner adfgetstarted.</span><span class="sxs-lookup"><span data-stu-id="baa32-184">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="baa32-185">Entidades do Data Factory no modelo</span><span class="sxs-lookup"><span data-stu-id="baa32-185">Data Factory entities in the template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="baa32-186">Definir Data Factory</span><span class="sxs-lookup"><span data-stu-id="baa32-186">Define data factory</span></span>
<span data-ttu-id="baa32-187">Você pode definir um Data Factory no modelo do Resource Manager, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="baa32-187">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="baa32-188">O dataFactoryName é definido como:</span><span class="sxs-lookup"><span data-stu-id="baa32-188">The dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="baa32-189">É uma cadeia de caracteres exclusiva com base na ID de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="baa32-189">It is a unique string based on the resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="baa32-190">Definir entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="baa32-190">Defining Data Factory entities</span></span>
<span data-ttu-id="baa32-191">As seguintes entidades de Data Factory são definidas no modelo JSON:</span><span class="sxs-lookup"><span data-stu-id="baa32-191">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="baa32-192">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="baa32-193">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="baa32-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="baa32-194">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="baa32-195">Conjunto de dados de saída do blob do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="baa32-196">Pipeline com a Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="baa32-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="baa32-197">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-197">Azure Storage linked service</span></span>
<span data-ttu-id="baa32-198">Especifique o nome e a chave da sua conta de armazenamento do Azure nesta seção.</span><span class="sxs-lookup"><span data-stu-id="baa32-198">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="baa32-199">Confira [Serviço vinculado de armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre os elementos JSON para definir um serviço vinculado de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="baa32-200">A **connectionString** usa os parâmetros storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="baa32-200">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="baa32-201">Os valores para esses parâmetros são passados pelo uso de um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="baa32-201">The values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="baa32-202">A definição também usa variáveis: azureStroageLinkedService e dataFactoryName definidos no modelo.</span><span class="sxs-lookup"><span data-stu-id="baa32-202">The definition also uses variables: azureStroageLinkedService and dataFactoryName defined in the template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="baa32-203">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="baa32-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="baa32-204">Confira o artigo [Serviços vinculados de computação](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes sobre as propriedades JSON usadas para definir um serviço vinculado do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="baa32-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

```json
{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "[variables('azureStorageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="baa32-205">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="baa32-205">Note the following points:</span></span> 

* <span data-ttu-id="baa32-206">O Data Factory cria um cluster HDInsight **baseado no Linux** para você com o JSON acima.</span><span class="sxs-lookup"><span data-stu-id="baa32-206">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="baa32-207">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="baa32-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="baa32-208">Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="baa32-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="baa32-209">Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="baa32-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="baa32-210">O cluster HDInsight cria um **contêiner padrão** no armazenamento de blobs especificado no JSON (**nomeServiçoVinculado**).</span><span class="sxs-lookup"><span data-stu-id="baa32-210">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="baa32-211">O HDInsight não exclui esse contêiner quando o cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="baa32-211">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="baa32-212">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="baa32-212">This behavior is by design.</span></span> <span data-ttu-id="baa32-213">Com o serviço vinculado HDInsight sob demanda, um cluster HDInsight é criado sempre que uma fatia precisa ser processada, a menos que haja um cluster ativo existente (**timeToLive**), e é excluído quando o processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="baa32-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>
  
    <span data-ttu-id="baa32-214">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="baa32-215">Se você não precisa deles para solução de problemas dos trabalhos, convém excluí-los para reduzir o custo de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="baa32-215">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="baa32-216">Os nomes desses contêineres seguem um padrão: "adf**nomeseudatafactory**-**nomeserviçovinculado**- carimbodatahora".</span><span class="sxs-lookup"><span data-stu-id="baa32-216">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="baa32-217">Use ferramentas como o [Gerenciador de Armazenamento da Microsoft](http://storageexplorer.com/) para excluir contêineres do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="baa32-218">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="baa32-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="baa32-219">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-219">Azure blob input dataset</span></span>
<span data-ttu-id="baa32-220">Você especifica os nomes do contêiner de blob, da pasta e do arquivo que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="baa32-220">You specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="baa32-221">Confira [Propriedades de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre os propriedades JSON usadas para definir um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

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
        "typeProperties": {
            "fileName": "[parameters('inputBlobName')]",
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('inputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true
    }
}
```
<span data-ttu-id="baa32-222">Essa definição usa os seguintes parâmetros definidos no modelo de parâmetro: blobContainer, inputBlobFolder e inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="baa32-222">This definition uses the following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="baa32-223">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="baa32-223">Azure Blob output dataset</span></span>
<span data-ttu-id="baa32-224">Especifique os nomes de contêiner de blob e a pasta que contém os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="baa32-224">You specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="baa32-225">Confira [Propriedades de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre os propriedades JSON usadas para definir um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="baa32-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

```json
{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('azureStorageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "[concat(parameters('blobContainer'), '/', parameters('outputBlobFolder'))]",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="baa32-226">Essa definição usa os seguintes parâmetros definidos no modelo de parâmetro: blobContainer e outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="baa32-226">This definition uses the following parameters defined in the parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="baa32-227">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="baa32-227">Data pipeline</span></span>
<span data-ttu-id="baa32-228">Você define um pipeline que transforma dados executando o script Hive em um cluster do Azure HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="baa32-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="baa32-229">Confira [JSON de Pipeline](data-factory-create-pipelines.md#pipeline-json) para obter descrições dos elementos JSON usados para definir um pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="baa32-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[variables('pipelineName')]",
    "dependsOn": [
        "[variables('dataFactoryName')]",
        "[variables('azureStorageLinkedServiceName')]",
        "[variables('hdInsightOnDemandLinkedServiceName')]",
        "[variables('blobInputDatasetName')]",
        "[variables('blobOutputDatasetName')]"
    ],
    "apiVersion": "2015-10-01",
    "properties": {
        "description": "Pipeline that transforms data using Hive script.",
        "activities": [
        {
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "[concat(parameters('blobContainer'), '/', parameters('hiveScriptFolder'), '/', parameters('hiveScriptFile'))]",
                "scriptLinkedService": "[variables('azureStorageLinkedServiceName')]",
                "defines": {
                    "inputtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('inputBlobFolder'))]",
                    "partitionedtable": "[concat('wasb://', parameters('blobContainer'), '@', parameters('storageAccountName'), '.blob.core.windows.net/', parameters('outputBlobFolder'))]"
                }
            },
            "inputs": [
            {
                "name": "[variables('blobInputDatasetName')]"
            }
            ],
            "outputs": [
            {
                "name": "[variables('blobOutputDatasetName')]"
            }
            ],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "[variables('hdInsightOnDemandLinkedServiceName')]"
        }
        ],
        "start": "2017-07-01T00:00:00Z",
        "end": "2017-07-02T00:00:00Z",
        "isPaused": false
    }
}
```

## <a name="reuse-the-template"></a><span data-ttu-id="baa32-230">Reutilizar o modelo</span><span class="sxs-lookup"><span data-stu-id="baa32-230">Reuse the template</span></span>
<span data-ttu-id="baa32-231">No tutorial, você criou um modelo para definir entidades de Data Factory e um modelo para passar valores para parâmetros.</span><span class="sxs-lookup"><span data-stu-id="baa32-231">In the tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="baa32-232">Para usar o mesmo modelo para implantar as entidades de Data Factory em ambientes diferentes, você cria um arquivo de parâmetro para cada ambiente e usa-o ao implantar esse ambiente.</span><span class="sxs-lookup"><span data-stu-id="baa32-232">To use the same template to deploy Data Factory entities to different environments, you create a parameter file for each environment and use it when deploying to that environment.</span></span>     

<span data-ttu-id="baa32-233">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="baa32-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="baa32-234">Observe que o primeiro comando usa o arquivo de parâmetro para o ambiente de desenvolvimento, outro para o ambiente de teste e um terceiro para o ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="baa32-234">Notice that the first command uses parameter file for the development environment, second one for the test environment, and the third one for the production environment.</span></span>  

<span data-ttu-id="baa32-235">Também é possível reutilizar o modelo para executar tarefas repetidas.</span><span class="sxs-lookup"><span data-stu-id="baa32-235">You can also reuse the template to perform repeated tasks.</span></span> <span data-ttu-id="baa32-236">Por exemplo, você precisa criar vários data factories com um ou mais pipelines que implementem a mesma lógica, mas cada data factory usa contas de Banco de Dados SQL e Armazenamento do Azure diferentes.</span><span class="sxs-lookup"><span data-stu-id="baa32-236">For example, you need to create many data factories with one or more pipelines that implement the same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="baa32-237">Nesse cenário, você usa o mesmo modelo no mesmo ambiente (desenvolvimento, teste ou produção) com arquivos de parâmetros diferentes para criar data factories.</span><span class="sxs-lookup"><span data-stu-id="baa32-237">In this scenario, you use the same template in the same environment (dev, test, or production) with different parameter files to create data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="baa32-238">Modelo do Resource Manager para criar um gateway</span><span class="sxs-lookup"><span data-stu-id="baa32-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="baa32-239">Aqui está um exemplo de modelo do Resource Manager para criar um gateway lógico na parte traseira.</span><span class="sxs-lookup"><span data-stu-id="baa32-239">Here is a sample Resource Manager template for creating a logical gateway in the back.</span></span> <span data-ttu-id="baa32-240">Instale um gateway em seu computador local ou na VM IaaS do Azure e registrar o gateway no serviço Data Factory usando uma chave.</span><span class="sxs-lookup"><span data-stu-id="baa32-240">Install a gateway on your on-premises computer or Azure IaaS VM and register the gateway with Data Factory service using a key.</span></span> <span data-ttu-id="baa32-241">Confira [Mover dados entre o local e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="baa32-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
    },
    "variables": {
        "dataFactoryName":  "GatewayUsingArmDF",
        "apiVersion": "2015-10-01",
        "singleQuote": "'"
    },
    "resources": [
        {
            "name": "[variables('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "eastus",
            "resources": [
                {
                    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', variables('dataFactoryName'))]" ],
                    "type": "gateways",
                    "apiVersion": "[variables('apiVersion')]",
                    "name": "GatewayUsingARM",
                    "properties": {
                        "description": "my gateway"
                    }
                }            
            ]
        }
    ]
}
```
<span data-ttu-id="baa32-242">O modelo cria uma data factory chamada GatewayUsingArmDF com um gateway chamado: GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="baa32-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="baa32-243">Consulte também</span><span class="sxs-lookup"><span data-stu-id="baa32-243">See Also</span></span>
| <span data-ttu-id="baa32-244">Tópico</span><span class="sxs-lookup"><span data-stu-id="baa32-244">Topic</span></span> | <span data-ttu-id="baa32-245">Descrição</span><span class="sxs-lookup"><span data-stu-id="baa32-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="baa32-246">Pipelines</span><span class="sxs-lookup"><span data-stu-id="baa32-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="baa32-247">Este artigo o ajuda a compreender pipelines e atividades no Azure Data Factory e como usá-los para construir fluxos de trabalho orientados a dados de ponta a ponta para seu cenário ou negócio.</span><span class="sxs-lookup"><span data-stu-id="baa32-247">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="baa32-248">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="baa32-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="baa32-249">Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="baa32-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="baa32-250">Agendamento e execução</span><span class="sxs-lookup"><span data-stu-id="baa32-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="baa32-251">Este artigo explica os aspectos de agendamento e execução do modelo de aplicativo do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="baa32-251">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="baa32-252">Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento</span><span class="sxs-lookup"><span data-stu-id="baa32-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="baa32-253">Este artigo descreve como monitorar, gerenciar e depurar seus pipelines usando o Aplicativo de Monitoramento e Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="baa32-253">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

