---
title: "modelos de aprendizado de máquina aaaUpdate usando o Azure Data Factory | Microsoft Docs"
description: "Descreve como toocreate criar pipelines de previsão usando o Azure Data Factory e aprendizado de máquina do Azure"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 6e5e4d2cfd245c7a9ed3bb9cdacca1f7f82b9620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a>Atualizando os modelos do Machine Learning do Azure usando a Atividade de Recurso de Atualização

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Atividade de Hive](data-factory-hive-activity.md) 
> * [Atividade Pig](data-factory-pig-activity.md)
> * [Atividade MapReduce](data-factory-map-reduce.md)
> * [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Atividade do Spark](data-factory-spark.md)
> * [Atividade de Execução em Lote do Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Atividade do Recurso de Atualização do Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md)
> * [Atividade do U-SQL do Data Lake Analytics](data-factory-usql-activity.md)
> * [Atividade Personalizada do .NET](data-factory-use-custom-activities.md)

Este artigo complementa Olá principal do Azure Data Factory - artigo de integração de aprendizado de máquina do Azure: [criar pipelines de previsão usando o aprendizado de máquina do Azure e o Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md). Se você ainda não fez isso, consulte o artigo principal de saudação antes de ler este artigo. 

## <a name="overview"></a>Visão geral
Ao longo do tempo, os modelos de previsão de saudação em experiências de pontuação do hello Azure ML necessário toobe treinados novamente usando novos conjuntos de dados de entrada. Depois que você treinamento, você deseja tooupdate Olá pontuação serviço web com hello retreinados modelo ML. Olá etapas típicas tooenable treinar novamente e atualizações modelos de ML do Azure por meio de serviços web são:

