---
title: "modelos do Gerenciador de recursos de aaaUse na fábrica de dados | Microsoft Docs"
description: "Saiba como toocreate entidades e de uso do Azure Resource Manager modelos toocreate fábrica de dados."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: 
ms.assetid: 37724021-f55f-4e85-9206-6d4a48bda3d8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 60d5dbd29494420006aed6d5bd9a10a63c36bec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-templates-toocreate-azure-data-factory-entities"></a>Usar modelos toocreate do Azure Data Factory entidades
## <a name="overview"></a>Visão geral
Durante o uso do Azure Data Factory para suas necessidades de integração de dados, você pode perceber que está reutilizando Olá mesmo padrão em diferentes ambientes ou implementando Olá mesma tarefa repetidamente dentro do hello mesmo solução. Modelos ajudam você a implementar e gerenciar estes cenários de forma fácil. Modelos no Azure Data Factory são ideais para cenários que envolvem reutilização e repetição.

Considere uma situação de saudação em que uma organização tem 10 instalações de produção em Olá, mundo. logs de saudação de cada fábrica são armazenados em um banco de dados do SQL Server local separado. empresa de saudação deseja toobuild um único data warehouse na nuvem Olá para análise ad hoc. Ele também deseja toohave Olá mesma lógica, mas diferentes configurações para ambientes de desenvolvimento, teste e produção.

Nesse caso, uma tarefa precisar toobe repetido dentro Olá mesmo ambiente, mas com diferentes valores entre Olá 10 fábricas de dados para cada fábrica. Na verdade, **repetição** está presente. Permite a modelagem abstração Olá este fluxo genérico (ou seja, pipelines tendo Olá atividades mesmo em cada fábrica de dados), mas usa um arquivo de parâmetro separado para cada fábrica.

Além disso, como Olá organização deseja que toodeploy essas fábricas de dados de 10 várias vezes em diferentes ambientes, modelos podem usar isso **reutilização** utilizando os arquivos de parâmetros separados para desenvolvimento, teste, e ambientes de produção.

## <a name="templating-with-azure-resource-manager"></a>Modelagem com o Azure Resource Manager
[Modelos do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md#template-deployment) são modelos de tooachieve uma ótima maneira na fábrica de dados do Azure. Modelos do Gerenciador de recursos definem infraestrutura hello e a configuração de sua solução do Azure por meio de um arquivo JSON. Como os modelos de Gerenciador de recursos do Azure funcionam com a maioria dos/de todos os serviços do Azure, ele pode ser amplamente usado tooeasily gerenciar todos os recursos dos ativos do Azure. Consulte [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn mais sobre Olá modelos do Gerenciador de recursos em geral.

## <a name="tutorials"></a>Tutoriais
Consulte Olá seguintes tutoriais para entidades de fábrica de dados toocreate instruções passo a passo usando modelos do Gerenciador de recursos:

* [Tutorial: Criar um pipeline de dados de toocopy usando o modelo do Gerenciador de recursos do Azure](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [Tutorial: Criar um pipeline de dados de tooprocess usando o modelo do Gerenciador de recursos do Azure](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a>Modelos do Data Factory no GitHub
Check-out Olá seguindo os modelos de início rápido do Azure no GitHub:

* [Criar um toocopy dados da fábrica de dados do armazenamento de BLOBs do Azure tooAzure banco de dados SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [Criar um Data Factory com a atividade do Hive em um cluster HDInsight do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [Criar um toocopy dados da fábrica de dados do Salesforce tooAzure Blobs](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [Criar uma fábrica de dados que se encadeia atividades: copia dados de um servidor FTP tooAzure Blobs, chama um script de hive em um HDInsight cluster tootransform Olá de dados sob demanda e copia os resultados no banco de dados do SQL Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

Sinta-se livre tooshare seus modelos do Azure Data Factory em [início rápido do Azure](https://azure.microsoft.com/documentation/templates/). Consulte toohello [guia contribuição](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) durante o desenvolvimento de modelos que podem ser compartilhados por meio deste repositório.

Olá seções a seguir fornece detalhes sobre como definir recursos de fábrica de dados em um modelo do Gerenciador de recursos.

## <a name="defining-data-factory-resources-in-templates"></a>Definir recursos de Data Factory em modelos
saudação de modelo de nível superior para definir uma fábrica de dados é:

```JSON
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
    { "type": "linkedservices",
        ...
    },
    {"type": "datasets",
        ...
    },
    {"type": "dataPipelines",
        ...
    }
}
```

### <a name="define-data-factory"></a>Definir Data Factory
Você pode definir uma fábrica de dados no modelo do Gerenciador de recursos de saudação conforme Olá exemplo a seguir:

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
Olá dataFactoryName é definido em "variáveis" como:

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a>Definir serviços vinculados

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

Consulte [serviço vinculado do armazenamento](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [serviços vinculados de computação](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes sobre as propriedades JSON Olá para o serviço vinculado específico de saudação desejar toodeploy. parâmetro de "dependsOn" Hello Especifica o nome da fábrica de dados correspondente hello. Um exemplo de definição de um serviço vinculado de armazenamento do Azure é mostrado no hello definição JSON a seguir:

### <a name="define-datasets"></a>Definir conjuntos de dados

```JSON
"type": "datasets",
"name": "[variables('<myDatasetName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<myDatasetLinkedServiceName>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    ...
}
```
Consulte também[suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para obter detalhes sobre as propriedades JSON Olá para o tipo de conjunto de dados específico Olá desejar toodeploy. Observação hello "dependsOn" parâmetro especifica o nome de dados correspondentes Olá serviço vinculado de armazenamento e fábrica. Um exemplo de definição de tipo de conjunto de dados de armazenamento de BLOBs do Azure é mostrado no hello definição JSON a seguir:

```JSON
"type": "datasets",
"name": "[variables('storageDataset')]",
"dependsOn": [
    "[variables('dataFactoryName')]",
    "[variables('storageLinkedServiceName')]"
],
"apiVersion": "2015-10-01",
"properties": {
"type": "AzureBlob",
"linkedServiceName": "[variables('storageLinkedServiceName')]",
"typeProperties": {
    "folderPath": "[concat(parameters('sourceBlobContainer'), '/')]",
    "fileName": "[parameters('sourceBlobName')]",
    "format": {
        "type": "TextFormat"
    }
},
"availability": {
    "frequency": "Hour",
    "interval": 1
}
```

### <a name="define-pipelines"></a>Definir pipelines

```JSON
"type": "dataPipelines",
"name": "[variables('<mypipelineName>')]",
"dependsOn": [
    "[variables('<dataFactoryName>')]",
    "[variables('<inputDatasetLinkedServiceName>')]",
    "[variables('<outputDatasetLinkedServiceName>')]",
    "[variables('<inputDataset>')]",
    "[variables('<outputDataset>')]"
],
"apiVersion": "2015-10-01",
"properties": {
    activities: {
        ...
    }
}
```

Consulte também[definir pipelines](data-factory-create-pipelines.md#pipeline-json) para obter detalhes sobre propriedades JSON Olá para definir Olá específico pipeline e atividades desejar toodeploy. Observação hello "dependsOn" parâmetro especifica o nome hello da fábrica de dados e serviços vinculados correspondentes ou conjuntos de dados. Um exemplo de um pipeline que copia dados de armazenamento de BLOBs do Azure tooAzure banco de dados SQL é mostrado no hello trecho JSON a seguir:

```JSON
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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a>Parametrizando o modelo de Data Factory
Para obter as práticas recomendadas sobre parametrização, consulte o artigo [Práticas recomendadas para criar modelos do Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters). Em geral, o uso do parâmetro deverá ser minimizado, especialmente se variáveis puderem ser usadas em vez disso. Apenas fornece parâmetros em Olá os seguintes cenários:

* As configurações variam de acordo com ambiente (exemplo: desenvolvimento, teste e produção)
* Segredos (por exemplo, senhas)

Se você precisar de segredos toopull de [Azure Key Vault](../key-vault/key-vault-get-started.md) quando entidades do Azure Data Factory usando modelos de implantação, especifique Olá **Cofre de chaves** e **nome secreto** conforme mostrado na saudação de exemplo a seguir:

```JSON
"parameters": {
    "storageAccountKey": {
        "reference": {
            "keyVault": {
                "id":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.KeyVault/vaults/<keyVaultName>",
             },
            "secretName": "<secretName>"
           },
       },
       ...
}
```

> [!NOTE]
> Ao exportar modelos para fábricas de dados existente no momento ainda não é suportada, é em Olá funciona.
>
>
