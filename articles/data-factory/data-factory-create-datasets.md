---
title: "conjuntos de dados de aaaCreate na fábrica de dados do Azure | Microsoft Docs"
description: "Saiba como conjuntos de dados toocreate na fábrica de dados do Azure, com exemplos que usam propriedades, como deslocamento e anchorDateTime."
keywords: criar conjunto de dados, exemplo de conjunto de dados, exemplo de deslocamento
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="d2805-104">Conjuntos de dados no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d2805-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="d2805-105">Este artigo descreve o que são conjuntos de dados, como eles são definidos no formato JSON e como são usados em pipelines do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d2805-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="d2805-106">Ele fornece detalhes sobre cada seção (por exemplo, estrutura, disponibilidade e política) na definição de JSON de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-106">It provides details about each section (for example, structure, availability, and policy) in hello dataset JSON definition.</span></span> <span data-ttu-id="d2805-107">Olá artigo também fornece exemplos de uso Olá **deslocamento**, **anchorDateTime**, e **estilo** propriedades em uma definição de conjunto de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="d2805-107">hello article also provides examples for using hello **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="d2805-108">Se você for novo tooData fábrica, consulte [tooAzure Introdução Data Factory](data-factory-introduction.md) para obter uma visão geral.</span><span class="sxs-lookup"><span data-stu-id="d2805-108">If you are new tooData Factory, see [Introduction tooAzure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="d2805-109">Se você não tiver experiência prática com a criação de fábricas de dados, você pode obter um melhor entendimento por leitura Olá [tutorial de transformação de dados](data-factory-build-your-first-pipeline.md) e hello [tutorial de movimentação de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="d2805-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading hello [data transformation tutorial](data-factory-build-your-first-pipeline.md) and hello [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="d2805-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d2805-110">Overview</span></span>
<span data-ttu-id="d2805-111">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="d2805-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="d2805-112">Um **pipeline** é um agrupamento lógico de **atividades** que juntas executam uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="d2805-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="d2805-113">atividades de saudação em um pipeline definem ações tooperform em seus dados.</span><span class="sxs-lookup"><span data-stu-id="d2805-113">hello activities in a pipeline define actions tooperform on your data.</span></span> <span data-ttu-id="d2805-114">Por exemplo, você pode usar uma cópia de dados de toocopy de atividade de um tooAzure do SQL Server local armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="d2805-114">For example, you might use a copy activity toocopy data from an on-premises SQL Server tooAzure Blob storage.</span></span> <span data-ttu-id="d2805-115">Em seguida, você pode usar uma atividade de Hive que executa um script de Hive em um dado de tooprocess do cluster HDInsight do Azure de dados de saída de tooproduce de armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="d2805-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster tooprocess data from Blob storage tooproduce output data.</span></span> <span data-ttu-id="d2805-116">Por fim, você pode usar uma segunda cópia atividade toocopy Olá saída dados tooAzure SQL Data Warehouse, na parte superior que inteligência comercial (BI) reporting soluções são criadas.</span><span class="sxs-lookup"><span data-stu-id="d2805-116">Finally, you might use a second copy activity toocopy hello output data tooAzure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="d2805-117">Para obter mais informações sobre pipelines e atividades, consulte [Pipelines e atividades no Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d2805-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="d2805-118">Uma atividade pode usar zero ou mais **conjuntos de dados** de entrada e gerar um ou mais conjuntos de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="d2805-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="d2805-119">Um conjunto de dados de entrada representa a entrada de saudação para uma atividade no pipeline hello e um conjunto de dados de saída representa a saída de hello atividade hello.</span><span class="sxs-lookup"><span data-stu-id="d2805-119">An input dataset represents hello input for an activity in hello pipeline, and an output dataset represents hello output for hello activity.</span></span> <span data-ttu-id="d2805-120">Conjuntos de dados identificam dados em armazenamentos de dados diferentes, como tabelas, arquivos, pastas e documentos.</span><span class="sxs-lookup"><span data-stu-id="d2805-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="d2805-121">Por exemplo, um conjunto de dados de Blob do Azure Especifica Olá contêiner de blob e a pasta no armazenamento de Blob do qual Olá pipeline deve ler dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-121">For example, an Azure Blob dataset specifies hello blob container and folder in Blob storage from which hello pipeline should read hello data.</span></span> 

<span data-ttu-id="d2805-122">Antes de criar um conjunto de dados, criar um **serviço vinculado** toolink toohello fábrica de dados de repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="d2805-122">Before you create a dataset, create a **linked service** toolink your data store toohello data factory.</span></span> <span data-ttu-id="d2805-123">Serviços vinculados são bem semelhantes às cadeias de caracteres de conexão, que definem informações de conexão de Olá necessárias para os recursos do Data Factory tooconnect tooexternal.</span><span class="sxs-lookup"><span data-stu-id="d2805-123">Linked services are much like connection strings, which define hello connection information needed for Data Factory tooconnect tooexternal resources.</span></span> <span data-ttu-id="d2805-124">Conjuntos de dados identificam os dados Olá vinculado armazenamentos de dados, como tabelas SQL, arquivos, pastas e documentos.</span><span class="sxs-lookup"><span data-stu-id="d2805-124">Datasets identify data within hello linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="d2805-125">Por exemplo, um armazenamento do Azure vinculada links de serviço com uma fábrica de dados de toohello de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d2805-125">For example, an Azure Storage linked service links a storage account toohello data factory.</span></span> <span data-ttu-id="d2805-126">Um conjunto de dados de Blob do Azure representa o contêiner de blob hello e a pasta de Olá que contém a saudação blobs entrada toobe processado.</span><span class="sxs-lookup"><span data-stu-id="d2805-126">An Azure Blob dataset represents hello blob container and hello folder that contains hello input blobs toobe processed.</span></span> 

<span data-ttu-id="d2805-127">Veja abaixo um cenário de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d2805-127">Here is a sample scenario.</span></span> <span data-ttu-id="d2805-128">toocopy dados do banco de dados SQL tooa de armazenamento de Blob, criar dois serviços vinculados: o armazenamento do Azure e banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d2805-128">toocopy data from Blob storage tooa SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="d2805-129">Em seguida, crie dois conjuntos de dados: conjunto de dados de Blob do Azure (que refere-se o serviço de armazenamento do Azure vinculada toohello) e o conjunto de dados de tabela do SQL Azure (que refere-se o serviço de banco de dados do SQL Azure vinculado toohello).</span><span class="sxs-lookup"><span data-stu-id="d2805-129">Then, create two datasets: Azure Blob dataset (which refers toohello Azure Storage linked service) and Azure SQL Table dataset (which refers toohello Azure SQL Database linked service).</span></span> <span data-ttu-id="d2805-130">Olá armazenamento do Azure e banco de dados do SQL Azure serviços vinculados contêm cadeias de caracteres de conexão que usa fábrica de dados em tempo de execução tooconnect tooyour armazenamento do Azure e banco de dados SQL Azure, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="d2805-130">hello Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime tooconnect tooyour Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="d2805-131">conjunto de dados de Blob do Azure Olá Especifica o contêiner de blob hello e a pasta de blob que contém blobs de entrada hello em seu armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="d2805-131">hello Azure Blob dataset specifies hello blob container and blob folder that contains hello input blobs in your Blob storage.</span></span> <span data-ttu-id="d2805-132">conjunto de dados de tabela do SQL Azure Olá Especifica a tabela SQL de saudação em seus dados de saudação do toowhich de banco de dados SQL é toobe copiado.</span><span class="sxs-lookup"><span data-stu-id="d2805-132">hello Azure SQL Table dataset specifies hello SQL table in your SQL database toowhich hello data is toobe copied.</span></span>

<span data-ttu-id="d2805-133">Olá diagrama a seguir mostra Olá relações entre pipeline, atividade, conjunto de dados e serviços vinculados na fábrica de dados:</span><span class="sxs-lookup"><span data-stu-id="d2805-133">hello following diagram shows hello relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relação entre pipeline, atividade e conjunto de dados, serviços vinculados](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="d2805-135">Conjunto de dados do JSON</span><span class="sxs-lookup"><span data-stu-id="d2805-135">Dataset JSON</span></span>
<span data-ttu-id="d2805-136">Um conjunto de dados no Data Factory é definido no formato JSON da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d2805-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="d2805-137">Olá, a tabela a seguir descreve as propriedades no hello acima JSON:</span><span class="sxs-lookup"><span data-stu-id="d2805-137">hello following table describes properties in hello above JSON:</span></span>   

| <span data-ttu-id="d2805-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d2805-138">Property</span></span> | <span data-ttu-id="d2805-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="d2805-139">Description</span></span> | <span data-ttu-id="d2805-140">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d2805-140">Required</span></span> | <span data-ttu-id="d2805-141">Padrão</span><span class="sxs-lookup"><span data-stu-id="d2805-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d2805-142">name</span><span class="sxs-lookup"><span data-stu-id="d2805-142">name</span></span> |<span data-ttu-id="d2805-143">Nome do conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-143">Name of hello dataset.</span></span> <span data-ttu-id="d2805-144">Confira [Azure Data Factory - Regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="d2805-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="d2805-145">Sim</span><span class="sxs-lookup"><span data-stu-id="d2805-145">Yes</span></span> |<span data-ttu-id="d2805-146">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-146">NA</span></span> |
| <span data-ttu-id="d2805-147">type</span><span class="sxs-lookup"><span data-stu-id="d2805-147">type</span></span> |<span data-ttu-id="d2805-148">Tipo de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-148">Type of hello dataset.</span></span> <span data-ttu-id="d2805-149">Especifique um dos tipos de saudação com suporte pela fábrica de dados (por exemplo: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="d2805-149">Specify one of hello types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="d2805-150">Para obter detalhes, consulte [Tipo de conjunto de dados](#Type).</span><span class="sxs-lookup"><span data-stu-id="d2805-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="d2805-151">Sim</span><span class="sxs-lookup"><span data-stu-id="d2805-151">Yes</span></span> |<span data-ttu-id="d2805-152">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-152">NA</span></span> |
| <span data-ttu-id="d2805-153">estrutura</span><span class="sxs-lookup"><span data-stu-id="d2805-153">structure</span></span> |<span data-ttu-id="d2805-154">Esquema de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-154">Schema of hello dataset.</span></span><br/><br/><span data-ttu-id="d2805-155">Para obter detalhes, consulte [Estrutura de conjunto de dados](#Structure).</span><span class="sxs-lookup"><span data-stu-id="d2805-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="d2805-156">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-156">No</span></span> |<span data-ttu-id="d2805-157">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-157">NA</span></span> |
| <span data-ttu-id="d2805-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="d2805-158">typeProperties</span></span> | <span data-ttu-id="d2805-159">Propriedades do tipo Hello são diferentes para cada tipo (por exemplo: Blob do Azure, tabela do SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="d2805-159">hello type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="d2805-160">Para obter detalhes sobre os tipos de saudação com suporte e suas propriedades, consulte [tipo de conjunto de dados](#Type).</span><span class="sxs-lookup"><span data-stu-id="d2805-160">For details on hello supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="d2805-161">Sim</span><span class="sxs-lookup"><span data-stu-id="d2805-161">Yes</span></span> |<span data-ttu-id="d2805-162">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-162">NA</span></span> |
| <span data-ttu-id="d2805-163">externo</span><span class="sxs-lookup"><span data-stu-id="d2805-163">external</span></span> | <span data-ttu-id="d2805-164">Booliano sinalizador toospecify se um conjunto de dados explicitamente produzido por um pipeline da fábrica de dados ou não.</span><span class="sxs-lookup"><span data-stu-id="d2805-164">Boolean flag toospecify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="d2805-165">Se o conjunto de dados de entrada de saudação para uma atividade não é produzido pelo pipeline atual Olá, defina esse sinalizador tootrue.</span><span class="sxs-lookup"><span data-stu-id="d2805-165">If hello input dataset for an activity is not produced by hello current pipeline, set this flag tootrue.</span></span> <span data-ttu-id="d2805-166">Defina tootrue este sinalizador de conjunto de dados entrada da atividade primeiro Olá Olá no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-166">Set this flag tootrue for hello input dataset of hello first activity in hello pipeline.</span></span>  |<span data-ttu-id="d2805-167">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-167">No</span></span> |<span data-ttu-id="d2805-168">false</span><span class="sxs-lookup"><span data-stu-id="d2805-168">false</span></span> |
| <span data-ttu-id="d2805-169">disponibilidade</span><span class="sxs-lookup"><span data-stu-id="d2805-169">availability</span></span> | <span data-ttu-id="d2805-170">Define Olá janela de processamento (por exemplo, por hora ou diariamente) ou hello dividindo o modelo para conjunto de dados de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="d2805-170">Defines hello processing window (for example, hourly or daily) or hello slicing model for hello dataset production.</span></span> <span data-ttu-id="d2805-171">Cada unidade de dados consumida e produzida por uma execução de atividade é chamada de uma fatia de dados.</span><span class="sxs-lookup"><span data-stu-id="d2805-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="d2805-172">Se a disponibilidade de saudação de um conjunto de dados de saída for conjunto toodaily (frequência - dia, o intervalo de-1), uma fatia é produzida diariamente.</span><span class="sxs-lookup"><span data-stu-id="d2805-172">If hello availability of an output dataset is set toodaily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="d2805-173">Para obter detalhes, consulte [Disponibilidade do conjunto de dados](#Availability).</span><span class="sxs-lookup"><span data-stu-id="d2805-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="d2805-174">Para obter detalhes sobre o conjunto de dados Olá dividindo o modelo, consulte Olá [de agendamento e execução](data-factory-scheduling-and-execution.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="d2805-174">For details on hello dataset slicing model, see hello [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="d2805-175">Sim</span><span class="sxs-lookup"><span data-stu-id="d2805-175">Yes</span></span> |<span data-ttu-id="d2805-176">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-176">NA</span></span> |
| <span data-ttu-id="d2805-177">policy</span><span class="sxs-lookup"><span data-stu-id="d2805-177">policy</span></span> |<span data-ttu-id="d2805-178">Define os critérios de saudação ou condição Olá que devem ser atendidos por fatias de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-178">Defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="d2805-179">Para obter detalhes, consulte Olá [política de conjunto de dados](#Policy) seção.</span><span class="sxs-lookup"><span data-stu-id="d2805-179">For details, see hello [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="d2805-180">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-180">No</span></span> |<span data-ttu-id="d2805-181">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="d2805-182">Exemplo de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="d2805-182">Dataset example</span></span>
<span data-ttu-id="d2805-183">Olá exemplo a seguir, Olá dataset representa uma tabela chamada **MyTable** em um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d2805-183">In hello following example, hello dataset represents a table named **MyTable** in a SQL database.</span></span>

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="d2805-184">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2805-184">Note hello following points:</span></span>

* <span data-ttu-id="d2805-185">**tipo** é definido tooAzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="d2805-185">**type** is set tooAzureSqlTable.</span></span>
* <span data-ttu-id="d2805-186">**tableName** propriedade type (tipo de específico tooAzureSqlTable) é definida tooMyTable.</span><span class="sxs-lookup"><span data-stu-id="d2805-186">**tableName** type property (specific tooAzureSqlTable type) is set tooMyTable.</span></span>
* <span data-ttu-id="d2805-187">**linkedServiceName** refere-se o serviço de tooa vinculado do tipo AzureSqlDatabase, que é definido no seguinte trecho JSON a saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-187">**linkedServiceName** refers tooa linked service of type AzureSqlDatabase, which is defined in hello next JSON snippet.</span></span> 
* <span data-ttu-id="d2805-188">**frequência de disponibilidade** é definido como tooDay, e **intervalo** é definido too1.</span><span class="sxs-lookup"><span data-stu-id="d2805-188">**availability frequency** is set tooDay, and **interval** is set too1.</span></span> <span data-ttu-id="d2805-189">Isso significa que essa fatia do conjunto de dados de saudação é produzida diariamente.</span><span class="sxs-lookup"><span data-stu-id="d2805-189">This means that hello dataset slice is produced daily.</span></span>  

<span data-ttu-id="d2805-190">**AzureSqlLinkedService** é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d2805-190">**AzureSqlLinkedService** is defined as follows:</span></span>

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

<span data-ttu-id="d2805-191">Em Olá precede o trecho JSON:</span><span class="sxs-lookup"><span data-stu-id="d2805-191">In hello preceding JSON snippet:</span></span>

* <span data-ttu-id="d2805-192">**tipo** é definido tooAzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="d2805-192">**type** is set tooAzureSqlDatabase.</span></span>
* <span data-ttu-id="d2805-193">**connectionString** propriedade de tipo Especifica o banco de dados SQL tooa de tooconnect de informações.</span><span class="sxs-lookup"><span data-stu-id="d2805-193">**connectionString** type property specifies information tooconnect tooa SQL database.</span></span>  

<span data-ttu-id="d2805-194">Como você pode ver, hello serviço vinculado define como banco de dados do SQL tooconnect tooa.</span><span class="sxs-lookup"><span data-stu-id="d2805-194">As you can see, hello linked service defines how tooconnect tooa SQL database.</span></span> <span data-ttu-id="d2805-195">saudação de conjunto de dados define qual tabela é usada como uma entrada e saída para a atividade de saudação em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="d2805-195">hello dataset defines what table is used as an input and output for hello activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="d2805-196">A menos que um conjunto de dados é produzido pelo pipeline hello, ele deve ser marcado como **externo**.</span><span class="sxs-lookup"><span data-stu-id="d2805-196">Unless a dataset is being produced by hello pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="d2805-197">Essa configuração geralmente se aplica a tooinputs da primeira atividade em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="d2805-197">This setting generally applies tooinputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="d2805-198"><a name="Type"></a> Tipo de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="d2805-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="d2805-199">tipo de saudação do conjunto de dados Olá depende de repositório de dados Olá que você usar.</span><span class="sxs-lookup"><span data-stu-id="d2805-199">hello type of hello dataset depends on hello data store you use.</span></span> <span data-ttu-id="d2805-200">Consulte Olá para obter uma lista de repositórios de dados com suporte pela fábrica de dados a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="d2805-200">See hello following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="d2805-201">Clique em um toolearn de repositório de dados como toocreate um serviço vinculado e um conjunto de dados para os dados armazenam.</span><span class="sxs-lookup"><span data-stu-id="d2805-201">Click a data store toolearn how toocreate a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="d2805-202">Armazenamentos de dados com * podem ser locais ou IaaS (infraestrutura como serviço) do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2805-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="d2805-203">Esses armazenamentos de dados exigem tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="d2805-203">These data stores require you tooinstall [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="d2805-204">No exemplo hello na seção anterior hello, tipo de saudação do conjunto de dados de saudação é definido muito**AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="d2805-204">In hello example in hello previous section, hello type of hello dataset is set too**AzureSqlTable**.</span></span> <span data-ttu-id="d2805-205">Da mesma forma, para um conjunto de dados de Blob do Azure, Olá tipo do conjunto de dados de saudação é definido muito**AzureBlob**, conforme mostrado no hello JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2805-205">Similarly, for an Azure Blob dataset, hello type of hello dataset is set too**AzureBlob**, as shown in hello following JSON:</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

## <span data-ttu-id="d2805-206"><a name="Structure"></a>Estrutura do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="d2805-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="d2805-207">Olá **estrutura** seção é opcional.</span><span class="sxs-lookup"><span data-stu-id="d2805-207">hello **structure** section is optional.</span></span> <span data-ttu-id="d2805-208">Ele define o esquema de Olá do conjunto de dados Olá, que contém uma coleção de nomes e tipos de dados das colunas.</span><span class="sxs-lookup"><span data-stu-id="d2805-208">It defines hello schema of hello dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="d2805-209">Você usar Olá estrutura seção tooprovide informações de tipo é usado tooconvert tipos e mapear colunas de destino de toohello Olá fonte.</span><span class="sxs-lookup"><span data-stu-id="d2805-209">You use hello structure section tooprovide type information that is used tooconvert types and map columns from hello source toohello destination.</span></span> <span data-ttu-id="d2805-210">Olá exemplo a seguir, Olá dataset tem três colunas: `slicetimestamp`, `projectname`, e `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="d2805-210">In hello following example, hello dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="d2805-211">Elas são do tipo String, String e Decimal, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="d2805-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="d2805-212">Cada coluna na estrutura de saudação contém Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2805-212">Each column in hello structure contains hello following properties:</span></span>

| <span data-ttu-id="d2805-213">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d2805-213">Property</span></span> | <span data-ttu-id="d2805-214">Descrição</span><span class="sxs-lookup"><span data-stu-id="d2805-214">Description</span></span> | <span data-ttu-id="d2805-215">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d2805-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d2805-216">name</span><span class="sxs-lookup"><span data-stu-id="d2805-216">name</span></span> |<span data-ttu-id="d2805-217">Nome da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-217">Name of hello column.</span></span> |<span data-ttu-id="d2805-218">Sim</span><span class="sxs-lookup"><span data-stu-id="d2805-218">Yes</span></span> |
| <span data-ttu-id="d2805-219">type</span><span class="sxs-lookup"><span data-stu-id="d2805-219">type</span></span> |<span data-ttu-id="d2805-220">Tipo de dados da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-220">Data type of hello column.</span></span>  |<span data-ttu-id="d2805-221">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-221">No</span></span> |
| <span data-ttu-id="d2805-222">culture</span><span class="sxs-lookup"><span data-stu-id="d2805-222">culture</span></span> |<span data-ttu-id="d2805-223">. Toobe cultura baseada em rede usada quando a saudação é um tipo .NET: `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="d2805-223">.NET-based culture toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="d2805-224">saudação padrão é `en-us`.</span><span class="sxs-lookup"><span data-stu-id="d2805-224">hello default is `en-us`.</span></span> |<span data-ttu-id="d2805-225">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-225">No</span></span> |
| <span data-ttu-id="d2805-226">formato</span><span class="sxs-lookup"><span data-stu-id="d2805-226">format</span></span> |<span data-ttu-id="d2805-227">Formatar toobe de cadeia de caracteres usada quando Olá é um tipo .NET: `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="d2805-227">Format string toobe used when hello type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="d2805-228">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-228">No</span></span> |

<span data-ttu-id="d2805-229">Olá diretrizes a seguir ajudarão a determinar quando tooinclude estrutura informações e quais tooinclude em Olá **estrutura** seção.</span><span class="sxs-lookup"><span data-stu-id="d2805-229">hello following guidelines help you determine when tooinclude structure information, and what tooinclude in hello **structure** section.</span></span>

* <span data-ttu-id="d2805-230">**Para fontes de dados estruturados**, especifique a seção de estrutura de saudação somente se você deseja mapear colunas de toosink de colunas de origem e seus nomes não são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="d2805-230">**For structured data sources**, specify hello structure section only if you want map source columns toosink columns, and their names are not hello same.</span></span> <span data-ttu-id="d2805-231">Esse tipo de fonte de dados estruturados armazena informações de esquema e o tipo de dados junto com dados de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="d2805-231">This kind of structured data source stores data schema and type information along with hello data itself.</span></span> <span data-ttu-id="d2805-232">Exemplos de fontes de dados estruturadas incluem SQL Server, Oracle e tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2805-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="d2805-233">Como informações de tipo já estão disponíveis para fontes de dados estruturados, você não deve incluir informações de tipo quando você inclui uma seção de estrutura de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-233">As type information is already available for structured data sources, you should not include type information when you do include hello structure section.</span></span>
* <span data-ttu-id="d2805-234">**Para o esquema de fontes de dados de leitura (especificamente o armazenamento de Blob)**, você pode escolher dados toostore sem armazenar qualquer informação de tipo ou esquema com dados saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-234">**For schema on read data sources (specifically Blob storage)**, you can choose toostore data without storing any schema or type information with hello data.</span></span> <span data-ttu-id="d2805-235">Para esses tipos de fontes de dados, inclua estrutura quando você desejar toomap fonte colunas toosink colunas.</span><span class="sxs-lookup"><span data-stu-id="d2805-235">For these types of data sources, include structure when you want toomap source columns toosink columns.</span></span> <span data-ttu-id="d2805-236">Também incluem estrutura quando Olá conjunto de dados é uma entrada para uma atividade de cópia e tipos de dados do conjunto de dados de origem devem ser tipos toonative convertido para o coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-236">Also include structure when hello dataset is an input for a copy activity, and data types of source dataset should be converted toonative types for hello sink.</span></span> 
    
    <span data-ttu-id="d2805-237">Fábrica de dados oferece suporte a saudação valores para fornecer informações de tipo na estrutura a seguir: **Int16, Int32, Int64, único, Double, Decimal, Byte [], booliano, cadeia de caracteres, Guid, Datetime, Datetimeoffset e Timespan**.</span><span class="sxs-lookup"><span data-stu-id="d2805-237">Data Factory supports hello following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="d2805-238">Esses valores são valores de tipo baseados em NET e em conformidade com CLS (Common Language Specification).</span><span class="sxs-lookup"><span data-stu-id="d2805-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="d2805-239">Fábrica de dados executa automaticamente conversões de tipo ao mover o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d2805-239">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="d2805-240">Disponibilidade do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="d2805-240">Dataset availability</span></span>
<span data-ttu-id="d2805-241">Olá **disponibilidade** seção em um conjunto de dados define Olá janela de processamento (por exemplo, por hora, diariamente ou semanalmente) para o conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-241">hello **availability** section in a dataset defines hello processing window (for example, hourly, daily, or weekly) for hello dataset.</span></span> <span data-ttu-id="d2805-242">Para obter mais informações sobre janelas de atividades, consulte [Agendamento e execução](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="d2805-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="d2805-243">Olá seção de disponibilidade a seguir especifica que hello conjunto de dados de saída ou produzido por hora, ou conjunto de dados de entrada hello está disponível por hora:</span><span class="sxs-lookup"><span data-stu-id="d2805-243">hello following availability section specifies that hello output dataset is either produced hourly, or hello input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="d2805-244">Se pipeline Olá Olá horas inicial e final a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2805-244">If hello pipeline has hello following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="d2805-245">Olá conjunto de dados de saída é produzido por hora no pipeline de saudação início e término.</span><span class="sxs-lookup"><span data-stu-id="d2805-245">hello output dataset is produced hourly within hello pipeline start and end times.</span></span> <span data-ttu-id="d2805-246">Portanto, cinco fatias de conjunto de dados são geradas por esse pipeline, uma para cada janela de atividades (00h à 1h, 1h às 2h, 2h às 3h, 3h às 4h e 4h às 5h).</span><span class="sxs-lookup"><span data-stu-id="d2805-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="d2805-247">Olá tabela a seguir descreve propriedades que você pode usar na seção de disponibilidade hello:</span><span class="sxs-lookup"><span data-stu-id="d2805-247">hello following table describes properties you can use in hello availability section:</span></span>

| <span data-ttu-id="d2805-248">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d2805-248">Property</span></span> | <span data-ttu-id="d2805-249">Descrição</span><span class="sxs-lookup"><span data-stu-id="d2805-249">Description</span></span> | <span data-ttu-id="d2805-250">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d2805-250">Required</span></span> | <span data-ttu-id="d2805-251">Padrão</span><span class="sxs-lookup"><span data-stu-id="d2805-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d2805-252">frequência</span><span class="sxs-lookup"><span data-stu-id="d2805-252">frequency</span></span> |<span data-ttu-id="d2805-253">Especifica a unidade de tempo de saudação de produção de fatia do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="d2805-253">Specifies hello time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="d2805-254"><b>Frequência com suporte</b>: Minuto, Hora, Dia, Semana, Mês</span><span class="sxs-lookup"><span data-stu-id="d2805-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="d2805-255">Sim</span><span class="sxs-lookup"><span data-stu-id="d2805-255">Yes</span></span> |<span data-ttu-id="d2805-256">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-256">NA</span></span> |
| <span data-ttu-id="d2805-257">intervalo</span><span class="sxs-lookup"><span data-stu-id="d2805-257">interval</span></span> |<span data-ttu-id="d2805-258">Especifica um multiplicador para a frequência.</span><span class="sxs-lookup"><span data-stu-id="d2805-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="d2805-259">"Intervalo de frequência x" determina com que frequência hello fatia é produzida.</span><span class="sxs-lookup"><span data-stu-id="d2805-259">"Frequency x interval" determines how often hello slice is produced.</span></span> <span data-ttu-id="d2805-260">Por exemplo, se você precisar hello toobe de conjunto de dados dividido por hora, definir <b>frequência</b> muito<b>hora</b>, e <b>intervalo</b> muito<b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="d2805-260">For example, if you need hello dataset toobe sliced on an hourly basis, you set <b>frequency</b> too<b>Hour</b>, and <b>interval</b> too<b>1</b>.</span></span><br/><br/><span data-ttu-id="d2805-261">Observe que, se você especificar **frequência** como **minuto**, você deve definir Olá intervalo toono menos de 15.</span><span class="sxs-lookup"><span data-stu-id="d2805-261">Note that if you specify **frequency** as **Minute**, you should set hello interval toono less than 15.</span></span> |<span data-ttu-id="d2805-262">Sim</span><span class="sxs-lookup"><span data-stu-id="d2805-262">Yes</span></span> |<span data-ttu-id="d2805-263">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-263">NA</span></span> |
| <span data-ttu-id="d2805-264">estilo</span><span class="sxs-lookup"><span data-stu-id="d2805-264">style</span></span> |<span data-ttu-id="d2805-265">Especifica se a fatia Olá deve ser produzida no início de saudação ou no final do intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-265">Specifies whether hello slice should be produced at hello start or end of hello interval.</span></span><ul><li><span data-ttu-id="d2805-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="d2805-266">StartOfInterval</span></span></li><li><span data-ttu-id="d2805-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="d2805-267">EndOfInterval</span></span></li></ul><span data-ttu-id="d2805-268">Se **frequência** está definido muito**mês**, e **estilo** está definido muito**EndOfInterval**, Olá fatia é produzida no último dia do mês de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-268">If **frequency** is set too**Month**, and **style** is set too**EndOfInterval**, hello slice is produced on hello last day of month.</span></span> <span data-ttu-id="d2805-269">Se **estilo** está definido muito**StartOfInterval**, fatia de saudação é produzida no hello primeiro dia do mês.</span><span class="sxs-lookup"><span data-stu-id="d2805-269">If **style** is set too**StartOfInterval**, hello slice is produced on hello first day of month.</span></span><br/><br/><span data-ttu-id="d2805-270">Se **frequência** está definido muito**dia**, e **estilo** está definido muito**EndOfInterval**, Olá fatia é produzida no hello última hora do dia de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-270">If **frequency** is set too**Day**, and **style** is set too**EndOfInterval**, hello slice is produced in hello last hour of hello day.</span></span><br/><br/><span data-ttu-id="d2805-271">Se **frequência** está definido muito**hora**, e **estilo** está definido muito**EndOfInterval**, Olá fatia é produzida no final de saudação de hora hello.</span><span class="sxs-lookup"><span data-stu-id="d2805-271">If **frequency** is set too**Hour**, and **style** is set too**EndOfInterval**, hello slice is produced at hello end of hello hour.</span></span> <span data-ttu-id="d2805-272">Por exemplo, para uma fatia para Olá PM 1-2 PM período, a fatia de saudação é produzida às 14: 00.</span><span class="sxs-lookup"><span data-stu-id="d2805-272">For example, for a slice for hello 1 PM - 2 PM period, hello slice is produced at 2 PM.</span></span> |<span data-ttu-id="d2805-273">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-273">No</span></span> |<span data-ttu-id="d2805-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="d2805-274">EndOfInterval</span></span> |
| <span data-ttu-id="d2805-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="d2805-275">anchorDateTime</span></span> |<span data-ttu-id="d2805-276">Define a posição absoluta Olá no tempo usado pelos limites de fatia Olá Agendador toocompute conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="d2805-276">Defines hello absolute position in time used by hello scheduler toocompute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="d2805-277">Observe que se este propoerty tem partes de data mais granulares de saudação especificado frequência, Olá partes mais granulares são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="d2805-277">Note that if this propoerty has date parts that are more granular than hello specified frequency, hello more granular parts are ignored.</span></span> <span data-ttu-id="d2805-278">Por exemplo, se hello **intervalo** é **por hora** (frequência: hora e intervalo: 1) e hello **anchorDateTime** contém **minutos e segundos**, Olá, em seguida, partes de minutos e segundos **anchorDateTime** são ignorados.</span><span class="sxs-lookup"><span data-stu-id="d2805-278">For example, if hello **interval** is **hourly** (frequency: hour and interval: 1), and hello **anchorDateTime** contains **minutes and seconds**, then hello minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="d2805-279">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-279">No</span></span> |<span data-ttu-id="d2805-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="d2805-280">01/01/0001</span></span> |
| <span data-ttu-id="d2805-281">deslocamento</span><span class="sxs-lookup"><span data-stu-id="d2805-281">offset</span></span> |<span data-ttu-id="d2805-282">O intervalo de tempo pelo qual saudação inicial e final de todas as fatias de conjunto de dados são transferidos.</span><span class="sxs-lookup"><span data-stu-id="d2805-282">Timespan by which hello start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="d2805-283">Observe que, se ambos os **anchorDateTime** e **deslocamento** forem especificados, resultado de saudação é shift Olá combinado.</span><span class="sxs-lookup"><span data-stu-id="d2805-283">Note that if both **anchorDateTime** and **offset** are specified, hello result is hello combined shift.</span></span> |<span data-ttu-id="d2805-284">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-284">No</span></span> |<span data-ttu-id="d2805-285">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="d2805-286">exemplo de deslocamento</span><span class="sxs-lookup"><span data-stu-id="d2805-286">offset example</span></span>
<span data-ttu-id="d2805-287">Por padrão, as fatias diárias (`"frequency": "Day", "interval": 1`) começam às 00h (meia-noite) em UTC (Tempo Universal Coordenado).</span><span class="sxs-lookup"><span data-stu-id="d2805-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="d2805-288">Se deseja saudação inicial tempo toobe 6 horas UTC em vez disso, defina Olá deslocamento conforme Olá trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2805-288">If you want hello start time toobe 6 AM UTC time instead, set hello offset as shown in hello following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="d2805-289">Exemplo de anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="d2805-289">anchorDateTime example</span></span>
<span data-ttu-id="d2805-290">No hello exemplo a seguir, Olá dataset é produzido cada 23 horas.</span><span class="sxs-lookup"><span data-stu-id="d2805-290">In hello following example, hello dataset is produced once every 23 hours.</span></span> <span data-ttu-id="d2805-291">Hello primeira fatia começa no tempo de saudação especificado por **anchorDateTime**, que está definido muito`2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="d2805-291">hello first slice starts at hello time specified by **anchorDateTime**, which is set too`2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="d2805-292">exemplo de deslocamento/estilo</span><span class="sxs-lookup"><span data-stu-id="d2805-292">offset/style example</span></span>
<span data-ttu-id="d2805-293">Olá seguinte conjunto de dados é mensal e é gerada em Olá 3º de cada mês às 8:00 (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="d2805-293">hello following dataset is monthly, and is produced on hello 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="d2805-294"><a name="Policy"></a>Política de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="d2805-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="d2805-295">Olá **política** seção na definição de conjunto de dados de saudação define os critérios de saudação ou condição Olá Olá fatias de conjunto de dados deve ser atendidos.</span><span class="sxs-lookup"><span data-stu-id="d2805-295">hello **policy** section in hello dataset definition defines hello criteria or hello condition that hello dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="d2805-296">Políticas de validação</span><span class="sxs-lookup"><span data-stu-id="d2805-296">Validation policies</span></span>
| <span data-ttu-id="d2805-297">Nome da política</span><span class="sxs-lookup"><span data-stu-id="d2805-297">Policy name</span></span> | <span data-ttu-id="d2805-298">Descrição</span><span class="sxs-lookup"><span data-stu-id="d2805-298">Description</span></span> | <span data-ttu-id="d2805-299">Aplicado muito</span><span class="sxs-lookup"><span data-stu-id="d2805-299">Applied too</span></span>| <span data-ttu-id="d2805-300">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d2805-300">Required</span></span> | <span data-ttu-id="d2805-301">Padrão</span><span class="sxs-lookup"><span data-stu-id="d2805-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="d2805-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="d2805-302">minimumSizeMB</span></span> |<span data-ttu-id="d2805-303">Valida que dados Olá em **armazenamento de BLOBs do Azure** Olá de atende aos requisitos de tamanho mínimo (em megabytes).</span><span class="sxs-lookup"><span data-stu-id="d2805-303">Validates that hello data in **Azure Blob storage** meets hello minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="d2805-304">Armazenamento do Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="d2805-304">Azure Blob storage</span></span> |<span data-ttu-id="d2805-305">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-305">No</span></span> |<span data-ttu-id="d2805-306">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-306">NA</span></span> |
| <span data-ttu-id="d2805-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="d2805-307">minimumRows</span></span> |<span data-ttu-id="d2805-308">Valida que dados Olá em um **banco de dados do SQL Azure** ou um **tabela do Azure** contém o número mínimo de saudação de linhas.</span><span class="sxs-lookup"><span data-stu-id="d2805-308">Validates that hello data in an **Azure SQL database** or an **Azure table** contains hello minimum number of rows.</span></span> |<ul><li><span data-ttu-id="d2805-309">Banco de Dados SQL Azure</span><span class="sxs-lookup"><span data-stu-id="d2805-309">Azure SQL database</span></span></li><li><span data-ttu-id="d2805-310">Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="d2805-310">Azure table</span></span></li></ul> |<span data-ttu-id="d2805-311">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-311">No</span></span> |<span data-ttu-id="d2805-312">ND</span><span class="sxs-lookup"><span data-stu-id="d2805-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="d2805-313">Exemplos</span><span class="sxs-lookup"><span data-stu-id="d2805-313">Examples</span></span>
<span data-ttu-id="d2805-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="d2805-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="d2805-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="d2805-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="d2805-316">Conjuntos de dados externos</span><span class="sxs-lookup"><span data-stu-id="d2805-316">External datasets</span></span>
<span data-ttu-id="d2805-317">Conjuntos de dados externos são Olá aqueles que não são produzidos por um pipeline em execução na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="d2805-317">External datasets are hello ones that are not produced by a running pipeline in hello data factory.</span></span> <span data-ttu-id="d2805-318">Se Olá conjunto de dados está marcado como **externo**, Olá **ExternalData** política pode ser definido tooinfluence Olá comportamento de disponibilidade de fatia do conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-318">If hello dataset is marked as **external**, hello **ExternalData** policy may be defined tooinfluence hello behavior of hello dataset slice availability.</span></span>

<span data-ttu-id="d2805-319">A menos que um conjunto de dados seja gerado pelo Data Factory, ele deverá ser marcado como **externo**.</span><span class="sxs-lookup"><span data-stu-id="d2805-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="d2805-320">Essa configuração geralmente se aplica a entradas toohello da primeira atividade em um pipeline, a menos que a atividade ou o encadeamento de pipeline está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="d2805-320">This setting generally applies toohello inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="d2805-321">Nome</span><span class="sxs-lookup"><span data-stu-id="d2805-321">Name</span></span> | <span data-ttu-id="d2805-322">Descrição</span><span class="sxs-lookup"><span data-stu-id="d2805-322">Description</span></span> | <span data-ttu-id="d2805-323">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d2805-323">Required</span></span> | <span data-ttu-id="d2805-324">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="d2805-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d2805-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="d2805-325">dataDelay</span></span> |<span data-ttu-id="d2805-326">tempo de Olá Olá toodelay Verificar disponibilidade de saudação de dados externa Olá Olá fornecido fatia.</span><span class="sxs-lookup"><span data-stu-id="d2805-326">hello time toodelay hello check on hello availability of hello external data for hello given slice.</span></span> <span data-ttu-id="d2805-327">Por exemplo, é possível atrasar uma verificação por hora usando essa configuração.</span><span class="sxs-lookup"><span data-stu-id="d2805-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="d2805-328">Olá configuração se aplica somente toohello a hora atual.</span><span class="sxs-lookup"><span data-stu-id="d2805-328">hello setting only applies toohello present time.</span></span>  <span data-ttu-id="d2805-329">Por exemplo, se for 1:00 PM agora e esse valor é 10 minutos, validação Olá inicia às 13:10.</span><span class="sxs-lookup"><span data-stu-id="d2805-329">For example, if it is 1:00 PM right now and this value is 10 minutes, hello validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="d2805-330">Observe que essa configuração não afeta fatias Olá anterior.</span><span class="sxs-lookup"><span data-stu-id="d2805-330">Note that this setting does not affect slices in hello past.</span></span> <span data-ttu-id="d2805-331">Fatias com **Hora de Término da Fatia** + **dataDelay** < **Agora** são processadas sem atrasos.</span><span class="sxs-lookup"><span data-stu-id="d2805-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="d2805-332">Vezes maior que 23:59 horas devem ser especificadas usando Olá `day.hours:minutes:seconds` formato.</span><span class="sxs-lookup"><span data-stu-id="d2805-332">Times greater than 23:59 hours should be specified by using hello `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="d2805-333">Por exemplo, toospecify 24 horas, não use 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="d2805-333">For example, toospecify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="d2805-334">Em vez disso, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="d2805-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="d2805-335">Se você usar 24:00:00, isso será tratado como 24 dias (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="d2805-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="d2805-336">Para 1 dia e 4 horas, especifique 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="d2805-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="d2805-337">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-337">No</span></span> |<span data-ttu-id="d2805-338">0</span><span class="sxs-lookup"><span data-stu-id="d2805-338">0</span></span> |
| <span data-ttu-id="d2805-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="d2805-339">retryInterval</span></span> |<span data-ttu-id="d2805-340">tempo de espera de saudação entre uma próxima tentativa falha e hello.</span><span class="sxs-lookup"><span data-stu-id="d2805-340">hello wait time between a failure and hello next attempt.</span></span> <span data-ttu-id="d2805-341">Essa configuração se aplica a toopresent tempo.</span><span class="sxs-lookup"><span data-stu-id="d2805-341">This setting applies toopresent time.</span></span> <span data-ttu-id="d2805-342">Se a tentativa anterior de saudação falha, próxima tentativa de saudação é após Olá **retryInterval** período.</span><span class="sxs-lookup"><span data-stu-id="d2805-342">If hello previous try failed, hello next try is after hello **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="d2805-343">Se for 1:00 PM agora, começamos Olá primeira tentativa.</span><span class="sxs-lookup"><span data-stu-id="d2805-343">If it is 1:00 PM right now, we begin hello first try.</span></span> <span data-ttu-id="d2805-344">Se Olá duração toocomplete Olá primeira verificação de validação é 1 minuto e Falha na operação de hello, Olá próxima tentativa é às 1:00 + 1 min (duração) + 1min (intervalo de repetição) = 1:02 PM.</span><span class="sxs-lookup"><span data-stu-id="d2805-344">If hello duration toocomplete hello first validation check is 1 minute and hello operation failed, hello next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="d2805-345">Para fatias Olá anterior, não há nenhum atraso.</span><span class="sxs-lookup"><span data-stu-id="d2805-345">For slices in hello past, there is no delay.</span></span> <span data-ttu-id="d2805-346">repetição de saudação ocorre imediatamente.</span><span class="sxs-lookup"><span data-stu-id="d2805-346">hello retry happens immediately.</span></span> |<span data-ttu-id="d2805-347">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-347">No</span></span> |<span data-ttu-id="d2805-348">00:01:00 (1 minuto)</span><span class="sxs-lookup"><span data-stu-id="d2805-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="d2805-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="d2805-349">retryTimeout</span></span> |<span data-ttu-id="d2805-350">Olá tempo limite para cada tentativa de repetição.</span><span class="sxs-lookup"><span data-stu-id="d2805-350">hello timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="d2805-351">Se essa propriedade for definida too10 minutos, validação Olá deve ser concluída em 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="d2805-351">If this property is set too10 minutes, hello validation should be completed within 10 minutes.</span></span> <span data-ttu-id="d2805-352">Se demorar mais de validação de saudação do tooperform de 10 minutos, Olá novamente o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="d2805-352">If it takes longer than 10 minutes tooperform hello validation, hello retry times out.</span></span><br/><br/><span data-ttu-id="d2805-353">Se todas as tentativas de saudação validação tempo limite, Olá fatia é marcada como **TimedOut**.</span><span class="sxs-lookup"><span data-stu-id="d2805-353">If all attempts for hello validation time out, hello slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="d2805-354">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-354">No</span></span> |<span data-ttu-id="d2805-355">00:10:00 (10 minutos)</span><span class="sxs-lookup"><span data-stu-id="d2805-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="d2805-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="d2805-356">maximumRetry</span></span> |<span data-ttu-id="d2805-357">Olá número de vezes toocheck para disponibilidade de saudação de dados externos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-357">hello number of times toocheck for hello availability of hello external data.</span></span> <span data-ttu-id="d2805-358">Olá valor máximo permitido é 10.</span><span class="sxs-lookup"><span data-stu-id="d2805-358">hello maximum allowed value is 10.</span></span> |<span data-ttu-id="d2805-359">Não</span><span class="sxs-lookup"><span data-stu-id="d2805-359">No</span></span> |<span data-ttu-id="d2805-360">3</span><span class="sxs-lookup"><span data-stu-id="d2805-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="d2805-361">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="d2805-361">Create datasets</span></span>
<span data-ttu-id="d2805-362">Você pode criar conjuntos de dados usando uma destas ferramentas ou SDKs:</span><span class="sxs-lookup"><span data-stu-id="d2805-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="d2805-363">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="d2805-363">Copy Wizard</span></span> 
- <span data-ttu-id="d2805-364">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2805-364">Azure portal</span></span>
- <span data-ttu-id="d2805-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2805-365">Visual Studio</span></span>
- <span data-ttu-id="d2805-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2805-366">PowerShell</span></span>
- <span data-ttu-id="d2805-367">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d2805-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="d2805-368">API REST</span><span class="sxs-lookup"><span data-stu-id="d2805-368">REST API</span></span>
- <span data-ttu-id="d2805-369">API do .NET</span><span class="sxs-lookup"><span data-stu-id="d2805-369">.NET API</span></span>

<span data-ttu-id="d2805-370">Consulte Olá tutoriais para obter instruções passo a passo para criar pipelines e conjuntos de dados usando uma dessas ferramentas ou SDKs a seguir:</span><span class="sxs-lookup"><span data-stu-id="d2805-370">See hello following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="d2805-371">Crie um pipeline com uma atividade de transformação de dados</span><span class="sxs-lookup"><span data-stu-id="d2805-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="d2805-372">Crie um pipeline com uma atividade de movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="d2805-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="d2805-373">Depois de um pipeline é criado e implantado, você pode gerenciar e monitorar seus pipelines usando Olá folhas portais do Azure ou um aplicativo de monitoramento e gerenciamento hello.</span><span class="sxs-lookup"><span data-stu-id="d2805-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using hello Azure portal blades, or hello Monitoring and Management app.</span></span> <span data-ttu-id="d2805-374">Consulte Olá seguintes tópicos para obter instruções passo a passo:</span><span class="sxs-lookup"><span data-stu-id="d2805-374">See hello following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="d2805-375">Monitorar e gerenciar pipelines usando as folhas do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2805-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="d2805-376">Monitorar e gerenciar pipelines usando o aplicativo de monitoramento e gerenciamento de saudação</span><span class="sxs-lookup"><span data-stu-id="d2805-376">Monitor and manage pipelines by using hello Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="d2805-377">Conjuntos de dados com escopo</span><span class="sxs-lookup"><span data-stu-id="d2805-377">Scoped datasets</span></span>
<span data-ttu-id="d2805-378">Você pode criar conjuntos de dados que estão no escopo tooa pipeline usando Olá **conjuntos de dados** propriedade.</span><span class="sxs-lookup"><span data-stu-id="d2805-378">You can create datasets that are scoped tooa pipeline by using hello **datasets** property.</span></span> <span data-ttu-id="d2805-379">Esses conjuntos de dados só podem ser usados por atividades dentro deste pipeline, não por atividades em outros pipelines.</span><span class="sxs-lookup"><span data-stu-id="d2805-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="d2805-380">saudação de exemplo a seguir define um pipeline com dois conjuntos de dados (rdc InputDataset e OutputDataset rdc) toobe usado no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="d2805-380">hello following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) toobe used within hello pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d2805-381">Conjuntos de dados no escopo são suportados apenas com pipelines única (onde **pipelineMode** está definido muito**OneTime**).</span><span class="sxs-lookup"><span data-stu-id="d2805-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set too**OneTime**).</span></span> <span data-ttu-id="d2805-382">Confira [Pipeline avulso](data-factory-create-pipelines.md#onetime-pipeline) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d2805-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d2805-383">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2805-383">Next steps</span></span>
- <span data-ttu-id="d2805-384">Para obter mais informações sobre pipelines, consulte [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="d2805-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="d2805-385">Para obter mais informações sobre como os pipelines são agendados e executados, consulte [Agendamento e execução no Azure Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="d2805-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
