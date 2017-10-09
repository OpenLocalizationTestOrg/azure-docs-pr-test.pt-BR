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
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-resource-manager-template"></a>Tutorial: Criar a sua primeira Azure Data Factory usando o modelo do Azure Resource Manager
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-build-your-first-pipeline.md)
> * [Portal do Azure](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Modelo do Resource Manager](data-factory-build-your-first-pipeline-using-arm.md)
> * [API REST](data-factory-build-your-first-pipeline-using-rest-api.md)
> 
> 

Neste artigo, você usar um toocreate de modelo do Gerenciador de recursos do Azure a primeira data factory do Azure. tutorial de saudação toodo usando outras ferramentas/SDKs, selecione uma das opções de saudação da lista suspensa de saudação.

pipeline de saudação neste tutorial tem uma atividade: **atividade Hive do HDInsight**. Essa atividade executa um script do hive em um cluster de HDInsight do Azure que transforma dados de saída de tooproduce de entrada. pipeline de saudação é agendado toorun depois de um mês entre hello especificar horários de início e término. 

> [!NOTE]
> pipeline de dados Olá neste tutorial transforma dados de saída de tooproduce de dados de entrada. Para obter um tutorial sobre como toocopy dados usando a fábrica de dados do Azure, consulte [Tutorial: copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> pipeline de saudação neste tutorial tem apenas uma atividade do tipo: HDInsightHive. Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Agendamento e execução no Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

## <a name="prerequisites"></a>Pré-requisitos
* Leia [visão geral do Tutorial](data-factory-build-your-first-pipeline.md) artigo e hello completa **pré-requisito** etapas.
* Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall versão mais recente do PowerShell do Azure no seu computador.
* Consulte [criação de modelos de Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sobre modelos do Gerenciador de recursos do Azure. 

## <a name="in-this-tutorial"></a>Neste tutorial
| Entidade | Descrição |
| --- | --- |
| Serviço vinculado de armazenamento do Azure |Vincula sua fábrica de dados de toohello de conta de armazenamento do Azure. Olá conta de armazenamento do Azure mantém Olá dados de entrada e saídos para o pipeline de saudação neste exemplo. |
| Serviço vinculado do HDInsight sob demanda |Vincula uma fábrica de dados sob demanda HDInsight cluster toohello. cluster de saudação é criado automaticamente para você tooprocess dados e é excluída após a conclusão do processamento de saudação. |
| Conjunto de dados de entrada de Blob do Azure |Refere-se o serviço de armazenamento do Azure vinculada toohello. Olá serviço vinculado refere-se tooan conta de armazenamento do Azure e conjunto de dados de Blob do Azure Olá Especifica contêiner Olá, nome de arquivo e pasta no armazenamento de saudação que contém os dados de entrada hello. |
| Conjunto de dados de saída de Blob do Azure |Refere-se o serviço de armazenamento do Azure vinculada toohello. Olá serviço vinculado refere-se tooan conta de armazenamento do Azure e conjunto de dados de Blob do Azure Olá Especifica contêiner Olá, nome de arquivo e pasta no armazenamento de saudação que contém dados de saída de saudação. |
| Pipeline de dados |pipeline de saudação tem uma atividade do tipo HDInsightHive, que consome Olá conjunto de dados de entrada e produz o conjunto de dados de saída de hello. |

Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline em um data factory pode ter uma ou mais atividades. Há dois tipos de atividades: [atividades de movimentação de dados](data-factory-data-movement-activities.md) e [atividades de transformação de dados](data-factory-data-transformation-activities.md). Neste tutorial, você criará um pipeline com uma atividade (atividade do Hive).

Olá seção a seguir fornece Olá completa Gerenciador de recursos modelo para definir entidades da fábrica de dados para que você possa executar rapidamente por meio do modelo de saudação tutorial e teste hello. toounderstand como cada entidade de fábrica de dados é definida, consulte [entidades da fábrica de dados no modelo de saudação](#data-factory-entities-in-the-template) seção.

## <a name="data-factory-json-template"></a>Modelo de JSON do Data Factory
Olá modelo de nível superior Gerenciador de recursos para definir uma fábrica de dados é: 

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
Crie um arquivo JSON chamado **ADFTutorialARM.json** na **C:\ADFGetStarted** pasta com hello conteúdo a seguir:

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
> Você pode encontrar outro exemplo de modelo do Gerenciador de Recursos para criar um Azure data factory em [Tutorial: criar um pipeline com atividade de cópia usando um modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md).  
> 
> 

## <a name="parameters-json"></a>Parâmetros JSON
Crie um arquivo JSON chamado **ADFTutorialARM Parameters.json** que contém parâmetros de modelo do Azure Resource Manager hello.  

> [!IMPORTANT]
> Especificar nome de saudação e a chave da sua conta de armazenamento do Azure para Olá **storageAccountName** e **storageAccountKey** parâmetros nesse arquivo de parâmetro. 
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
> Você pode ter arquivos JSON de parâmetros separados para desenvolvimento, teste e ambientes de produção que você pode usar com hello mesmo modelo JSON da fábrica de dados. Usando um script do PowerShell, você pode automatizar a implantação de entidades de Data Factory nesses ambientes. 
> 
> 

## <a name="create-data-factory"></a>Criar um data factory
1. Iniciar **Azure PowerShell** e execução Olá comando a seguir: 
   * Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure.
    ```PowerShell
    Login-AzureRmAccount
    ```  
   * Execute Olá tooview de comando a seguir todas as assinaturas de saudação para esta conta.
    ```PowerShell
    Get-AzureRmSubscription
    ``` 
   * Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir. Essa assinatura deve ser Olá mesmas Olá aquele que você usou no portal do Azure de saudação.
    ```
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```   
2. Olá execução seguintes entidades de fábrica de dados toodeploy de comando usando o modelo do Gerenciador de recursos de saudação que você criou na etapa 1. 

    ```PowerShell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Monitorar o pipeline
1. Depois de fazer logon em toohello [portal do Azure](https://portal.azure.com/), clique em **procurar** e selecione **fábricas de dados**.
     ![Procurar->Data factories](./media/data-factory-build-your-first-pipeline-using-arm/BrowseDataFactories.png)
2. Em hello **fábricas de dados** folha, clique em fábrica de dados hello (**TutorialFactoryARM**) criado por você.    
3. Em Olá **Data Factory** folha sua fábrica de dados, clique em **diagrama**.

     ![Bloco Diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramTile.png)
4. Em Olá **exibição de diagrama**, consulte uma visão geral dos pipelines hello e conjuntos de dados usados neste tutorial.
   
   ![Exibição de diagrama](./media/data-factory-build-your-first-pipeline-using-arm/DiagramView.png) 
5. Na exibição de diagrama de Olá, clique duas vezes em dataset Olá **AzureBlobOutput**. Você verá essa fatia Olá que está sendo processada atualmente.
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/AzureBlobOutput.png)
6. Quando o processamento é concluído, você verá fatia Olá **pronto** estado. A criação de um cluster do HDInsight sob demanda geralmente leva algum tempo (20 minutos, aproximadamente). Portanto, espere Olá pipeline tootake **aproximadamente 30 minutos** tooprocess Olá fatia.
   
    ![Conjunto de dados](./media/data-factory-build-your-first-pipeline-using-arm/SliceReady.png)    
7. Quando a fatia hello está em **pronto** de estado, verifique Olá **partitioneddata** pasta Olá **adfgetstarted** contêiner no seu armazenamento de blob para Olá dados de saída.  

Consulte [monitorar conjuntos de dados e pipeline](data-factory-monitor-manage-pipelines.md) para obter instruções sobre como o pipeline de saudação do toouse Olá folhas portal do Azure toomonitor e conjuntos de dados você tiver criado neste tutorial.

Você também pode usar o Monitor e gerenciar aplicativos toomonitor seus pipelines de dados. Consulte [monitorar e gerenciar os pipelines de fábrica de dados do Azure usando o monitoramento de aplicativo](data-factory-monitor-manage-app.md) para obter detalhes sobre como usar o aplicativo hello. 

> [!IMPORTANT]
> arquivo de entrada Hello é excluído quando a fatia de saudação é processada com êxito. Portanto, se você deseja toorerun Olá fatia ou Olá tutorial novamente, pasta de carregamento Olá arquivo de entrada (input.log) toohello inputdata do contêiner de adfgetstarted hello.
> 
> 

## <a name="data-factory-entities-in-hello-template"></a>Entidades da fábrica de dados no modelo de saudação
### <a name="define-data-factory"></a>Definir Data Factory
Você pode definir uma fábrica de dados no modelo do Gerenciador de recursos de saudação conforme Olá exemplo a seguir:  

```json
"resources": [
{
    "name": "[variables('dataFactoryName')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "West US"
}
```
Olá dataFactoryName é definido como: 

```json
"dataFactoryName": "[concat('HiveTransformDF', uniqueString(resourceGroup().id))]",
```
É uma cadeia de caracteres exclusiva com base no ID do grupo de recursos de saudação.  

### <a name="defining-data-factory-entities"></a>Definir entidades de Data Factory
Hello seguintes entidades da fábrica de dados estão definidas no modelo JSON hello: 

* [Serviço vinculado de armazenamento do Azure](#azure-storage-linked-service)
* [Serviço vinculado do HDInsight sob demanda](#hdinsight-on-demand-linked-service)
* [Conjunto de dados de entrada de Blob do Azure](#azure-blob-input-dataset)
* [Conjunto de dados de saída do blob do Azure](#azure-blob-output-dataset)
* [Pipeline com a Atividade de cópia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure
Especifique o nome hello e a chave da sua conta de armazenamento do Azure nesta seção. Consulte [serviço vinculado do armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre o JSON propriedades usadas toodefine um armazenamento do Azure serviço vinculado. 

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
Olá **connectionString** usa Olá parâmetros storageAccountName e storageAccountKey. valores de saudação para esses parâmetros passados usando um arquivo de configuração. definição de saudação também usa variáveis: azureStroageLinkedService e dataFactoryName definido no modelo de saudação. 

#### <a name="hdinsight-on-demand-linked-service"></a>Serviço vinculado do HDInsight sob demanda
Consulte [serviços vinculados de computação](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) artigo para obter detalhes sobre o JSON propriedades usadas toodefine um serviço vinculado do HDInsight sob demanda.  

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
Observe Olá pontos a seguir: 

* Olá fábrica de dados cria um **baseados em Linux** cluster HDInsight para você com hello acima JSON. Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes. 
* Você pode usar **seu próprio cluster do HDInsight** em vez de usar um cluster do HDInsight sob demanda. Confira [Serviço vinculado do HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) para obter detalhes.
* Olá HDInsight cluster cria um **contêiner padrão** no armazenamento de blob Olá especificado no hello JSON (**linkedServiceName**). HDInsight não exclui esse contêiner quando Olá cluster é excluído. Este comportamento ocorre por design. Com o serviço de vinculado do HDInsight sob demanda, um cluster HDInsight é criado sempre que precisa de uma fatia toobe processado a menos que haja um cluster existente de ao vivo (**timeToLive**) e é excluído quando Olá processamento é concluído.
  
    Quanto mais fatias forem processadas, você verá muitos contêineres no armazenamento de blobs do Azure. Se não precisar para solução de problemas de trabalhos de saudação, talvez você queira toodelete-os custos de armazenamento do tooreduce hello. nomes de saudação desses contêineres seguem um padrão: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp". Use ferramentas como [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com/) armazenamento de blobs de contêineres toodelete do Azure.

Confira [Serviço vinculado do HDInsight sob demanda](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes.

#### <a name="azure-blob-input-dataset"></a>Conjunto de dados de entrada de Blob do Azure
Você especificar nomes de saudação do contêiner de blob, a pasta e o arquivo que contém os dados de entrada hello. Consulte [propriedades de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure. 

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
Esta definição usa Olá parâmetros definidos no modelo de parâmetro a seguir: blobContainer, inputBlobFolder e inputBlobName. 

#### <a name="azure-blob-output-dataset"></a>Conjunto de dados de saída de Blob do Azure
Você especificar nomes de saudação do contêiner de blob e a pasta que contém os dados de saída de hello. Consulte [propriedades de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure.  

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

Esta definição usa Olá parâmetros definidos no modelo de parâmetro hello a seguir: blobContainer e outputBlobFolder. 

#### <a name="data-pipeline"></a>Pipeline de dados
Você define um pipeline que transforma dados executando o script Hive em um cluster do Azure HDInsight sob demanda. Consulte [JSON de Pipeline](data-factory-create-pipelines.md#pipeline-json) para obter descrições dos elementos usados de JSON toodefine um pipeline neste exemplo. 

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

## <a name="reuse-hello-template"></a>Reutilizar Olá modelo
No tutorial de saudação, você criou um modelo de definição de entidades da fábrica de dados e um modelo para passar valores para parâmetros. toouse Olá ambientes de toodifferent do mesmo modelo toodeploy Data Factory entidades, crie um arquivo de parâmetro para cada ambiente e usá-lo ao implantar o ambiente toothat.     

Exemplo:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Dev.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Test.json

New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json -TemplateParameterFile ADFTutorialARM-Parameters-Production.json
```
Observe que Olá primeiro comando usa o arquivo de parâmetro para o ambiente de desenvolvimento hello, segundo uma para Olá ambiente de teste e Olá um terceiro para o ambiente de produção de hello.  

Também é possível reutilizar Olá modelo tooperform repetido tarefas. Por exemplo, você precisa toocreate muitos fábricas de dados com um ou mais pipelines que implementam Olá mesma lógica, mas cada fábrica usa diferentes do Azure armazenamento de dados e contas do Azure SQL Database. Nesse cenário, você usa Olá mesmo modelo em Olá mesmo ambiente (desenvolvimento, teste ou produção) com parâmetros diferentes arquivos toocreate fábricas de dados. 

## <a name="resource-manager-template-for-creating-a-gateway"></a>Modelo do Resource Manager para criar um gateway
Aqui está uma amostra de modelo de Gerenciador de recursos para criar um gateway lógico no hello novamente. Instalar um gateway em seu computador local ou a VM de IaaS do Azure e registrar o gateway de saudação com serviço de fábrica de dados usando uma chave. Confira [Mover dados entre o local e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes.

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
O modelo cria uma data factory chamada GatewayUsingArmDF com um gateway chamado: GatewayUsingARM. 

## <a name="see-also"></a>Consulte também
| Tópico | Descrição |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |Este artigo ajuda você a entender os pipelines e atividades do Azure Data Factory e como toouse-los tooconstruct ponta a ponta controladas por dados fluxos de trabalho para seu cenário ou business. |
| [Conjunto de dados](data-factory-create-datasets.md) |Este artigo o ajuda a entender os conjuntos de dados no Azure Data Factory. |
| [Agendamento e execução](data-factory-scheduling-and-execution.md) |Este artigo explica os aspectos de programação e a execução de saudação do modelo de aplicativo do Azure Data Factory. |
| [Monitorar e gerenciar pipelines usando o Aplicativo de Monitoramento](data-factory-monitor-manage-app.md) |Este artigo descreve como toomonitor, gerenciar e depurar pipelines usando Olá monitoramento e gerenciamento de aplicativo. |

