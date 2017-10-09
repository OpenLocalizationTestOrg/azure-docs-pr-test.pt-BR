---
title: "aaaBuild sua primeira fábrica de dados (modelo do Gerenciador de recursos) | Microsoft Docs"
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
ms.openlocfilehash: fa08cd1ac3a0e5c5bf4bd4c6bd9dfa6dba9f4319
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a><span data-ttu-id="839a9-103">Tutorial: Criar a sua primeira Azure Data Factory usando o modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="839a9-103">Tutorial: Build your first Azure data factory using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="839a9-104">Visão geral e pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="839a9-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="839a9-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="839a9-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="839a9-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="839a9-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="839a9-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="839a9-108">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="839a9-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="839a9-109">API REST</span><span class="sxs-lookup"><span data-stu-id="839a9-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

<span data-ttu-id="839a9-110">Neste artigo, você usar um toocreate de modelo do Gerenciador de recursos do Azure a primeira data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="839a9-110">In this article, you use an Azure Resource Manager template toocreate your first Azure data factory.</span></span> <span data-ttu-id="839a9-111">tutorial de saudação toodo usando outras ferramentas/SDKs, selecione uma das opções de saudação da lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="839a9-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="839a9-112">pipeline de saudação neste tutorial tem uma atividade: **atividade Hive do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="839a9-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="839a9-113">Essa atividade executa um script do hive em um cluster de HDInsight do Azure que transforma dados de saída de tooproduce de entrada.</span><span class="sxs-lookup"><span data-stu-id="839a9-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="839a9-114">pipeline de saudação é agendado toorun depois de um mês entre hello especificar horários de início e término.</span><span class="sxs-lookup"><span data-stu-id="839a9-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="839a9-115">pipeline de dados Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="839a9-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="839a9-116">Para obter um tutorial sobre como toocopy dados usando a fábrica de dados do Azure, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="839a9-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="839a9-117">pipeline de saudação neste tutorial tem apenas uma atividade do tipo: HDInsightHive.</span><span class="sxs-lookup"><span data-stu-id="839a9-117">hello pipeline in this tutorial has only one activity of type: HDInsightHive.</span></span> <span data-ttu-id="839a9-118">Um pipeline pode ter mais de uma atividade.</span><span class="sxs-lookup"><span data-stu-id="839a9-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="839a9-119">E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada.</span><span class="sxs-lookup"><span data-stu-id="839a9-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="839a9-120">Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="839a9-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="839a9-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="839a9-121">Prerequisites</span></span>
* <span data-ttu-id="839a9-122">Leia [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e hello completa **pré-requisito** etapas.</span><span class="sxs-lookup"><span data-stu-id="839a9-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="839a9-123">Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall versão mais recente do PowerShell do Azure no seu computador.</span><span class="sxs-lookup"><span data-stu-id="839a9-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="839a9-124">Consulte [criação de modelos de Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sobre modelos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="839a9-124">See [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn about Azure Resource Manager templates.</span></span> 

## <a name="in-this-tutorial"></a><span data-ttu-id="839a9-125">Neste tutorial</span><span class="sxs-lookup"><span data-stu-id="839a9-125">In this tutorial</span></span>
| <span data-ttu-id="839a9-126">Entidade</span><span class="sxs-lookup"><span data-stu-id="839a9-126">Entity</span></span> | <span data-ttu-id="839a9-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="839a9-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="839a9-128">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-128">Azure Storage linked service</span></span> |<span data-ttu-id="839a9-129">Vincula sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="839a9-129">Links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="839a9-130">Olá conta de armazenamento do Azure mantém Olá dados de entrada e saídos para o pipeline de saudação neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="839a9-130">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> |
| <span data-ttu-id="839a9-131">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="839a9-131">HDInsight on-demand linked service</span></span> |<span data-ttu-id="839a9-132">Vincula uma fábrica de dados sob demanda HDInsight cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="839a9-132">Links an on-demand HDInsight cluster toohello data factory.</span></span> <span data-ttu-id="839a9-133">cluster de saudação é criado automaticamente para você tooprocess dados e é excluída após a conclusão do processamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="839a9-133">hello cluster is automatically created for you tooprocess data and is deleted after hello processing is done.</span></span> |
| <span data-ttu-id="839a9-134">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-134">Azure Blob input dataset</span></span> |<span data-ttu-id="839a9-135">Refere-se o serviço de armazenamento do Azure vinculada toohello.</span><span class="sxs-lookup"><span data-stu-id="839a9-135">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="839a9-136">Olá serviço vinculado refere-se tooan conta de armazenamento do Azure e conjunto de dados de Blob do Azure Olá Especifica contêiner Olá, nome de arquivo e pasta no armazenamento de saudação que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-136">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello input data.</span></span> |
| <span data-ttu-id="839a9-137">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-137">Azure Blob output dataset</span></span> |<span data-ttu-id="839a9-138">Refere-se o serviço de armazenamento do Azure vinculada toohello.</span><span class="sxs-lookup"><span data-stu-id="839a9-138">Refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="839a9-139">Olá serviço vinculado refere-se tooan conta de armazenamento do Azure e conjunto de dados de Blob do Azure Olá Especifica contêiner Olá, nome de arquivo e pasta no armazenamento de saudação que contém dados de saída de saudação.</span><span class="sxs-lookup"><span data-stu-id="839a9-139">hello linked service refers tooan Azure Storage account and hello Azure Blob dataset specifies hello container, folder, and file name in hello storage that holds hello output data.</span></span> |
| <span data-ttu-id="839a9-140">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="839a9-140">Data pipeline</span></span> |<span data-ttu-id="839a9-141">pipeline de saudação tem uma atividade do tipo HDInsightHive, que consome Olá conjunto de dados de entrada e produz o conjunto de dados de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-141">hello pipeline has one activity of type HDInsightHive, which consumes hello input dataset and produces hello output dataset.</span></span> |

<span data-ttu-id="839a9-142">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="839a9-142">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="839a9-143">Um pipeline em um data factory pode ter uma ou mais atividades.</span><span class="sxs-lookup"><span data-stu-id="839a9-143">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="839a9-144">Há dois tipos de atividades: [atividades de movimentação de dados](data-factory-data-movement-activities.md) e [atividades de transformação de dados](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="839a9-144">There are two types of activities: [data movement activities](data-factory-data-movement-activities.md) and [data transformation activities](data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="839a9-145">Neste tutorial, você criará um pipeline com uma atividade (atividade do Hive).</span><span class="sxs-lookup"><span data-stu-id="839a9-145">In this tutorial, you create a pipeline with one activity (Hive activity).</span></span>

<span data-ttu-id="839a9-146">Olá seção a seguir fornece Olá completa Gerenciador de recursos modelo para definir entidades da fábrica de dados para que você possa executar rapidamente por meio do modelo de saudação tutorial e teste hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-146">hello following section provides hello complete Resource Manager template for defining Data Factory entities so that you can quickly run through hello tutorial and test hello template.</span></span> <span data-ttu-id="839a9-147">toounderstand como cada entidade de fábrica de dados é definida, consulte [entidades da fábrica de dados no modelo de saudação](#data-factory-entities-in-the-template) seção.</span><span class="sxs-lookup"><span data-stu-id="839a9-147">toounderstand how each Data Factory entity is defined, see [Data Factory entities in hello template](#data-factory-entities-in-the-template) section.</span></span>

## <a name="data-factory-json-template"></a><span data-ttu-id="839a9-148">Modelo de JSON do Data Factory</span><span class="sxs-lookup"><span data-stu-id="839a9-148">Data Factory JSON template</span></span>
<span data-ttu-id="839a9-149">Olá modelo de nível superior Gerenciador de recursos para definir uma fábrica de dados é:</span><span class="sxs-lookup"><span data-stu-id="839a9-149">hello top-level Resource Manager template for defining a data factory is:</span></span> 

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
<span data-ttu-id="839a9-150">Crie um arquivo JSON chamado **ADFTutorialARM.json** na **C:\ADFGetStarted** pasta com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="839a9-150">Create a JSON file named **ADFTutorialARM.json** in **C:\ADFGetStarted** folder with hello following content:</span></span>

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": {
        "storageAccountName": { "type": "string", "metadata": { "description": "Name of hello Azure storage account that contains hello input/output data." } },
          "storageAccountKey": { "type": "securestring", "metadata": { "description": "Key for hello Azure storage account." } },
          "blobContainer": { "type": "string", "metadata": { "description": "Name of hello blob container in hello Azure Storage account." } },
          "inputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that has hello input file." } },
          "inputBlobName": { "type": "string", "metadata": { "description": "Name of hello input file/blob." } },
          "outputBlobFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that will hold hello transformed data." } },
          "hiveScriptFolder": { "type": "string", "metadata": { "description": "hello folder in hello blob container that contains hello Hive query file." } },
          "hiveScriptFile": { "type": "string", "metadata": { "description": "Name of hello hive query (HQL) file." } }
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
> <span data-ttu-id="839a9-151">Você pode encontrar outro exemplo de modelo do Gerenciador de Recursos para criar um Azure data factory em [Tutorial: criar um pipeline com atividade de cópia usando um modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="839a9-151">You can find another example of Resource Manager template for creating an Azure data factory on [Tutorial: Create a pipeline with Copy Activity using an Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).</span></span>  
> 
> 

## <a name="parameters-json"></a><span data-ttu-id="839a9-152">Parâmetros JSON</span><span class="sxs-lookup"><span data-stu-id="839a9-152">Parameters JSON</span></span>
<span data-ttu-id="839a9-153">Crie um arquivo JSON chamado **ADFTutorialARM Parameters.json** que contém parâmetros de modelo do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-153">Create a JSON file named **ADFTutorialARM-Parameters.json** that contains parameters for hello Azure Resource Manager template.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="839a9-154">Especificar nome de saudação e a chave da sua conta de armazenamento do Azure para Olá **storageAccountName** e **storageAccountKey** parâmetros nesse arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="839a9-154">Specify hello name and key of your Azure Storage account for hello **storageAccountName** and **storageAccountKey** parameters in this parameter file.</span></span> 
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
> <span data-ttu-id="839a9-155">Você pode ter arquivos JSON de parâmetros separados para desenvolvimento, teste e ambientes de produção que você pode usar com hello mesmo modelo JSON da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="839a9-155">You may have separate parameter JSON files for development, testing, and production environments that you can use with hello same Data Factory JSON template.</span></span> <span data-ttu-id="839a9-156">Usando um script do PowerShell, você pode automatizar a implantação de entidades de Data Factory nesses ambientes.</span><span class="sxs-lookup"><span data-stu-id="839a9-156">By using a Power Shell script, you can automate deploying Data Factory entities in these environments.</span></span> 
> 
> 

## <a name="create-data-factory"></a><span data-ttu-id="839a9-157">Criar um data factory</span><span class="sxs-lookup"><span data-stu-id="839a9-157">Create data factory</span></span>
1. <span data-ttu-id="839a9-158">Iniciar **Azure PowerShell** e execução Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="839a9-158">Start **Azure PowerShell** and run hello following command:</span></span> 
   * <span data-ttu-id="839a9-159">Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="839a9-159">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * <span data-ttu-id="839a9-160">Execute Olá tooview de comando a seguir todas as assinaturas de saudação para esta conta.</span><span class="sxs-lookup"><span data-stu-id="839a9-160">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * <span data-ttu-id="839a9-161">Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir.</span><span class="sxs-lookup"><span data-stu-id="839a9-161">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="839a9-162">Essa assinatura deve ser Olá mesmas Olá aquele que você usou no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="839a9-162">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. <span data-ttu-id="839a9-163">Olá execução seguintes entidades de fábrica de dados toodeploy de comando usando o modelo do Gerenciador de recursos de saudação que você criou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="839a9-163">Run hello following command toodeploy Data Factory entities using hello Resource Manager template you created in Step 1.</span></span> 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a><span data-ttu-id="839a9-164">Monitorar o pipeline</span><span class="sxs-lookup"><span data-stu-id="839a9-164">Monitor pipeline</span></span>
1. <span data-ttu-id="839a9-165">Depois de fazer logon em toohello [portal do Azure](https://portal.azure.com/), clique em **procurar** e selecione **fábricas de dados**.</span><span class="sxs-lookup"><span data-stu-id="839a9-165">After logging in toohello [Azure portal](https://portal.azure.com/), Click **Browse** and select **Data factories**.</span></span>
     <span data-ttu-id="839a9-166">![Procurar->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span><span class="sxs-lookup"><span data-stu-id="839a9-166">![Browse->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)</span></span>
2. <span data-ttu-id="839a9-167">Em hello **fábricas de dados** folha, clique em fábrica de dados hello (**TutorialFactoryARM**) criado por você.</span><span class="sxs-lookup"><span data-stu-id="839a9-167">In hello **Data Factories** blade, click hello data factory (**TutorialFactoryARM**) you created.</span></span>    
3. <span data-ttu-id="839a9-168">Em Olá **Data Factory** folha sua fábrica de dados, clique em **diagrama**.</span><span class="sxs-lookup"><span data-stu-id="839a9-168">In hello **Data Factory** blade for your data factory, click **Diagram**.</span></span>

     ![Bloco Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. <span data-ttu-id="839a9-170">Em Olá **exibição de diagrama**, consulte uma visão geral dos pipelines hello e conjuntos de dados usados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="839a9-170">In hello **Diagram View**, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>
   
   ![Exibição de diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. <span data-ttu-id="839a9-172">Na exibição de diagrama de Olá, clique duas vezes em dataset Olá **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="839a9-172">In hello Diagram View, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="839a9-173">Você verá essa fatia Olá que está sendo processada atualmente.</span><span class="sxs-lookup"><span data-stu-id="839a9-173">You see that hello slice that is currently being processed.</span></span>
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. <span data-ttu-id="839a9-175">Quando o processamento é concluído, você verá fatia Olá **pronto** estado.</span><span class="sxs-lookup"><span data-stu-id="839a9-175">When processing is done, you see hello slice in **Ready** state.</span></span> <span data-ttu-id="839a9-176">A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente).</span><span class="sxs-lookup"><span data-stu-id="839a9-176">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="839a9-177">Portanto, espere Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá fatia.</span><span class="sxs-lookup"><span data-stu-id="839a9-177">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. <span data-ttu-id="839a9-179">Quando a fatia hello está em **pronto** de estado, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** contêiner no seu armazenamento de blob para Olá dados de saída.</span><span class="sxs-lookup"><span data-stu-id="839a9-179">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

<span data-ttu-id="839a9-180">Consulte [monitorar conjuntos de dados e pipeline](data-factory-monitor-manage-pipelines.md) para obter instruções sobre como o pipeline de saudação do toouse Olá folhas portal do Azure toomonitor e conjuntos de dados você tiver criado neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="839a9-180">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal blades toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

<span data-ttu-id="839a9-181">Você também pode usar o Monitor e gerenciar aplicativos toomonitor seus pipelines de dados.</span><span class="sxs-lookup"><span data-stu-id="839a9-181">You can also use Monitor and Manage App toomonitor your data pipelines.</span></span> <span data-ttu-id="839a9-182">Consulte [monitorar e gerenciar os pipelines de fábrica de dados do Azure usando o monitoramento de aplicativo](data-factory-monitor-manage-app.md) para obter detalhes sobre como usar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-182">See [Monitor and manage Azure Data Factory pipelines using Monitoring App](data-factory-monitor-manage-app.md) for details about using hello application.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="839a9-183">arquivo de entrada Hello é excluído quando a fatia de saudação é processada com êxito.</span><span class="sxs-lookup"><span data-stu-id="839a9-183">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="839a9-184">Portanto, se você deseja toorerun Olá fatia ou Olá tutorial novamente, pasta de carregamento Olá arquivo de entrada (input.log) toohello inputdata do contêiner de adfgetstarted hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-184">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
> 
> 

## <a name="data-factory-entities-in-hello-template"></a><span data-ttu-id="839a9-185">Entidades da fábrica de dados no modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="839a9-185">Data Factory entities in hello template</span></span>
### <a name="define-data-factory"></a><span data-ttu-id="839a9-186">Definir Data Factory</span><span class="sxs-lookup"><span data-stu-id="839a9-186">Define data factory</span></span>
<span data-ttu-id="839a9-187">Você pode definir uma fábrica de dados no modelo do Gerenciador de recursos de saudação conforme Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="839a9-187">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
<span data-ttu-id="839a9-188">Olá dataFactoryName é definido como:</span><span class="sxs-lookup"><span data-stu-id="839a9-188">hello dataFactoryName is defined as:</span></span> 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
<span data-ttu-id="839a9-189">É uma cadeia de caracteres exclusiva com base no ID do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="839a9-189">It is a unique string based on hello resource group ID.</span></span>  

### <a name="defining-data-factory-entities"></a><span data-ttu-id="839a9-190">Definir entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="839a9-190">Defining Data Factory entities</span></span>
<span data-ttu-id="839a9-191">Hello seguintes entidades da fábrica de dados estão definidas no modelo JSON hello:</span><span class="sxs-lookup"><span data-stu-id="839a9-191">hello following Data Factory entities are defined in hello JSON template:</span></span> 

* [<span data-ttu-id="839a9-192">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-192">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="839a9-193">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="839a9-193">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="839a9-194">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-194">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="839a9-195">Conjunto de dados de saída do blob do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-195">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="839a9-196">Pipeline com a Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="839a9-196">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="839a9-197">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-197">Azure Storage linked service</span></span>
<span data-ttu-id="839a9-198">Especifique o nome hello e a chave da sua conta de armazenamento do Azure nesta seção.</span><span class="sxs-lookup"><span data-stu-id="839a9-198">You specify hello name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="839a9-199">Consulte [serviço vinculado do armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre o JSON propriedades usadas toodefine um armazenamento do Azure serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="839a9-199">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used toodefine an Azure Storage linked service.</span></span> 

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
<span data-ttu-id="839a9-200">Olá **connectionString** usa Olá parâmetros storageAccountName e storageAccountKey.</span><span class="sxs-lookup"><span data-stu-id="839a9-200">hello **connectionString** uses hello storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="839a9-201">valores de saudação para esses parâmetros passados usando um arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="839a9-201">hello values for these parameters passed by using a configuration file.</span></span> <span data-ttu-id="839a9-202">definição de saudação também usa variáveis: azureStroageLinkedService e dataFactoryName definido no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="839a9-202">hello definition also uses variables: azureStroageLinkedService and dataFactoryName defined in hello template.</span></span> 

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="839a9-203">Serviço vinculado do HDInsight sob demanda</span><span class="sxs-lookup"><span data-stu-id="839a9-203">HDInsight on-demand linked service</span></span>
<span data-ttu-id="839a9-204">Consulte [serviços vinculados de computação](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artigo para obter detalhes sobre o JSON propriedades usadas toodefine um serviço vinculado do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="839a9-204">See [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used toodefine an HDInsight on-demand linked service.</span></span>  

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
<span data-ttu-id="839a9-205">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="839a9-205">Note hello following points:</span></span> 

* <span data-ttu-id="839a9-206">Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você com hello acima JSON.</span><span class="sxs-lookup"><span data-stu-id="839a9-206">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello above JSON.</span></span> <span data-ttu-id="839a9-207">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="839a9-207">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span> 
* <span data-ttu-id="839a9-208">Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="839a9-208">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="839a9-209">Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="839a9-209">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="839a9-210">Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="839a9-210">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="839a9-211">HDInsight não exclui esse contêiner quando Olá cluster é excluído.</span><span class="sxs-lookup"><span data-stu-id="839a9-211">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="839a9-212">Este comportamento ocorre por design.</span><span class="sxs-lookup"><span data-stu-id="839a9-212">This behavior is by design.</span></span> <span data-ttu-id="839a9-213">Com o serviço de vinculado do HDInsight sob demanda, um cluster HDInsight é criado sempre que precisa de uma fatia toobe processado a menos que haja um cluster existente de ao vivo (**timeToLive**) e é excluído quando Olá processamento é concluído.</span><span class="sxs-lookup"><span data-stu-id="839a9-213">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs toobe processed unless there is an existing live cluster (**timeToLive**) and is deleted when hello processing is done.</span></span>
  
    <span data-ttu-id="839a9-214">Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="839a9-214">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="839a9-215">Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-215">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="839a9-216">nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="839a9-216">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="839a9-217">Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.</span><span class="sxs-lookup"><span data-stu-id="839a9-217">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

<span data-ttu-id="839a9-218">Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="839a9-218">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="839a9-219">Conjunto de dados de entrada de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-219">Azure blob input dataset</span></span>
<span data-ttu-id="839a9-220">Você especificar nomes de saudação do contêiner de blob, a pasta e o arquivo que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-220">You specify hello names of blob container, folder, and file that contains hello input data.</span></span> <span data-ttu-id="839a9-221">Consulte [propriedades de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="839a9-221">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span> 

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
<span data-ttu-id="839a9-222">Esta definição usa Olá parâmetros definidos no modelo de parâmetro a seguir: blobContainer, inputBlobFolder e inputBlobName.</span><span class="sxs-lookup"><span data-stu-id="839a9-222">This definition uses hello following parameters defined in parameter template: blobContainer, inputBlobFolder, and inputBlobName.</span></span> 

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="839a9-223">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="839a9-223">Azure Blob output dataset</span></span>
<span data-ttu-id="839a9-224">Você especificar nomes de saudação do contêiner de blob e a pasta que contém os dados de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-224">You specify hello names of blob container and folder that holds hello output data.</span></span> <span data-ttu-id="839a9-225">Consulte [propriedades de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="839a9-225">See [Azure Blob dataset properties](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used toodefine an Azure Blob dataset.</span></span>  

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

<span data-ttu-id="839a9-226">Esta definição usa Olá parâmetros definidos no modelo de parâmetro hello a seguir: blobContainer e outputBlobFolder.</span><span class="sxs-lookup"><span data-stu-id="839a9-226">This definition uses hello following parameters defined in hello parameter template: blobContainer and outputBlobFolder.</span></span> 

#### <a name="data-pipeline"></a><span data-ttu-id="839a9-227">Pipeline de dados</span><span class="sxs-lookup"><span data-stu-id="839a9-227">Data pipeline</span></span>
<span data-ttu-id="839a9-228">Você define um pipeline que transforma dados executando o script Hive em um cluster do Azure HDInsight sob demanda.</span><span class="sxs-lookup"><span data-stu-id="839a9-228">You define a pipeline that transform data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="839a9-229">Consulte [JSON de Pipeline](data-factory-create-pipelines.md#pipeline-json) para obter descrições dos elementos usados de JSON toodefine um pipeline neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="839a9-229">See [Pipeline JSON](data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used toodefine a pipeline in this example.</span></span> 

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

## <a name="reuse-hello-template"></a><span data-ttu-id="839a9-230">Reutilizar Olá modelo</span><span class="sxs-lookup"><span data-stu-id="839a9-230">Reuse hello template</span></span>
<span data-ttu-id="839a9-231">No tutorial de saudação, você criou um modelo de definição de entidades da fábrica de dados e um modelo para passar valores para parâmetros.</span><span class="sxs-lookup"><span data-stu-id="839a9-231">In hello tutorial, you created a template for defining Data Factory entities and a template for passing values for parameters.</span></span> <span data-ttu-id="839a9-232">toouse Olá ambientes de toodifferent do mesmo modelo toodeploy Data Factory entidades, crie um arquivo de parâmetro para cada ambiente e usá-lo ao implantar o ambiente toothat.</span><span class="sxs-lookup"><span data-stu-id="839a9-232">toouse hello same template toodeploy Data Factory entities toodifferent environments, you create a parameter file for each environment and use it when deploying toothat environment.</span></span>     

<span data-ttu-id="839a9-233">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="839a9-233">Example:</span></span>  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
<span data-ttu-id="839a9-234">Observe que Olá primeiro comando usa o arquivo de parâmetro para o ambiente de desenvolvimento hello, segundo uma para Olá ambiente de teste e Olá um terceiro para o ambiente de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="839a9-234">Notice that hello first command uses parameter file for hello development environment, second one for hello test environment, and hello third one for hello production environment.</span></span>  

<span data-ttu-id="839a9-235">Também é possível reutilizar Olá modelo tooperform repetido tarefas.</span><span class="sxs-lookup"><span data-stu-id="839a9-235">You can also reuse hello template tooperform repeated tasks.</span></span> <span data-ttu-id="839a9-236">Por exemplo, você precisa toocreate muitos fábricas de dados com um ou mais pipelines que implementam Olá mesma lógica, mas cada fábrica usa diferentes do Azure armazenamento de dados e contas do Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="839a9-236">For example, you need toocreate many data factories with one or more pipelines that implement hello same logic but each data factory uses different Azure storage and Azure SQL Database accounts.</span></span> <span data-ttu-id="839a9-237">Nesse cenário, você usa Olá mesmo modelo em Olá mesmo ambiente (desenvolvimento, teste ou produção) com parâmetros diferentes arquivos toocreate fábricas de dados.</span><span class="sxs-lookup"><span data-stu-id="839a9-237">In this scenario, you use hello same template in hello same environment (dev, test, or production) with different parameter files toocreate data factories.</span></span> 

## <a name="resource-manager-template-for-creating-a-gateway"></a><span data-ttu-id="839a9-238">Modelo do Resource Manager para criar um gateway</span><span class="sxs-lookup"><span data-stu-id="839a9-238">Resource Manager template for creating a gateway</span></span>
<span data-ttu-id="839a9-239">Aqui está uma amostra de modelo de Gerenciador de recursos para criar um gateway lógico no hello novamente.</span><span class="sxs-lookup"><span data-stu-id="839a9-239">Here is a sample Resource Manager template for creating a logical gateway in hello back.</span></span> <span data-ttu-id="839a9-240">Instalar um gateway em seu computador local ou a VM de IaaS do Azure e registrar o gateway de saudação com serviço de fábrica de dados usando uma chave.</span><span class="sxs-lookup"><span data-stu-id="839a9-240">Install a gateway on your on-premises computer or Azure IaaS VM and register hello gateway with Data Factory service using a key.</span></span> <span data-ttu-id="839a9-241">Confira [Mover dados entre o local e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="839a9-241">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) for details.</span></span>

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
<span data-ttu-id="839a9-242">O modelo cria uma data factory chamada GatewayUsingArmDF com um gateway chamado: GatewayUsingARM.</span><span class="sxs-lookup"><span data-stu-id="839a9-242">This template creates a data factory named GatewayUsingArmDF with a gateway named: GatewayUsingARM.</span></span> 

## <a name="see-also"></a><span data-ttu-id="839a9-243">Consulte também</span><span class="sxs-lookup"><span data-stu-id="839a9-243">See Also</span></span>
| <span data-ttu-id="839a9-244">Tópico</span><span class="sxs-lookup"><span data-stu-id="839a9-244">Topic</span></span> | <span data-ttu-id="839a9-245">Descrição</span><span class="sxs-lookup"><span data-stu-id="839a9-245">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="839a9-246">Pipelines</span><span class="sxs-lookup"><span data-stu-id="839a9-246">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="839a9-247">Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e como toouse-los tooconstruct ponta a ponta controladas por dados fluxos de trabalho para seu cenário ou business.</span><span class="sxs-lookup"><span data-stu-id="839a9-247">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="839a9-248">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="839a9-248">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="839a9-249">Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="839a9-249">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="839a9-250">Agendamento e execução</span><span class="sxs-lookup"><span data-stu-id="839a9-250">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="839a9-251">Este artigo explica os aspectos de programação e a execução de saudação do modelo de aplicativo do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="839a9-251">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="839a9-252">Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento</span><span class="sxs-lookup"><span data-stu-id="839a9-252">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="839a9-253">Este artigo descreve como toomonitor, gerenciar e depurar pipelines usando Olá monitoramento e gerenciamento de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="839a9-253">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |

