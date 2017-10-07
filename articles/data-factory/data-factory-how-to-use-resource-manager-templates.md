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
# <a name="use-templates-toocreate-azure-data-factory-entities"></a><span data-ttu-id="638fe-103">Usar modelos toocreate do Azure Data Factory entidades</span><span class="sxs-lookup"><span data-stu-id="638fe-103">Use templates toocreate Azure Data Factory entities</span></span>
## <a name="overview"></a><span data-ttu-id="638fe-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="638fe-104">Overview</span></span>
<span data-ttu-id="638fe-105">Durante o uso do Azure Data Factory para suas necessidades de integração de dados, você pode perceber que está reutilizando Olá mesmo padrão em diferentes ambientes ou implementando Olá mesma tarefa repetidamente dentro do hello mesmo solução.</span><span class="sxs-lookup"><span data-stu-id="638fe-105">While using Azure Data Factory for your data integration needs, you may find yourself reusing hello same pattern across different environments or implementing hello same task repetitively within hello same solution.</span></span> <span data-ttu-id="638fe-106">Modelos ajudam você a implementar e gerenciar estes cenários de forma fácil.</span><span class="sxs-lookup"><span data-stu-id="638fe-106">Templates help you implement and manage these scenarios in an easy manner.</span></span> <span data-ttu-id="638fe-107">Modelos no Azure Data Factory são ideais para cenários que envolvem reutilização e repetição.</span><span class="sxs-lookup"><span data-stu-id="638fe-107">Templates in Azure Data Factory are ideal for scenarios that involve reusability and repetition.</span></span>

<span data-ttu-id="638fe-108">Considere uma situação de saudação em que uma organização tem 10 instalações de produção em Olá, mundo.</span><span class="sxs-lookup"><span data-stu-id="638fe-108">Consider hello situation where an organization has 10 manufacturing plants across hello world.</span></span> <span data-ttu-id="638fe-109">logs de saudação de cada fábrica são armazenados em um banco de dados do SQL Server local separado.</span><span class="sxs-lookup"><span data-stu-id="638fe-109">hello logs from each plant are stored in a separate on-premises SQL Server database.</span></span> <span data-ttu-id="638fe-110">empresa de saudação deseja toobuild um único data warehouse na nuvem Olá para análise ad hoc.</span><span class="sxs-lookup"><span data-stu-id="638fe-110">hello company wants toobuild a single data warehouse in hello cloud for ad-hoc analytics.</span></span> <span data-ttu-id="638fe-111">Ele também deseja toohave Olá mesma lógica, mas diferentes configurações para ambientes de desenvolvimento, teste e produção.</span><span class="sxs-lookup"><span data-stu-id="638fe-111">It also wants toohave hello same logic but different configurations for development, test, and production environments.</span></span>

<span data-ttu-id="638fe-112">Nesse caso, uma tarefa precisar toobe repetido dentro Olá mesmo ambiente, mas com diferentes valores entre Olá 10 fábricas de dados para cada fábrica.</span><span class="sxs-lookup"><span data-stu-id="638fe-112">In this case, a task needs toobe repeated within hello same environment, but with different values across hello 10 data factories for each manufacturing plant.</span></span> <span data-ttu-id="638fe-113">Na verdade, **repetição** está presente.</span><span class="sxs-lookup"><span data-stu-id="638fe-113">In effect, **repetition** is present.</span></span> <span data-ttu-id="638fe-114">Permite a modelagem abstração Olá este fluxo genérico (ou seja, pipelines tendo Olá atividades mesmo em cada fábrica de dados), mas usa um arquivo de parâmetro separado para cada fábrica.</span><span class="sxs-lookup"><span data-stu-id="638fe-114">Templating allows hello abstraction of this generic flow (that is, pipelines having hello same activities in each data factory), but uses a separate parameter file for each manufacturing plant.</span></span>

<span data-ttu-id="638fe-115">Além disso, como Olá organização deseja que toodeploy essas fábricas de dados de 10 várias vezes em diferentes ambientes, modelos podem usar isso **reutilização** utilizando os arquivos de parâmetros separados para desenvolvimento, teste, e ambientes de produção.</span><span class="sxs-lookup"><span data-stu-id="638fe-115">Furthermore, as hello organization wants toodeploy these 10 data factories multiple times across different environments, templates can use this **reusability** by utilizing separate parameter files for development, test, and production environments.</span></span>

## <a name="templating-with-azure-resource-manager"></a><span data-ttu-id="638fe-116">Modelagem com o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="638fe-116">Templating with Azure Resource Manager</span></span>
<span data-ttu-id="638fe-117">[Modelos do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md#template-deployment) são modelos de tooachieve uma ótima maneira na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="638fe-117">[Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md#template-deployment) are a great way tooachieve templating in Azure Data Factory.</span></span> <span data-ttu-id="638fe-118">Modelos do Gerenciador de recursos definem infraestrutura hello e a configuração de sua solução do Azure por meio de um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="638fe-118">Resource Manager templates define hello infrastructure and configuration of your Azure solution through a JSON file.</span></span> <span data-ttu-id="638fe-119">Como os modelos de Gerenciador de recursos do Azure funcionam com a maioria dos/de todos os serviços do Azure, ele pode ser amplamente usado tooeasily gerenciar todos os recursos dos ativos do Azure.</span><span class="sxs-lookup"><span data-stu-id="638fe-119">Because Azure Resource Manager templates work with all/most Azure services, it can be widely used tooeasily manage all resources of your Azure assets.</span></span> <span data-ttu-id="638fe-120">Consulte [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) toolearn mais sobre Olá modelos do Gerenciador de recursos em geral.</span><span class="sxs-lookup"><span data-stu-id="638fe-120">See [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) toolearn more about hello Resource Manager Templates in general.</span></span>

## <a name="tutorials"></a><span data-ttu-id="638fe-121">Tutoriais</span><span class="sxs-lookup"><span data-stu-id="638fe-121">Tutorials</span></span>
<span data-ttu-id="638fe-122">Consulte Olá seguintes tutoriais para entidades de fábrica de dados toocreate instruções passo a passo usando modelos do Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="638fe-122">See hello following tutorials for step-by-step instructions toocreate Data Factory entities by using Resource Manager templates:</span></span>

* [<span data-ttu-id="638fe-123">Tutorial: Criar um pipeline de dados de toocopy usando o modelo do Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="638fe-123">Tutorial: Create a pipeline toocopy data by using Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="638fe-124">Tutorial: Criar um pipeline de dados de tooprocess usando o modelo do Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="638fe-124">Tutorial: Create a pipeline tooprocess data by using Azure Resource Manager template</span></span>](data-factory-build-your-first-pipeline.md)

## <a name="data-factory-templates-on-github"></a><span data-ttu-id="638fe-125">Modelos do Data Factory no GitHub</span><span class="sxs-lookup"><span data-stu-id="638fe-125">Data Factory templates on GitHub</span></span>
<span data-ttu-id="638fe-126">Check-out Olá seguindo os modelos de início rápido do Azure no GitHub:</span><span class="sxs-lookup"><span data-stu-id="638fe-126">Check out hello following Azure quick start templates on GitHub:</span></span>

* [<span data-ttu-id="638fe-127">Criar um toocopy dados da fábrica de dados do armazenamento de BLOBs do Azure tooAzure banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="638fe-127">Create a Data factory toocopy data from Azure Blob Storage tooAzure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy)
* [<span data-ttu-id="638fe-128">Criar um Data Factory com a atividade do Hive em um cluster HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="638fe-128">Create a Data factory with Hive activity on Azure HDInsight cluster</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation)
* [<span data-ttu-id="638fe-129">Criar um toocopy dados da fábrica de dados do Salesforce tooAzure Blobs</span><span class="sxs-lookup"><span data-stu-id="638fe-129">Create a Data factory toocopy data from Salesforce tooAzure Blobs</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy)
* [<span data-ttu-id="638fe-130">Criar uma fábrica de dados que se encadeia atividades: copia dados de um servidor FTP tooAzure Blobs, chama um script de hive em um HDInsight cluster tootransform Olá de dados sob demanda e copia os resultados no banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="638fe-130">Create a Data factory that chains activities: copies data from an FTP server tooAzure Blobs, invokes a hive script on an on-demand HDInsight cluster tootransform hello data, and copies result into Azure SQL Database</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-data-factory-ftp-hive-blob)

<span data-ttu-id="638fe-131">Sinta-se livre tooshare seus modelos do Azure Data Factory em [início rápido do Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="638fe-131">Feel free tooshare your Azure Data Factory templates at [Azure Quick start](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="638fe-132">Consulte toohello [guia contribuição](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) durante o desenvolvimento de modelos que podem ser compartilhados por meio deste repositório.</span><span class="sxs-lookup"><span data-stu-id="638fe-132">Refer toohello [contribution guide](https://github.com/Azure/azure-quickstart-templates/tree/master/1-CONTRIBUTION-GUIDE) while developing templates that can be shared via this repository.</span></span>

<span data-ttu-id="638fe-133">Olá seções a seguir fornece detalhes sobre como definir recursos de fábrica de dados em um modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="638fe-133">hello following sections provide details about defining Data Factory resources in a Resource Manager template.</span></span>

## <a name="defining-data-factory-resources-in-templates"></a><span data-ttu-id="638fe-134">Definir recursos de Data Factory em modelos</span><span class="sxs-lookup"><span data-stu-id="638fe-134">Defining Data Factory resources in templates</span></span>
<span data-ttu-id="638fe-135">saudação de modelo de nível superior para definir uma fábrica de dados é:</span><span class="sxs-lookup"><span data-stu-id="638fe-135">hello top-level template for defining a data factory is:</span></span>

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

### <a name="define-data-factory"></a><span data-ttu-id="638fe-136">Definir Data Factory</span><span class="sxs-lookup"><span data-stu-id="638fe-136">Define data factory</span></span>
<span data-ttu-id="638fe-137">Você pode definir uma fábrica de dados no modelo do Gerenciador de recursos de saudação conforme Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="638fe-137">You define a data factory in hello Resource Manager template as shown in hello following sample:</span></span>

```JSON
"resources": [
{
    "name": "[variables('<mydataFactoryName>')]",
    "apiVersion": "2015-10-01",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "East US"
}
```
<span data-ttu-id="638fe-138">Olá dataFactoryName é definido em "variáveis" como:</span><span class="sxs-lookup"><span data-stu-id="638fe-138">hello dataFactoryName is defined in “variables” as:</span></span>

```JSON
"dataFactoryName": "[concat('<myDataFactoryName>', uniqueString(resourceGroup().id))]",
```

### <a name="define-linked-services"></a><span data-ttu-id="638fe-139">Definir serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="638fe-139">Define linked services</span></span>

```JSON
"type": "linkedservices",
"name": "[variables('<LinkedServiceName>')]",
"apiVersion": "2015-10-01",
"dependsOn": [ "[variables('<dataFactoryName>')]" ],
"properties": {
    ...
}
```

<span data-ttu-id="638fe-140">Consulte [serviço vinculado do armazenamento](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [serviços vinculados de computação](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) para obter detalhes sobre as propriedades JSON Olá para o serviço vinculado específico de saudação desejar toodeploy.</span><span class="sxs-lookup"><span data-stu-id="638fe-140">See [Storage Linked Service](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [Compute Linked Services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details about hello JSON properties for hello specific linked service you wish toodeploy.</span></span> <span data-ttu-id="638fe-141">parâmetro de "dependsOn" Hello Especifica o nome da fábrica de dados correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="638fe-141">hello “dependsOn” parameter specifies name of hello corresponding data factory.</span></span> <span data-ttu-id="638fe-142">Um exemplo de definição de um serviço vinculado de armazenamento do Azure é mostrado no hello definição JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="638fe-142">An example of defining a linked service for Azure Storage is shown in hello following JSON definition:</span></span>

### <a name="define-datasets"></a><span data-ttu-id="638fe-143">Definir conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="638fe-143">Define datasets</span></span>

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
<span data-ttu-id="638fe-144">Consulte também[suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) para obter detalhes sobre as propriedades JSON Olá para o tipo de conjunto de dados específico Olá desejar toodeploy.</span><span class="sxs-lookup"><span data-stu-id="638fe-144">Refer too[Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for details about hello JSON properties for hello specific dataset type you wish toodeploy.</span></span> <span data-ttu-id="638fe-145">Observação hello "dependsOn" parâmetro especifica o nome de dados correspondentes Olá serviço vinculado de armazenamento e fábrica.</span><span class="sxs-lookup"><span data-stu-id="638fe-145">Note hello “dependsOn” parameter specifies name of hello corresponding data factory and storage linked service.</span></span> <span data-ttu-id="638fe-146">Um exemplo de definição de tipo de conjunto de dados de armazenamento de BLOBs do Azure é mostrado no hello definição JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="638fe-146">An example of defining dataset type of Azure blob storage is shown in hello following JSON definition:</span></span>

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

### <a name="define-pipelines"></a><span data-ttu-id="638fe-147">Definir pipelines</span><span class="sxs-lookup"><span data-stu-id="638fe-147">Define pipelines</span></span>

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

<span data-ttu-id="638fe-148">Consulte também[definir pipelines](data-factory-create-pipelines.md#pipeline-json) para obter detalhes sobre propriedades JSON Olá para definir Olá específico pipeline e atividades desejar toodeploy.</span><span class="sxs-lookup"><span data-stu-id="638fe-148">Refer too[defining pipelines](data-factory-create-pipelines.md#pipeline-json) for details about hello JSON properties for defining hello specific pipeline and activities you wish toodeploy.</span></span> <span data-ttu-id="638fe-149">Observação hello "dependsOn" parâmetro especifica o nome hello da fábrica de dados e serviços vinculados correspondentes ou conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="638fe-149">Note hello “dependsOn” parameter specifies name of hello data factory, and any corresponding linked services or datasets.</span></span> <span data-ttu-id="638fe-150">Um exemplo de um pipeline que copia dados de armazenamento de BLOBs do Azure tooAzure banco de dados SQL é mostrado no hello trecho JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="638fe-150">An example of a pipeline that copies data from Azure Blob Storage tooAzure SQL Database is shown in hello following JSON snippet:</span></span>

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
## <a name="parameterizing-data-factory-template"></a><span data-ttu-id="638fe-151">Parametrizando o modelo de Data Factory</span><span class="sxs-lookup"><span data-stu-id="638fe-151">Parameterizing Data Factory template</span></span>
<span data-ttu-id="638fe-152">Para obter as práticas recomendadas sobre parametrização, consulte o artigo [Práticas recomendadas para criar modelos do Azure Resource Manager](../azure-resource-manager/resource-manager-template-best-practices.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="638fe-152">For best practices on parameterizing, see [Best practices for creating Azure Resource Manager templates](../azure-resource-manager/resource-manager-template-best-practices.md#parameters) article.</span></span> <span data-ttu-id="638fe-153">Em geral, o uso do parâmetro deverá ser minimizado, especialmente se variáveis puderem ser usadas em vez disso.</span><span class="sxs-lookup"><span data-stu-id="638fe-153">In general, parameter usage should be minimized, especially if variables can be used instead.</span></span> <span data-ttu-id="638fe-154">Apenas fornece parâmetros em Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="638fe-154">Only provide parameters in hello following scenarios:</span></span>

* <span data-ttu-id="638fe-155">As configurações variam de acordo com ambiente (exemplo: desenvolvimento, teste e produção)</span><span class="sxs-lookup"><span data-stu-id="638fe-155">Settings vary by environment (example: development, test, and production)</span></span>
* <span data-ttu-id="638fe-156">Segredos (por exemplo, senhas)</span><span class="sxs-lookup"><span data-stu-id="638fe-156">Secrets (such as passwords)</span></span>

<span data-ttu-id="638fe-157">Se você precisar de segredos toopull de [Azure Key Vault](../key-vault/key-vault-get-started.md) quando entidades do Azure Data Factory usando modelos de implantação, especifique Olá **Cofre de chaves** e **nome secreto** conforme mostrado na saudação de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="638fe-157">If you need toopull secrets from [Azure Key Vault](../key-vault/key-vault-get-started.md) when deploying Azure Data Factory entities using templates, specify hello **key vault** and **secret name** as shown in hello following example:</span></span>

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
> <span data-ttu-id="638fe-158">Ao exportar modelos para fábricas de dados existente no momento ainda não é suportada, é em Olá funciona.</span><span class="sxs-lookup"><span data-stu-id="638fe-158">While exporting templates for existing data factories is currently not yet supported, it is in hello works.</span></span>
>
>
