---
title: Usar modelos do Resource Manager no Data Factory | Microsoft Docs
description: Saiba como criar e usar modelos do Azure Resource Manager para criar entidades de Data Factory.
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
ms.openlocfilehash: c3ea2c047434b5b5495f0ce85be9376a502e4962
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-templates-to-create-azure-data-factory-entities"></a><span data-ttu-id="4b134-103">Usar modelos para criar entidades do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b134-103">Use templates to create Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="4b134-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4b134-104">Overview</span></span>
<span data-ttu-id="4b134-105">Ao usar o Azure Data Factory para suas necessidades de integração de dados, talvez você precise reutilizar o mesmo padrão em diversos ambientes ou implementar a mesma tarefa repetidamente na mesma solução.</span><span class="sxs-lookup"><span data-stu-id="4b134-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing the same pattern across different environments or implementing the same task repetitively within the same solution.</span></span> <span data-ttu-id="4b134-106">Modelos ajudam você a implementar e gerenciar estes cenários de forma fácil.</span><span class="sxs-lookup"><span data-stu-id="4b134-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="4b134-107">Modelos no Azure Data Factory são ideais para cenários que envolvem reutilização e repetição.</span><span class="sxs-lookup"><span data-stu-id="4b134-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="4b134-108">Considere a situação em que uma organização tem 10 instalações de produção em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="4b134-108">Consider the situation where an organization has 10 manufacturing plants across the world.</span></span> <span data-ttu-id="4b134-109">Os logs de cada fábrica são armazenados em um banco de dados do SQL Server local separado.</span><span class="sxs-lookup"><span data-stu-id="4b134-109">The logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="4b134-110">A empresa quer criar um único data warehouse na nuvem para análise ad hoc.</span><span class="sxs-lookup"><span data-stu-id="4b134-110">The company wants to build a single data warehouse in the cloud for ad-hoc analytics.</span></span> <span data-ttu-id="4b134-111">Ele também quer ter a mesma lógica, mas configurações diferentes para ambientes de desenvolvimento, teste e produção.</span><span class="sxs-lookup"><span data-stu-id="4b134-111">It also wants to have the same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="4b134-112">Nesse caso, uma tarefa precisa ser repetida dentro do mesmo ambiente, mas com valores diferentes entre as 10 fábricas de dados para cada fábrica.</span><span class="sxs-lookup"><span data-stu-id="4b134-112">In this case, a task needs to be repeated within the same environment, but with different values across the 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="4b134-113">Na verdade, **repetição** está presente.</span><span class="sxs-lookup"><span data-stu-id="4b134-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="4b134-114">A modelagem permite a abstração desse fluxo genérico (ou seja, pipelines com as mesmas atividades em cada data factory), mas usa um arquivo de parâmetro separado para cada fábrica.</span><span class="sxs-lookup"><span data-stu-id="4b134-114">Templating allows the abstraction of this generic flow (that is, pipelines having the same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="4b134-115">Além disso, como a organização deseja implantar essas 10 data factories diversas vezes em vários ambientes, os modelos podem usar a **reutilização** ao utilizar arquivos de parâmetros separados para ambientes de desenvolvimento, teste e produção.</span><span class="sxs-lookup"><span data-stu-id="4b134-115">Furthermore, as the organization wants to deploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="4b134-116">Modelagem com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b134-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="4b134-117">[Modelos do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#template-deployment) são uma ótima maneira de obter modelagem no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4b134-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way to achieve templating in Azure Data Factory.</span></span> <span data-ttu-id="4b134-118">Os modelos do Resource Manager definem a infraestrutura e a configuração de sua solução do Azure por meio de um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="4b134-118">Resource Manager templates define the infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="4b134-119">Como modelos de Azure Resource Manager funcionam com todos/quase todos os serviços do Azure, eles podem ser amplamente usados para gerenciar facilmente todos os recursos dos ativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b134-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used to easily manage all resources of your Azure assets.</span></span> <span data-ttu-id="4b134-120">Consulte [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) para saber mais sobre os modelos do Resource Manager em geral.</span><span class="sxs-lookup"><span data-stu-id="4b134-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to learn more about the Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="4b134-121">Tutoriais</span><span class="sxs-lookup"><span data-stu-id="4b134-121">Tutorials</span></span>
<span data-ttu-id="4b134-122">Consulte os tutoriais a seguir para obter instruções passo a passo para criar entidades de Data Factory usando modelos do Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="4b134-122">See the following tutorials for step-by-step instructions to create Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="4b134-123">Tutorial: criar um pipeline para copiar os dados usando o modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b134-123">Tutorial: Create a pipeline to copy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="4b134-124">Tutorial: criar um pipeline para processar os dados usando o modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4b134-124">Tutorial: Create a pipeline to process data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="4b134-125">Modelos do Data Factory no GitHub</span><span class="sxs-lookup"><span data-stu-id="4b134-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="4b134-126">Confira os seguintes modelos de início rápido do Azure no GitHub:</span><span class="sxs-lookup"><span data-stu-id="4b134-126">Check out the following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="4b134-127">Criar o Data Factory para copiar dados do Armazenamento de Blobs do Azure para o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="4b134-127">Create a Data factory to copy data from Azure Blob Storage to Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="4b134-128">Criar um Data Factory com a atividade do Hive em um cluster HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="4b134-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="4b134-129">Criar um Data Factory para copiar dados do Salesforce para Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="4b134-129">Create a Data factory to copy data from Salesforce to Azure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="4b134-130">Criar um Data Factory que encadeia atividades: copia dados de um servidor FTP para Blobs do Azure, invoca um script hive em um cluster HDInsight sob demanda para transformar os dados e copia o resultado no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="4b134-130">Create a Data factory that chains activities: copies data from an FTP server to Azure Blobs, invokes a hive script on an on-demand HDInsight cluster to transform the data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="4b134-131">Fique à vontade para compartilhar seus modelos do Azure Data Factory em [início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="4b134-131">Feel free to share your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="4b134-132">Consulte o [guia de contribuição](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) ao desenvolver modelos que podem ser compartilhados por meio deste repositório.</span><span class="sxs-lookup"><span data-stu-id="4b134-132">Refer to the [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="4b134-133">As seções a seguir fornecem detalhes sobre como definir recursos do Data Factory em um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4b134-133">The following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="4b134-134">Definir recursos de Data Factory em modelos</span><span class="sxs-lookup"><span data-stu-id="4b134-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="4b134-135">O modelo de nível superior para definir um Data Factory é:</span><span class="sxs-lookup"><span data-stu-id="4b134-135">The top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="4b134-136">Definir Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b134-136">Define data factory</span></span>
<span data-ttu-id="4b134-137">Você pode definir um Data Factory no modelo do Resource Manager, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b134-137">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="4b134-138">O dataFactoryName é definido em “variáveis” como:</span><span class="sxs-lookup"><span data-stu-id="4b134-138">The dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="4b134-139">Definir serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="4b134-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="4b134-140">Consulte [Serviço de Armazenamento Vinculado](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [Serviços de Computação Vinculados](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes sobre as propriedades JSON para o serviço vinculado específico que você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="4b134-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about the JSON properties for the specific linked service you wish to deploy.</span></span> <span data-ttu-id="4b134-141">O parâmetro "dependsOn" especifica o nome do Data Factory correspondente.</span><span class="sxs-lookup"><span data-stu-id="4b134-141">The “dependsOn” parameter specifies name of the corresponding data factory.</span></span> <span data-ttu-id="4b134-142">Um exemplo de definição de um serviço vinculado do Armazenamento do Azure é mostrado na definição de JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b134-142">An example of defining a linked service for Azure Storage is shown in the following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="4b134-143">Definir conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="4b134-143">Define datasets</span></span>

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
<span data-ttu-id="4b134-144">Consulte [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para obter detalhes sobre as propriedades JSON para o tipo de conjunto de dados específico que você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="4b134-144">Refer to [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about the JSON properties for the specific dataset type you wish to deploy.</span></span> <span data-ttu-id="4b134-145">Observe que o parâmetro "dependsOn" especifica o nome do Data Factory correspondente e o serviço de armazenamento vinculado.</span><span class="sxs-lookup"><span data-stu-id="4b134-145">Note the “dependsOn” parameter specifies name of the corresponding data factory and storage linked service.</span></span> <span data-ttu-id="4b134-146">Um exemplo de definição de um tipo de conjunto de dados do armazenamento de blobs do Azure na seguinte definição JSON:</span><span class="sxs-lookup"><span data-stu-id="4b134-146">An example of defining dataset type of Azure blob storage is shown in the following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="4b134-147">Definir pipelines</span><span class="sxs-lookup"><span data-stu-id="4b134-147">Define pipelines</span></span>

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

<span data-ttu-id="4b134-148">Consulte [definindo pipelines](data-factory-create-pipelines.md#pipeline-json) para obter detalhes sobre as propriedades JSON para definir o pipeline específico e as atividades que você deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="4b134-148">Refer to [defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about the JSON properties for defining the specific pipeline and activities you wish to deploy.</span></span> <span data-ttu-id="4b134-149">Observe o parâmetro "dependsOn" especifica o nome do Data Factory e quaisquer serviços vinculados ou conjuntos de dados correspondentes.</span><span class="sxs-lookup"><span data-stu-id="4b134-149">Note the “dependsOn” parameter specifies name of the data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="4b134-150">Um exemplo de um pipeline que copia dados do Armazenamento de Blobs do Azure para o Banco de Dados SQL é mostrado no seguinte trecho de JSON:</span><span class="sxs-lookup"><span data-stu-id="4b134-150">An example of a pipeline that copies data from Azure Blob Storage to Azure SQL Database is shown in the following JSON snippet:</span></span>

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
    "start": "2016-10-03T00:00:00Z",
    "end": "2016-10-04T00:00:00Z"
}
```
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="4b134-151">Parametrizando o modelo de Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b134-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="4b134-152">Para obter as práticas recomendadas sobre parametrização, consulte o artigo [Práticas recomendadas para criar modelos do Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="4b134-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="4b134-153">Em geral, o uso do parâmetro deverá ser minimizado, especialmente se variáveis puderem ser usadas em vez disso.</span><span class="sxs-lookup"><span data-stu-id="4b134-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="4b134-154">Apenas forneça parâmetros nos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="4b134-154">Only provide parameters in the following scenarios:</span></span>

* <span data-ttu-id="4b134-155">As configurações variam de acordo com ambiente (exemplo: desenvolvimento, teste e produção)</span><span class="sxs-lookup"><span data-stu-id="4b134-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="4b134-156">Segredos (por exemplo, senhas)</span><span class="sxs-lookup"><span data-stu-id="4b134-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="4b134-157">Se você precisar receber segredos do [Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md) ao implantar entidades do Azure Data Factory usando modelos, especifique o **cofre de chaves** e **nome secreto** conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b134-157">If you need to pull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify the **key vault** and **secret name** as shown in the following example:</span></span>

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
> <span data-ttu-id="4b134-158">Embora ainda não haja suporte para exportar modelos para Data Factories existentes, ele ainda funciona.</span><span class="sxs-lookup"><span data-stu-id="4b134-158">While exporting templates for existing data factories is currently not yet supported, it is in the works.</span></span>
>
>
