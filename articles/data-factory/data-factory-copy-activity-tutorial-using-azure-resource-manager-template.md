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
# <a name="tutorial-use-azure-resource-manager-template-toocreate-a-data-factory-pipeline-toocopy-data"></a>Tutorial: Uso do Azure Resource Manager modelo toocreate uma fábrica de dados pipeline toocopy de dados 
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md)
> * [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API do .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

Este tutorial mostra como toouse uma toocreate de modelo do Gerenciador de recursos do Azure uma fábrica de dados do Azure. pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa. Ela não transforma dados de saída de tooproduce de dados de entrada. Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).

Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia. Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte. Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats). atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável. Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).

Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa. Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="prerequisites"></a>Pré-requisitos
* Passar [Tutorial visão geral e pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) e hello completa **pré-requisito** etapas.
* Siga as instruções em [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo tooinstall versão mais recente do PowerShell do Azure no seu computador. Neste tutorial, você deve usar entidades do PowerShell toodeploy fábrica de dados. 
* (opcional) Consulte [criação de modelos de Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md) toolearn sobre modelos do Gerenciador de recursos do Azure.

## <a name="in-this-tutorial"></a>Neste tutorial
Neste tutorial, você pode criar uma fábrica de dados com hello entidades da fábrica de dados a seguir:

| Entidade | Descrição |
| --- | --- |
| Serviço vinculado de armazenamento do Azure |Vincula sua fábrica de dados de toohello de conta de armazenamento do Azure. Armazenamento do Azure é um repositório de dados de origem hello e banco de dados do SQL Azure é Olá coletor repositório de dados para a atividade de cópia Olá Olá tutorial. Especifica a conta de armazenamento de saudação que contém dados de entrada hello para atividade de cópia de saudação. |
| Serviço vinculado para o Banco de Dados SQL do Azure |Vincula sua fábrica de dados de toohello de banco de dados do SQL Azure. Ele especifica o banco de dados de SQL do Azure de saudação que armazena dados de saída de hello de atividade de cópia de saudação. |
| Conjunto de dados de entrada de Blob do Azure |Refere-se o serviço de armazenamento do Azure vinculada toohello. Olá serviço vinculado refere-se tooan conta de armazenamento do Azure e conjunto de dados de Blob do Azure Olá Especifica contêiner Olá, nome de arquivo e pasta no armazenamento de saudação que contém os dados de entrada hello. |
| Conjunto de dados de saída do SQL Azure |Refere-se o serviço vinculado do SQL Azure de toohello. Olá vinculado do SQL Azure serviço refere-se tooan Azure SQL server e conjunto de dados de SQL do Azure Olá Especifica o nome de Olá da tabela de saudação que contém dados de saída de saudação. |
| Pipeline de dados |pipeline de saudação tem uma atividade de cópia que usa Olá o conjunto de dados de blob do Azure como uma entrada de tipo e Olá conjunto de dados do SQL Azure como uma saída. Olá Copiar atividade copia dados de uma tabela de tooa de BLOBs do Azure no banco de dados do SQL Azure hello. |

Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline em um data factory pode ter uma ou mais atividades. Há dois tipos de atividades: [atividades de movimentação de dados](data-factory-data-movement-activities.md) e [atividades de transformação de dados](data-factory-data-transformation-activities.md). Neste tutorial, você criará um pipeline com uma atividade (atividade de cópia).

![Copiar Blob do Azure tooAzure banco de dados SQL](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/CopyBlob2SqlDiagram.png) 

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
Crie um arquivo JSON chamado **ADFCopyTutorialARM.json** na **C:\ADFGetStarted** pasta com hello conteúdo a seguir:

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

## <a name="parameters-json"></a>Parâmetros JSON
Crie um arquivo JSON chamado **ADFCopyTutorialARM Parameters.json** que contém parâmetros de modelo do Azure Resource Manager hello. 

> [!IMPORTANT]
> Especifique o nome e a chave de sua conta do Armazenamento do Azure nos parâmetros storageAccountName e storageAccountKey.  
> 
> Especifique o servidor Azure SQL, o banco de dados, o usuário e a senha para os parâmetros sqlServerName, databaseName, sqlServerUserName e sqlServerPassword.  

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
   * Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir.
    
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```    
2. Olá execução seguintes entidades de fábrica de dados toodeploy de comando usando o modelo do Gerenciador de recursos de saudação que você criou na etapa 1.

    ```PowerShell   
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile C:\ADFGetStarted\ADFCopyTutorialARM.json -TemplateParameterFile C:\ADFGetStarted\ADFCopyTutorialARM-Parameters.json
    ```

## <a name="monitor-pipeline"></a>Monitorar o pipeline

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) usando sua conta do Azure.
2. Clique em **fábricas de dados** no hello esquerdo menu (ou) clique **mais serviços** e clique em **fábricas de dados** em **INTELLIGENCE + análise** categoria.
   
    ![Menu Data factories](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factories-menu.png)
3. Em Olá **fábricas de dados** página, pesquisar e localizar sua fábrica de dados (AzureBlobToAzureSQLDatabaseDF). 
   
    ![Pesquisar por data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/search-for-data-factory.png)  
4. Clique no seu Azure Data Factory. Página de home Olá Olá fábrica de dados é exibida.
   
    ![Home page do data factory](media/data-factory-copy-activity-tutorial-using-azure-resource-manager-template/data-factory-home-page.png)  
6. Siga as instruções de [monitorar conjuntos de dados e pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) pipeline de saudação toomonitor e conjuntos de dados, você criou neste tutorial. Atualmente, o Visual Studio não dá suporte a monitoramento de pipelines do Data Factory.
7. Quando uma fatia está em Olá **pronto** de estado, verifique se os dados de saudação copiado toohello **emp** tabela no banco de dados do SQL Azure hello.


Para obter mais informações sobre como toouse pipeline de toomonitor de folhas de portal do Azure e conjuntos de dados você tiver criado neste tutorial, consulte [monitorar conjuntos de dados e pipeline](data-factory-monitor-manage-pipelines.md) .

Para obter mais informações sobre como toouse Olá monitorar e gerenciar aplicativos toomonitor seus dados pipelines, consulte [monitorar e gerenciar os pipelines de fábrica de dados do Azure usando o monitoramento de aplicativo](data-factory-monitor-manage-app.md).

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
"dataFactoryName": "[concat('AzureBlobToAzureSQLDatabaseDF', uniqueString(resourceGroup().id))]"
```

É uma cadeia de caracteres exclusiva com base no ID do grupo de recursos de saudação.  

### <a name="defining-data-factory-entities"></a>Definir entidades de Data Factory
Hello seguintes entidades da fábrica de dados estão definidas no modelo JSON hello: 

1. [Serviço vinculado de armazenamento do Azure](#azure-storage-linked-service)
2. [Serviço vinculado do SQL do Azure](#azure-sql-database-linked-service)
3. [Conjunto de dados de blob do Azure](#azure-blob-dataset)
4. [Conjunto de dados do SQL do Azure](#azure-sql-dataset)
5. [Pipeline de dados com a atividade de cópia](#data-pipeline)

#### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure
Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure. Você criou um contêiner e carregados conta de armazenamento toothis dados como parte de [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Especifique o nome hello e a chave da sua conta de armazenamento do Azure nesta seção. Consulte [serviço vinculado do armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre o JSON propriedades usadas toodefine um armazenamento do Azure serviço vinculado. 

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

Olá connectionString usa parâmetros storageAccountName e storageAccountKey de saudação. valores de saudação para esses parâmetros passados usando um arquivo de configuração. definição de saudação também usa variáveis: azureStroageLinkedService e dataFactoryName definido no modelo de saudação. 

#### <a name="azure-sql-database-linked-service"></a>Serviço vinculado para o Banco de Dados SQL do Azure
AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure. Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados. Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). Especifique o nome do servidor SQL Azure Olá, nome do banco de dados, nome de usuário e senha de usuário nesta seção. Consulte [serviço vinculado do SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um SQL Azure serviço vinculado.  

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

Olá connectionString usa sqlServerName, databaseName, sqlServerUserName e sqlServerPassword parâmetros cujos valores são passados usando um arquivo de configuração. Olá definição também usa Olá seguir variáveis de modelo Olá: azureSqlLinkedServiceName, dataFactoryName.

#### <a name="azure-blob-dataset"></a>Conjunto de dados de blob do Azure
serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure. Na definição de conjunto de dados de blob do Azure, você deve especificar nomes de contêiner de blob, a pasta e arquivo que contém os dados de entrada hello. Consulte [propriedades de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados de Blob do Azure. 

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

#### <a name="azure-sql-dataset"></a>Conjunto de dados do SQL do Azure
Especifique o nome de saudação da tabela Olá no banco de dados de SQL do Azure de saudação que contém dados Olá copiado da saudação armazenamento de BLOBs do Azure. Consulte [propriedades de conjunto de dados do SQL Azure](data-factory-azure-sql-connector.md#dataset-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um conjunto de dados do SQL Azure. 

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

#### <a name="data-pipeline"></a>Pipeline de dados
Você define um pipeline que copia dados de conjunto de dados do hello BLOBs do Azure dataset toohello SQL Azure. Consulte [JSON de Pipeline](data-factory-create-pipelines.md#pipeline-json) para obter descrições dos elementos usados de JSON toodefine um pipeline neste exemplo. 

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

## <a name="reuse-hello-template"></a>Reutilizar Olá modelo
No tutorial de saudação, você criou um modelo de definição de entidades da fábrica de dados e um modelo para passar valores para parâmetros. pipeline de saudação copia dados de um armazenamento do Azure conta tooan SQL Azure banco de dados especificado por meio de parâmetros. toouse Olá ambientes de toodifferent do mesmo modelo toodeploy Data Factory entidades, crie um arquivo de parâmetro para cada ambiente e usá-lo ao implantar o ambiente toothat.     

Exemplo:  

```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Dev.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Test.json
```
```PowerShell
New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFCopyTutorialARM.json -TemplateParameterFile ADFCopyTutorialARM-Parameters-Production.json
```

Observe que Olá primeiro comando usa o arquivo de parâmetro para o ambiente de desenvolvimento hello, segundo uma para Olá ambiente de teste e Olá um terceiro para o ambiente de produção de hello.  

Também é possível reutilizar Olá modelo tooperform repetido tarefas. Por exemplo, você precisa toocreate muitos fábricas de dados com um ou mais pipelines que implementam Olá mesmo lógica, mas cada fábrica de dados usa diferentes contas de armazenamento e o banco de dados SQL. Nesse cenário, você usa Olá mesmo modelo em Olá mesmo ambiente (desenvolvimento, teste ou produção) com parâmetros diferentes arquivos toocreate fábricas de dados.   

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia. Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação.