1. Crie um teste no [Estúdio AM do Azure](https://studio.azureml.net).
2. Quando estiver satisfeito com o modelo de hello, usar o Azure ML Studio toopublish web services para ambos os Olá **experiência de treinamento** e pontuação /**experimento previsão**.

Olá tabela a seguir descreve Olá web services usado neste exemplo.  Confira [Readaptar os modelos do Machine Learning de forma programática](../machine-learning/machine-learning-retrain-models-programmatically.md) para obter detalhes.

- **Treinamento do serviço Web** - recebe dados de treinamento e produz modelos treinados. saída Olá Olá treinamento é um arquivo .ilearner em um armazenamento de BLOBs do Azure. Olá **padrão de ponto de extremidade** é criado automaticamente para você quando você publica o treinamento Olá testar como um serviço web. Você pode criar mais pontos de extremidade, mas exemplo hello usa apenas Olá ponto de extremidade padrão.
- **Pontuação do serviço Web** - recebe exemplos de dados sem rótulo de e faz previsões. saída de Hello de previsão pode ter várias formas, como um arquivo. csv ou linhas em um banco de dados SQL do Azure, dependendo da configuração de saudação do experimento hello. ponto de extremidade saudação padrão é criado automaticamente para você quando você publica a experiência de previsão de saudação como um serviço web. 

Olá, imagem a seguir descreve Olá relação entre o treinamento e pontuação de pontos de extremidade no Azure ML.

![SERVIÇOS WEB](./media/data-factory-azure-ml-batch-execution-activity/web-services.png)

Você pode chamar hello **treinamento de serviço web** usando Olá **atividades de execução em lote do Azure ML**. A invocação de um serviço Web de treinamento é igual à invocação de um serviço Web do AM do Azure ML (serviço Web de pontuação) para pontuação de dados. Olá cobertura de seções anteriores como tooinvoke um serviço de web do ML do Azure de uma fábrica de dados do Azure pipeline em detalhes. 

Você pode chamar hello **serviço web de pontuação** usando Olá **atividades de recurso de atualização do Azure ML** tooupdate Olá web service com hello recentemente treinado. Olá exemplos a seguir fornece as definições de serviço vinculado: 

## <a name="scoring-web-service-is-a-classic-web-service"></a>Serviço web de pontuação é um serviço web clássico
Se Olá pontuação serviço web é um **serviço web clássico**, criar hello segundo **ponto de extremidade não padrão e atualizável** usando Olá [portal do Azure](https://manage.windowsazure.com). Confira o artigo [Criar pontos de extremidade](../machine-learning/machine-learning-create-endpoint.md) para conhecer as etapas. Depois de criar o ponto de extremidade atualizável Olá não padrão, Olá etapas a seguir:

* Clique em **BATCH EXECUTION** tooget Olá URI valor para Olá **mlEndpoint** propriedade JSON.
* Clique em **recurso de atualização** vincular o valor de URI de saudação tooget para Olá **updateResourceEndpoint** propriedade JSON. chave de API de saudação é na própria página de ponto de extremidade hello (no canto do hello inferior direito).

![ponto de extremidade atualizável](./media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

saudação de exemplo a seguir fornece um exemplo de definição de JSON para Olá serviço vinculado do AzureML. Olá apiKey de saudação do serviço vinculado usa para autenticação.  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a>Serviço Web de pontuação é um serviço Web do Azure Resource Manager 
Se o serviço web de saudação é Olá novo tipo de serviço da web que expõe um ponto de extremidade do Gerenciador de recursos do Azure, não é necessário tooadd Olá segundo **não-padrão** ponto de extremidade. Olá **updateResourceEndpoint** em Olá serviço vinculado é do formato de saudação: 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

Você pode obter valores de espaços reservados na URL de saudação ao consultar o serviço web Olá Olá [o Portal de serviços do Azure Machine Learning Web](https://services.azureml.net/). novo tipo de saudação do ponto de extremidade do recurso de atualização requer um token do AAD (Azure Active Directory). Especifique **servicePrincipalId** e **servicePrincipalKey**no serviço vinculado do AzureML. Consulte [como toocreate principal de serviço e atribuir permissões toomanage recursos do Azure](../azure-resource-manager/resource-group-create-service-principal-portal.md). Aqui está um exemplo de definição de serviço AzureML vinculado: 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "hello linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

Olá cenário a seguir fornece mais detalhes. Ele tem um exemplo de readaptação e atualização de modelos de AM do Azure de um pipeline do Azure Data Factory.

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a>Cenário: novo treinamento e atualização de um modelo do AM do Azure
Esta seção fornece um pipeline de exemplo que usa Olá **atividade de execução de lote do Azure ML** tooretrain um modelo. pipeline de saudação também usa Olá **atividade de atualização do recurso do Azure ML** tooupdate modelo Olá Olá pontuação serviço da web. Olá fornece também Olá de trechos de código JSON para todos os serviços vinculados, conjuntos de dados e pipeline no exemplo hello.

Aqui está o modo de exibição de diagrama de saudação do pipeline de exemplo hello. Como você pode ver, hello atividade de execução de lote do Azure ML aceita entrada de treinamento hello e produz uma saída de treinamento (arquivo iLearner). Hello atividade de recursos do Azure ML atualização usa esta saída de treinamento e atualizações Olá modelo no hello pontuação de ponto de extremidade de serviço web. Hello atividade de atualização de recurso não produz nenhuma saída. Olá placeholderBlob é apenas um saída fictício conjunto de dados que é exigido pelo pipeline de saudação do hello Azure Data Factory serviço toorun.

![diagrama de pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a>Serviço vinculado do armazenamento de Blob do Azure:
saudação de armazenamento do Azure mantém Olá seguintes dados:

* dados de treinamento. dados de entrada Hello para serviço de web de treinamento Olá ML do Azure.  
* Arquivo iLearner. saudação de saída do serviço web do hello Azure ML treinamento. Esse arquivo também é toohello de entrada hello atividade do recurso de atualização.  

Aqui está a definição de JSON de exemplo hello do serviço vinculado de saudação:

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a>Conjunto de dados de entrada do treinamento:
Olá seguinte conjunto de dados representa dados de treinamento de entrada hello para serviço de web de treinamento Olá ML do Azure. Hello atividade de execução de lote do ML do Azure usa esse conjunto de dados como entrada.

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a>Conjunto de dados de saída de treinamento:
Olá seguinte conjunto de dados representa Olá saída iLearner arquivo do serviço web do hello Azure ML treinamento. Hello atividade de execução de lote do Azure ML produz este conjunto de dados. Este conjunto de dados também é toohello de entrada hello atividade de atualização do recurso do Azure ML.

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a>Serviço vinculado para o ponto de extremidade de treinamento do AM do Azure ML
Olá trecho JSON a seguir define um serviço vinculado do aprendizado de máquina do Azure que aponta toohello o ponto de extremidade padrão do serviço de web hello treinamento.

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

Em **Azure ML Studio**, Olá seguintes valores de tooget para **mlEndpoint** e **apiKey**:

1. Clique em **serviços WEB** no menu esquerdo hello.
2. Clique em Olá **treinamento de serviço web** na lista de saudação de serviços web.
3. Em Copiar Avançar muito**chave API** caixa de texto. Cole editor de JSON da fábrica de dados Olá chave Olá na área de transferência hello.
4. Em Olá **studio ML do Azure**, clique em **BATCH EXECUTION** link.
5. Saudação de cópia **URI da solicitação** de saudação **solicitação** seção e colá-lo no editor de JSON da fábrica de dados de saudação.   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a>Serviço Vinculado para o ponto de extremidade de pontuação atualizável do AM do Azure:
Olá trecho JSON a seguir define um serviço vinculado do aprendizado de máquina do Azure que aponta toohello padrão não atualizável ponto de extremidade de Olá pontuação serviço da web.  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a>Conjunto de dados de saída de espaço reservado:
Hello atividade de atualização do recurso do Azure ML não gera nenhuma saída. No entanto, o Azure Data Factory requer uma conjunto de dados toodrive Olá agenda de um pipeline. Portanto, usamos um conjunto de dados fictício/espaço reservado neste exemplo.  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a>Pipeline
pipeline de saudação tem duas atividades: **AzureMLBatchExecution** e **AzureMLUpdateResource**. Hello atividade de execução de lote do ML do Azure usa dados de treinamento hello como entrada e produz um arquivo iLearner como saída. atividade de Olá chama o serviço web de treinamento hello (experiência de treinamento exposto como um serviço da web) com dados de treinamento de entrada hello e recebe o arquivo ilearner de saudação do hello webservice. Olá placeholderBlob é apenas um saída fictício conjunto de dados que é exigido pelo pipeline de saudação do hello Azure Data Factory serviço toorun.

![diagrama de pipeline](./media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```
