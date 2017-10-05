---
title: Criar conjuntos de dados no Azure Data Factory | Microsoft Docs
description: Saiba como criar conjuntos de dados no Azure Data Factory, com exemplos que usam propriedades como offset e anchorDateTime.
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
ms.openlocfilehash: 6fd58edd830df8ea3f77a68e8dfcaf6de055b17c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="datasets-in-azure-data-factory"></a><span data-ttu-id="994f4-104">Conjuntos de dados no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="994f4-104">Datasets in Azure Data Factory</span></span>
<span data-ttu-id="994f4-105">Este artigo descreve o que são conjuntos de dados, como eles são definidos no formato JSON e como são usados em pipelines do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="994f4-105">This article describes what datasets are, how they are defined in JSON format, and how they are used in Azure Data Factory pipelines.</span></span> <span data-ttu-id="994f4-106">Ele fornece detalhes sobre cada seção (por exemplo, estrutura, disponibilidade e política) na definição de JSON do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-106">It provides details about each section (for example, structure, availability, and policy) in the dataset JSON definition.</span></span> <span data-ttu-id="994f4-107">O artigo também fornece exemplos de como usar as propriedades **offset**, **anchorDateTime** e **style** em uma definição de JSON do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-107">The article also provides examples for using the **offset**, **anchorDateTime**, and **style** properties in a dataset JSON definition.</span></span>

> [!NOTE]
> <span data-ttu-id="994f4-108">Se estiver conhecendo o Azure Data Factory agora, consulte [Introdução ao Azure Data Factory](data-factory-introduction.md) para obter uma visão geral.</span><span class="sxs-lookup"><span data-stu-id="994f4-108">If you are new to Data Factory, see [Introduction to Azure Data Factory](data-factory-introduction.md) for an overview.</span></span> <span data-ttu-id="994f4-109">Caso não tenha experiência prática com a criação de data factories, obtenha um melhor entendimento lendo o [tutorial de transformação de dados](data-factory-build-your-first-pipeline.md) e o [tutorial de movimentação de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="994f4-109">If you do not have hands-on experience with creating data factories, you can gain a better understanding by reading the [data transformation tutorial](data-factory-build-your-first-pipeline.md) and the [data movement tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

## <a name="overview"></a><span data-ttu-id="994f4-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="994f4-110">Overview</span></span>
<span data-ttu-id="994f4-111">Uma fábrica de dados pode ter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="994f4-111">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="994f4-112">Um **pipeline** é um agrupamento lógico de **atividades** que juntas executam uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="994f4-112">A **pipeline** is a logical grouping of **activities** that together perform a task.</span></span> <span data-ttu-id="994f4-113">As atividades em um pipeline definem ações para executar em seus dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-113">The activities in a pipeline define actions to perform on your data.</span></span> <span data-ttu-id="994f4-114">Por exemplo, você poderá usar uma atividade de cópia para copiar os dados de um SQL Server local para um armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="994f4-114">For example, you might use a copy activity to copy data from an on-premises SQL Server to Azure Blob storage.</span></span> <span data-ttu-id="994f4-115">Em seguida, poderá usar uma atividade do Hive que executa um script Hive em um cluster HDInsight do Azure a fim de processar dados do armazenamento de Blobs para gerar dados de saída.</span><span class="sxs-lookup"><span data-stu-id="994f4-115">Then, you might use a Hive activity that runs a Hive script on an Azure HDInsight cluster to process data from Blob storage to produce output data.</span></span> <span data-ttu-id="994f4-116">Por fim, poderá usar uma segunda atividade de cópia para copiar os dados de saída para o SQL Data Warehouse do Azure, no qual as soluções de relatório de BI (business intelligence) são criadas.</span><span class="sxs-lookup"><span data-stu-id="994f4-116">Finally, you might use a second copy activity to copy the output data to Azure SQL Data Warehouse, on top of which business intelligence (BI) reporting solutions are built.</span></span> <span data-ttu-id="994f4-117">Para obter mais informações sobre pipelines e atividades, consulte [Pipelines e atividades no Azure Data Factory](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="994f4-117">For more information about pipelines and activities, see [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md).</span></span>

<span data-ttu-id="994f4-118">Uma atividade pode usar zero ou mais **conjuntos de dados** de entrada e gerar um ou mais conjuntos de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="994f4-118">An activity can take zero or more input **datasets**, and produce one or more output datasets.</span></span> <span data-ttu-id="994f4-119">Um conjunto de dados de entrada representa a entrada de uma atividade no pipeline e um conjunto de dados de saída representa a saída da atividade.</span><span class="sxs-lookup"><span data-stu-id="994f4-119">An input dataset represents the input for an activity in the pipeline, and an output dataset represents the output for the activity.</span></span> <span data-ttu-id="994f4-120">Conjuntos de dados identificam dados em armazenamentos de dados diferentes, como tabelas, arquivos, pastas e documentos.</span><span class="sxs-lookup"><span data-stu-id="994f4-120">Datasets identify data within different data stores, such as tables, files, folders, and documents.</span></span> <span data-ttu-id="994f4-121">Por exemplo, um conjunto de dados de Blob do Azure especifica o contêiner de blobs e a pasta no armazenamento de Blobs dos quais o pipeline deve ler os dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-121">For example, an Azure Blob dataset specifies the blob container and folder in Blob storage from which the pipeline should read the data.</span></span> 

<span data-ttu-id="994f4-122">Antes de criar um conjunto de dados, crie um **serviço vinculado** para vincular o armazenamento de dados ao data factory.</span><span class="sxs-lookup"><span data-stu-id="994f4-122">Before you create a dataset, create a **linked service** to link your data store to the data factory.</span></span> <span data-ttu-id="994f4-123">Serviços vinculados são como cadeias de conexão, que definem as informações de conexão necessárias para o Data Factory para se conectar a recursos externos.</span><span class="sxs-lookup"><span data-stu-id="994f4-123">Linked services are much like connection strings, which define the connection information needed for Data Factory to connect to external resources.</span></span> <span data-ttu-id="994f4-124">Conjuntos de dados identificam dados em armazenamentos de dados vinculados, como tabelas SQL, arquivos, pastas e documentos.</span><span class="sxs-lookup"><span data-stu-id="994f4-124">Datasets identify data within the linked data stores, such as SQL tables, files, folders, and documents.</span></span> <span data-ttu-id="994f4-125">Por exemplo, um serviço vinculado do Armazenamento do Azure vincula uma conta de armazenamento ao data factory.</span><span class="sxs-lookup"><span data-stu-id="994f4-125">For example, an Azure Storage linked service links a storage account to the data factory.</span></span> <span data-ttu-id="994f4-126">Um conjunto de dados de Blob do Azure representa o contêiner de blob e a pasta que contém os blobs de entrada a ser processado.</span><span class="sxs-lookup"><span data-stu-id="994f4-126">An Azure Blob dataset represents the blob container and the folder that contains the input blobs to be processed.</span></span> 

<span data-ttu-id="994f4-127">Veja abaixo um cenário de exemplo.</span><span class="sxs-lookup"><span data-stu-id="994f4-127">Here is a sample scenario.</span></span> <span data-ttu-id="994f4-128">Para copiar dados do armazenamento de Blobs para um banco de dados SQL, crie dois serviços vinculados: Armazenamento do Azure e Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="994f4-128">To copy data from Blob storage to a SQL database, you create two linked services: Azure Storage and Azure SQL Database.</span></span> <span data-ttu-id="994f4-129">Em seguida, crie dois conjuntos de dados: o conjunto de dados de Blob do Azure (que se refere ao serviço vinculado do Armazenamento do Azure) e o conjunto de dados de Tabela do SQL do Azure (que se refere ao serviço vinculado do Banco de Dados SQL do Azure).</span><span class="sxs-lookup"><span data-stu-id="994f4-129">Then, create two datasets: Azure Blob dataset (which refers to the Azure Storage linked service) and Azure SQL Table dataset (which refers to the Azure SQL Database linked service).</span></span> <span data-ttu-id="994f4-130">Os serviços vinculados do Armazenamento do Azure e do Banco de Dados SQL do Azure contêm cadeias de conexão que o Data Factory usa em tempo de execução para se conectar ao Armazenamento do Azure e ao Banco de Dados SQL do Azure, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="994f4-130">The Azure Storage and Azure SQL Database linked services contain connection strings that Data Factory uses at runtime to connect to your Azure Storage and Azure SQL Database, respectively.</span></span> <span data-ttu-id="994f4-131">O conjunto de dados de Blob do Azure especifica o contêiner de blobs e a pasta de blobs que contém os blobs de entrada no armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="994f4-131">The Azure Blob dataset specifies the blob container and blob folder that contains the input blobs in your Blob storage.</span></span> <span data-ttu-id="994f4-132">O conjunto de dados de Tabela do SQL do Azure especifica a tabela do SQL no banco de dados SQL para o qual os dados serão copiados.</span><span class="sxs-lookup"><span data-stu-id="994f4-132">The Azure SQL Table dataset specifies the SQL table in your SQL database to which the data is to be copied.</span></span>

<span data-ttu-id="994f4-133">O seguinte diagrama mostra a relação entre pipeline, atividade, conjunto de dados e serviço vinculado no Data Factory:</span><span class="sxs-lookup"><span data-stu-id="994f4-133">The following diagram shows the relationships among pipeline, activity, dataset, and linked service in Data Factory:</span></span> 

![Relação entre pipeline, atividade e conjunto de dados, serviços vinculados](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a><span data-ttu-id="994f4-135">Conjunto de dados do JSON</span><span class="sxs-lookup"><span data-stu-id="994f4-135">Dataset JSON</span></span>
<span data-ttu-id="994f4-136">Um conjunto de dados no Data Factory é definido no formato JSON da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="994f4-136">A dataset in Data Factory is defined in JSON format as follows:</span></span>

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag to indicate external data. only for input datasets>,
        "linkedServiceName": "<Name of the linked service that refers to a data store.>",
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies the time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies the interval within the defined frequency. For example, frequency set to 'Hour' and interval set to 1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

<span data-ttu-id="994f4-137">A tabela a seguir descreve as propriedades no JSON acima:</span><span class="sxs-lookup"><span data-stu-id="994f4-137">The following table describes properties in the above JSON:</span></span>   

| <span data-ttu-id="994f4-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="994f4-138">Property</span></span> | <span data-ttu-id="994f4-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="994f4-139">Description</span></span> | <span data-ttu-id="994f4-140">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="994f4-140">Required</span></span> | <span data-ttu-id="994f4-141">Padrão</span><span class="sxs-lookup"><span data-stu-id="994f4-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="994f4-142">name</span><span class="sxs-lookup"><span data-stu-id="994f4-142">name</span></span> |<span data-ttu-id="994f4-143">Nome do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-143">Name of the dataset.</span></span> <span data-ttu-id="994f4-144">Confira [Azure Data Factory - Regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="994f4-144">See [Azure Data Factory - Naming rules](data-factory-naming-rules.md) for naming rules.</span></span> |<span data-ttu-id="994f4-145">Sim</span><span class="sxs-lookup"><span data-stu-id="994f4-145">Yes</span></span> |<span data-ttu-id="994f4-146">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-146">NA</span></span> |
| <span data-ttu-id="994f4-147">type</span><span class="sxs-lookup"><span data-stu-id="994f4-147">type</span></span> |<span data-ttu-id="994f4-148">Tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-148">Type of the dataset.</span></span> <span data-ttu-id="994f4-149">Especifique um dos tipos com suporte no Data Factory (por exemplo: AzureBlob, AzureSqlTable).</span><span class="sxs-lookup"><span data-stu-id="994f4-149">Specify one of the types supported by Data Factory (for example: AzureBlob, AzureSqlTable).</span></span> <br/><br/><span data-ttu-id="994f4-150">Para obter detalhes, consulte [Tipo de conjunto de dados](#Type).</span><span class="sxs-lookup"><span data-stu-id="994f4-150">For details, see [Dataset type](#Type).</span></span> |<span data-ttu-id="994f4-151">Sim</span><span class="sxs-lookup"><span data-stu-id="994f4-151">Yes</span></span> |<span data-ttu-id="994f4-152">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-152">NA</span></span> |
| <span data-ttu-id="994f4-153">estrutura</span><span class="sxs-lookup"><span data-stu-id="994f4-153">structure</span></span> |<span data-ttu-id="994f4-154">Esquema do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-154">Schema of the dataset.</span></span><br/><br/><span data-ttu-id="994f4-155">Para obter detalhes, consulte [Estrutura de conjunto de dados](#Structure).</span><span class="sxs-lookup"><span data-stu-id="994f4-155">For details, see [Dataset structure](#Structure).</span></span> |<span data-ttu-id="994f4-156">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-156">No</span></span> |<span data-ttu-id="994f4-157">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-157">NA</span></span> |
| <span data-ttu-id="994f4-158">typeProperties</span><span class="sxs-lookup"><span data-stu-id="994f4-158">typeProperties</span></span> | <span data-ttu-id="994f4-159">As propriedades de tipo são diferentes para cada tipo (por exemplo: Blob do Azure, tabela do SQL Azure).</span><span class="sxs-lookup"><span data-stu-id="994f4-159">The type properties are different for each type (for example: Azure Blob, Azure SQL table).</span></span> <span data-ttu-id="994f4-160">Para obter detalhes sobre os tipos com suporte e suas propriedades, consulte [Tipo de conjunto de dados](#Type).</span><span class="sxs-lookup"><span data-stu-id="994f4-160">For details on the supported types and their properties, see [Dataset type](#Type).</span></span> |<span data-ttu-id="994f4-161">Sim</span><span class="sxs-lookup"><span data-stu-id="994f4-161">Yes</span></span> |<span data-ttu-id="994f4-162">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-162">NA</span></span> |
| <span data-ttu-id="994f4-163">externo</span><span class="sxs-lookup"><span data-stu-id="994f4-163">external</span></span> | <span data-ttu-id="994f4-164">Sinalizador booliano para especificar se um conjunto de dados é explicitamente produzido por um pipeline de data factory ou não.</span><span class="sxs-lookup"><span data-stu-id="994f4-164">Boolean flag to specify whether a dataset is explicitly produced by a data factory pipeline or not.</span></span> <span data-ttu-id="994f4-165">Se o conjunto de dados de entrada para uma atividade não é produzido pelo pipeline atual, defina esse sinalizador como true.</span><span class="sxs-lookup"><span data-stu-id="994f4-165">If the input dataset for an activity is not produced by the current pipeline, set this flag to true.</span></span> <span data-ttu-id="994f4-166">Defina esse sinalizador como true para o conjunto de dados de entrada da primeira atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="994f4-166">Set this flag to true for the input dataset of the first activity in the pipeline.</span></span>  |<span data-ttu-id="994f4-167">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-167">No</span></span> |<span data-ttu-id="994f4-168">false</span><span class="sxs-lookup"><span data-stu-id="994f4-168">false</span></span> |
| <span data-ttu-id="994f4-169">disponibilidade</span><span class="sxs-lookup"><span data-stu-id="994f4-169">availability</span></span> | <span data-ttu-id="994f4-170">Define a janela de processamento (por exemplo, por hora ou diária) ou o modelo de divisão para a produção de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-170">Defines the processing window (for example, hourly or daily) or the slicing model for the dataset production.</span></span> <span data-ttu-id="994f4-171">Cada unidade de dados consumida e produzida por uma execução de atividade é chamada de uma fatia de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-171">Each unit of data consumed and produced by an activity run is called a data slice.</span></span> <span data-ttu-id="994f4-172">Se a disponibilidade de um conjunto de dados de saída é definida como diária (frequência - Dia, intervalo - 1), uma fatia é produzida diariamente.</span><span class="sxs-lookup"><span data-stu-id="994f4-172">If the availability of an output dataset is set to daily (frequency - Day, interval - 1), a slice is produced daily.</span></span> <br/><br/><span data-ttu-id="994f4-173">Para obter detalhes, consulte [Disponibilidade do conjunto de dados](#Availability).</span><span class="sxs-lookup"><span data-stu-id="994f4-173">For details, see [Dataset availability](#Availability).</span></span> <br/><br/><span data-ttu-id="994f4-174">Para obter detalhes sobre o modelo de divisão do conjunto de dados, consulte o artigo [Agendamento e execução](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="994f4-174">For details on the dataset slicing model, see the [Scheduling and execution](data-factory-scheduling-and-execution.md) article.</span></span> |<span data-ttu-id="994f4-175">Sim</span><span class="sxs-lookup"><span data-stu-id="994f4-175">Yes</span></span> |<span data-ttu-id="994f4-176">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-176">NA</span></span> |
| <span data-ttu-id="994f4-177">policy</span><span class="sxs-lookup"><span data-stu-id="994f4-177">policy</span></span> |<span data-ttu-id="994f4-178">Define os critérios ou a condição que as fatias de conjunto de dados devem atender.</span><span class="sxs-lookup"><span data-stu-id="994f4-178">Defines the criteria or the condition that the dataset slices must fulfill.</span></span> <br/><br/><span data-ttu-id="994f4-179">Para obter detalhes, consulte a seção [Política do conjunto de dados](#Policy).</span><span class="sxs-lookup"><span data-stu-id="994f4-179">For details, see the [Dataset policy](#Policy) section.</span></span> |<span data-ttu-id="994f4-180">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-180">No</span></span> |<span data-ttu-id="994f4-181">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-181">NA</span></span> |

## <a name="dataset-example"></a><span data-ttu-id="994f4-182">Exemplo de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="994f4-182">Dataset example</span></span>
<span data-ttu-id="994f4-183">No exemplo a seguir, o conjunto de dados representa uma tabela chamada **MyTable** em um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="994f4-183">In the following example, the dataset represents a table named **MyTable** in a SQL database.</span></span>

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

<span data-ttu-id="994f4-184">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="994f4-184">Note the following points:</span></span>

* <span data-ttu-id="994f4-185">**type** foi definido como AzureSqlTable.</span><span class="sxs-lookup"><span data-stu-id="994f4-185">**type** is set to AzureSqlTable.</span></span>
* <span data-ttu-id="994f4-186">A propriedade de tipo **tableName** (específica ao tipo AzureSqlTable) foi definida como MyTable.</span><span class="sxs-lookup"><span data-stu-id="994f4-186">**tableName** type property (specific to AzureSqlTable type) is set to MyTable.</span></span>
* <span data-ttu-id="994f4-187">**linkedServiceName** se refere a um serviço vinculado do tipo AzureSqlDatabase, que é definido no próximo trecho de JSON.</span><span class="sxs-lookup"><span data-stu-id="994f4-187">**linkedServiceName** refers to a linked service of type AzureSqlDatabase, which is defined in the next JSON snippet.</span></span> 
* <span data-ttu-id="994f4-188">**Frequência de disponibilidade** é definida como Dia e **intervalo** como 1.</span><span class="sxs-lookup"><span data-stu-id="994f4-188">**availability frequency** is set to Day, and **interval** is set to 1.</span></span> <span data-ttu-id="994f4-189">Isso significa que a fatia do conjunto de dados é gerada diariamente.</span><span class="sxs-lookup"><span data-stu-id="994f4-189">This means that the dataset slice is produced daily.</span></span>  

<span data-ttu-id="994f4-190">**AzureSqlLinkedService** é definido da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="994f4-190">**AzureSqlLinkedService** is defined as follows:</span></span>

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

<span data-ttu-id="994f4-191">No trecho de JSON anterior:</span><span class="sxs-lookup"><span data-stu-id="994f4-191">In the preceding JSON snippet:</span></span>

* <span data-ttu-id="994f4-192">**type** foi definido como AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="994f4-192">**type** is set to AzureSqlDatabase.</span></span>
* <span data-ttu-id="994f4-193">A propriedade de tipo **connectionString** especifica informações para se conectar a um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="994f4-193">**connectionString** type property specifies information to connect to a SQL database.</span></span>  

<span data-ttu-id="994f4-194">Como você pode ver, o serviço vinculado define como se conectar a um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="994f4-194">As you can see, the linked service defines how to connect to a SQL database.</span></span> <span data-ttu-id="994f4-195">O conjunto de dados define qual tabela é usada como uma entrada e saída para a atividade em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="994f4-195">The dataset defines what table is used as an input and output for the activity in a pipeline.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="994f4-196">A menos que um conjunto de dados seja produzido pela pipeline, ele deverá ser marcado como **externo**.</span><span class="sxs-lookup"><span data-stu-id="994f4-196">Unless a dataset is being produced by the pipeline, it should be marked as **external**.</span></span> <span data-ttu-id="994f4-197">Essa configuração geralmente se aplica às entradas da primeira atividade em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="994f4-197">This setting generally applies to inputs of first activity in a pipeline.</span></span>   


## <span data-ttu-id="994f4-198"><a name="Type"></a> Tipo de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="994f4-198"><a name="Type"></a> Dataset type</span></span>
<span data-ttu-id="994f4-199">O tipo do conjunto de dados depende do armazenamento de dados que você usa.</span><span class="sxs-lookup"><span data-stu-id="994f4-199">The type of the dataset depends on the data store you use.</span></span> <span data-ttu-id="994f4-200">Consulte a tabela a seguir para obter uma lista de armazenamentos de dados com suporte pelo Data Factory.</span><span class="sxs-lookup"><span data-stu-id="994f4-200">See the following table for a list of data stores supported by Data Factory.</span></span> <span data-ttu-id="994f4-201">Clique em um armazenamento de dados para saber como criar um serviço vinculado e um conjunto de dados para esse armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-201">Click a data store to learn how to create a linked service and a dataset for that data store.</span></span>

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> <span data-ttu-id="994f4-202">Armazenamentos de dados com * podem ser locais ou IaaS (infraestrutura como serviço) do Azure.</span><span class="sxs-lookup"><span data-stu-id="994f4-202">Data stores with * can be on-premises or on Azure infrastructure as a service (IaaS).</span></span> <span data-ttu-id="994f4-203">Esses armazenamentos de dados exigem a instalação do [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="994f4-203">These data stores require you to install [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="994f4-204">No exemplo na seção anterior, o tipo do conjunto de dados é definido como **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="994f4-204">In the example in the previous section, the type of the dataset is set to **AzureSqlTable**.</span></span> <span data-ttu-id="994f4-205">Da mesma forma, para um conjunto de dados de Blob do Azure, o tipo do conjunto de dados é definido como **AzureBlob**, conforme mostrado no seguinte JSON:</span><span class="sxs-lookup"><span data-stu-id="994f4-205">Similarly, for an Azure Blob dataset, the type of the dataset is set to **AzureBlob**, as shown in the following JSON:</span></span>

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

## <span data-ttu-id="994f4-206"><a name="Structure"></a>Estrutura do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="994f4-206"><a name="Structure"></a>Dataset structure</span></span>
<span data-ttu-id="994f4-207">A seção **estrutura** é opcional.</span><span class="sxs-lookup"><span data-stu-id="994f4-207">The **structure** section is optional.</span></span> <span data-ttu-id="994f4-208">Ela define o esquema do conjunto de dados contendo uma coleção de nomes e tipos de dados de colunas.</span><span class="sxs-lookup"><span data-stu-id="994f4-208">It defines the schema of the dataset by containing a collection of names and data types of columns.</span></span> <span data-ttu-id="994f4-209">Use a seção de estrutura para fornecer informações de tipo que são usadas para converter tipos e mapear colunas da origem para o destino.</span><span class="sxs-lookup"><span data-stu-id="994f4-209">You use the structure section to provide type information that is used to convert types and map columns from the source to the destination.</span></span> <span data-ttu-id="994f4-210">No seguinte exemplo, o conjunto de dados tem três colunas: `slicetimestamp`, `projectname` e `pageviews`.</span><span class="sxs-lookup"><span data-stu-id="994f4-210">In the following example, the dataset has three columns: `slicetimestamp`, `projectname`, and `pageviews`.</span></span> <span data-ttu-id="994f4-211">Elas são do tipo String, String e Decimal, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="994f4-211">They are of type String, String, and Decimal, respectively.</span></span>

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

<span data-ttu-id="994f4-212">Cada coluna da seção Estrutura contém as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="994f4-212">Each column in the structure contains the following properties:</span></span>

| <span data-ttu-id="994f4-213">Propriedade</span><span class="sxs-lookup"><span data-stu-id="994f4-213">Property</span></span> | <span data-ttu-id="994f4-214">Descrição</span><span class="sxs-lookup"><span data-stu-id="994f4-214">Description</span></span> | <span data-ttu-id="994f4-215">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="994f4-215">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="994f4-216">name</span><span class="sxs-lookup"><span data-stu-id="994f4-216">name</span></span> |<span data-ttu-id="994f4-217">Nome da coluna.</span><span class="sxs-lookup"><span data-stu-id="994f4-217">Name of the column.</span></span> |<span data-ttu-id="994f4-218">Sim</span><span class="sxs-lookup"><span data-stu-id="994f4-218">Yes</span></span> |
| <span data-ttu-id="994f4-219">type</span><span class="sxs-lookup"><span data-stu-id="994f4-219">type</span></span> |<span data-ttu-id="994f4-220">Tipo de dados da coluna.</span><span class="sxs-lookup"><span data-stu-id="994f4-220">Data type of the column.</span></span>  |<span data-ttu-id="994f4-221">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-221">No</span></span> |
| <span data-ttu-id="994f4-222">culture</span><span class="sxs-lookup"><span data-stu-id="994f4-222">culture</span></span> |<span data-ttu-id="994f4-223">Cultura baseada em .NET a ser usada quando o tipo é um tipo .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="994f4-223">.NET-based culture to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> <span data-ttu-id="994f4-224">O padrão é `en-us`.</span><span class="sxs-lookup"><span data-stu-id="994f4-224">The default is `en-us`.</span></span> |<span data-ttu-id="994f4-225">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-225">No</span></span> |
| <span data-ttu-id="994f4-226">formato</span><span class="sxs-lookup"><span data-stu-id="994f4-226">format</span></span> |<span data-ttu-id="994f4-227">O formato de cadeia de caracteres a ser usado quando o tipo é um tipo .NET `Datetime` ou `Datetimeoffset`.</span><span class="sxs-lookup"><span data-stu-id="994f4-227">Format string to be used when the type is a .NET type: `Datetime` or `Datetimeoffset`.</span></span> |<span data-ttu-id="994f4-228">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-228">No</span></span> |

<span data-ttu-id="994f4-229">As diretrizes a seguir ajudam você a determinar quando incluir informações de estrutura e o que incluir na seção **estrutura**.</span><span class="sxs-lookup"><span data-stu-id="994f4-229">The following guidelines help you determine when to include structure information, and what to include in the **structure** section.</span></span>

* <span data-ttu-id="994f4-230">**Para fontes de dados estruturadas**, especifique a seção de estrutura somente se desejar mapear colunas de origem para colunas do coletor; além disso, seus nomes não são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="994f4-230">**For structured data sources**, specify the structure section only if you want map source columns to sink columns, and their names are not the same.</span></span> <span data-ttu-id="994f4-231">Esse tipo de fonte de dados estruturada armazena informações de esquema de dados e de tipo juntamente com os próprios dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-231">This kind of structured data source stores data schema and type information along with the data itself.</span></span> <span data-ttu-id="994f4-232">Exemplos de fontes de dados estruturadas incluem SQL Server, Oracle e tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="994f4-232">Examples of structured data sources include SQL Server, Oracle, and Azure table.</span></span> 
  
    <span data-ttu-id="994f4-233">Como as informações de tipo já estão disponíveis para fontes de dados estruturadas, não inclua informações de tipo quando incluir a seção de estrutura.</span><span class="sxs-lookup"><span data-stu-id="994f4-233">As type information is already available for structured data sources, you should not include type information when you do include the structure section.</span></span>
* <span data-ttu-id="994f4-234">**Para o esquema em fontes de dados de leitura (especificamente o armazenamento de Blobs)**, você pode optar por armazenar os dados sem armazenar nenhuma informação de tipo ou de esquema juntamente com os dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-234">**For schema on read data sources (specifically Blob storage)**, you can choose to store data without storing any schema or type information with the data.</span></span> <span data-ttu-id="994f4-235">Para esses tipos de fontes de dados, inclua a estrutura quando desejar mapear as colunas de origem para as colunas do coletor.</span><span class="sxs-lookup"><span data-stu-id="994f4-235">For these types of data sources, include structure when you want to map source columns to sink columns.</span></span> <span data-ttu-id="994f4-236">Também inclua a estrutura quando o conjunto de dados for uma entrada para uma atividade de cópia e os tipos de dados do conjunto de dados de origem precisarem ser convertidos em tipos nativos para o coletor.</span><span class="sxs-lookup"><span data-stu-id="994f4-236">Also include structure when the dataset is an input for a copy activity, and data types of source dataset should be converted to native types for the sink.</span></span> 
    
    <span data-ttu-id="994f4-237">O Data Factory dá suporte aos seguintes valores para fornecer informações de tipo na estrutura: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset e Timespan**.</span><span class="sxs-lookup"><span data-stu-id="994f4-237">Data Factory supports the following values for providing type information in structure: **Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan**.</span></span> <span data-ttu-id="994f4-238">Esses valores são valores de tipo baseados em NET e em conformidade com CLS (Common Language Specification).</span><span class="sxs-lookup"><span data-stu-id="994f4-238">These values are Common Language Specification (CLS)-compliant, .NET-based type values.</span></span>

<span data-ttu-id="994f4-239">O Data Factory executa conversões de tipo automaticamente ao mover dados de um armazenamento de dados de origem para um armazenamento de dados do coletor.</span><span class="sxs-lookup"><span data-stu-id="994f4-239">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span> 
  

## <a name="dataset-availability"></a><span data-ttu-id="994f4-240">Disponibilidade do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="994f4-240">Dataset availability</span></span>
<span data-ttu-id="994f4-241">A seção **disponibilidade** em um conjunto de dados define a janela de processamento (por exemplo, por hora, diária ou semanal) do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-241">The **availability** section in a dataset defines the processing window (for example, hourly, daily, or weekly) for the dataset.</span></span> <span data-ttu-id="994f4-242">Para obter mais informações sobre janelas de atividades, consulte [Agendamento e execução](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="994f4-242">For more information about activity windows, see [Scheduling and execution](data-factory-scheduling-and-execution.md).</span></span>

<span data-ttu-id="994f4-243">A seguinte seção de disponibilidade especifica que o conjunto de dados de saída é gerado a cada hora ou o conjunto de dados de entrada está disponível a cada hora:</span><span class="sxs-lookup"><span data-stu-id="994f4-243">The following availability section specifies that the output dataset is either produced hourly, or the input dataset is available hourly:</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

<span data-ttu-id="994f4-244">Se o pipeline tem as seguintes horas de início e término:</span><span class="sxs-lookup"><span data-stu-id="994f4-244">If the pipeline has the following start and end times:</span></span>  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

<span data-ttu-id="994f4-245">O conjunto de dados de saída é gerado de hora em hora, dentro dos horários de início e término do pipeline.</span><span class="sxs-lookup"><span data-stu-id="994f4-245">The output dataset is produced hourly within the pipeline start and end times.</span></span> <span data-ttu-id="994f4-246">Portanto, cinco fatias de conjunto de dados são geradas por esse pipeline, uma para cada janela de atividades (00h à 1h, 1h às 2h, 2h às 3h, 3h às 4h e 4h às 5h).</span><span class="sxs-lookup"><span data-stu-id="994f4-246">Therefore, there are five dataset slices produced by this pipeline, one for each activity window (12 AM - 1 AM, 1 AM - 2 AM, 2 AM - 3 AM, 3 AM - 4 AM, 4 AM - 5 AM).</span></span> 

<span data-ttu-id="994f4-247">A tabela a seguir descreve as propriedades que você pode usar na seção de disponibilidade:</span><span class="sxs-lookup"><span data-stu-id="994f4-247">The following table describes properties you can use in the availability section:</span></span>

| <span data-ttu-id="994f4-248">Propriedade</span><span class="sxs-lookup"><span data-stu-id="994f4-248">Property</span></span> | <span data-ttu-id="994f4-249">Descrição</span><span class="sxs-lookup"><span data-stu-id="994f4-249">Description</span></span> | <span data-ttu-id="994f4-250">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="994f4-250">Required</span></span> | <span data-ttu-id="994f4-251">Padrão</span><span class="sxs-lookup"><span data-stu-id="994f4-251">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="994f4-252">frequência</span><span class="sxs-lookup"><span data-stu-id="994f4-252">frequency</span></span> |<span data-ttu-id="994f4-253">Especifica a unidade de tempo para a produção da fatia de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-253">Specifies the time unit for dataset slice production.</span></span><br/><br/><span data-ttu-id="994f4-254"><b>Frequência com suporte</b>: Minuto, Hora, Dia, Semana, Mês</span><span class="sxs-lookup"><span data-stu-id="994f4-254"><b>Supported frequency</b>: Minute, Hour, Day, Week, Month</span></span> |<span data-ttu-id="994f4-255">Sim</span><span class="sxs-lookup"><span data-stu-id="994f4-255">Yes</span></span> |<span data-ttu-id="994f4-256">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-256">NA</span></span> |
| <span data-ttu-id="994f4-257">intervalo</span><span class="sxs-lookup"><span data-stu-id="994f4-257">interval</span></span> |<span data-ttu-id="994f4-258">Especifica um multiplicador para a frequência.</span><span class="sxs-lookup"><span data-stu-id="994f4-258">Specifies a multiplier for frequency.</span></span><br/><br/><span data-ttu-id="994f4-259">“Frequência x intervalo” determina a frequência com que a fatia é gerada.</span><span class="sxs-lookup"><span data-stu-id="994f4-259">"Frequency x interval" determines how often the slice is produced.</span></span> <span data-ttu-id="994f4-260">Por exemplo, se você precisa que o conjunto de dados seja dividido por hora, defina <b>frequência</b> como <b>Hora</b> e <b>intervalo</b> como <b>1</b>.</span><span class="sxs-lookup"><span data-stu-id="994f4-260">For example, if you need the dataset to be sliced on an hourly basis, you set <b>frequency</b> to <b>Hour</b>, and <b>interval</b> to <b>1</b>.</span></span><br/><br/><span data-ttu-id="994f4-261">Observe que, caso você especifique a **frequência** como **Minuto**, deverá definir o intervalo como não inferior a 15.</span><span class="sxs-lookup"><span data-stu-id="994f4-261">Note that if you specify **frequency** as **Minute**, you should set the interval to no less than 15.</span></span> |<span data-ttu-id="994f4-262">Sim</span><span class="sxs-lookup"><span data-stu-id="994f4-262">Yes</span></span> |<span data-ttu-id="994f4-263">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-263">NA</span></span> |
| <span data-ttu-id="994f4-264">estilo</span><span class="sxs-lookup"><span data-stu-id="994f4-264">style</span></span> |<span data-ttu-id="994f4-265">Especifica se a fatia deve ser gerada no início ou término do intervalo.</span><span class="sxs-lookup"><span data-stu-id="994f4-265">Specifies whether the slice should be produced at the start or end of the interval.</span></span><ul><li><span data-ttu-id="994f4-266">StartOfInterval</span><span class="sxs-lookup"><span data-stu-id="994f4-266">StartOfInterval</span></span></li><li><span data-ttu-id="994f4-267">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="994f4-267">EndOfInterval</span></span></li></ul><span data-ttu-id="994f4-268">Se a **frequência** for definida como **Mês** e o **estilo** como **EndOfInterval**, a fatia será gerada no último dia do mês.</span><span class="sxs-lookup"><span data-stu-id="994f4-268">If **frequency** is set to **Month**, and **style** is set to **EndOfInterval**, the slice is produced on the last day of month.</span></span> <span data-ttu-id="994f4-269">Se o **estilo** for definido como **StartOfInterval**, a fatia será gerada no primeiro dia do mês.</span><span class="sxs-lookup"><span data-stu-id="994f4-269">If **style** is set to **StartOfInterval**, the slice is produced on the first day of month.</span></span><br/><br/><span data-ttu-id="994f4-270">Se a **frequência** for definida como **Dia** e o **estilo** como **EndOfInterval**, a fatia será gerada na última hora do dia.</span><span class="sxs-lookup"><span data-stu-id="994f4-270">If **frequency** is set to **Day**, and **style** is set to **EndOfInterval**, the slice is produced in the last hour of the day.</span></span><br/><br/><span data-ttu-id="994f4-271">Se a **frequência** for definida como **Hora** e o **estilo** como **EndOfInterval**, a fatia será gerada ao final da hora.</span><span class="sxs-lookup"><span data-stu-id="994f4-271">If **frequency** is set to **Hour**, and **style** is set to **EndOfInterval**, the slice is produced at the end of the hour.</span></span> <span data-ttu-id="994f4-272">Por exemplo, para uma fatia do período 13h às 14h, a fatia é gerada às 14h.</span><span class="sxs-lookup"><span data-stu-id="994f4-272">For example, for a slice for the 1 PM - 2 PM period, the slice is produced at 2 PM.</span></span> |<span data-ttu-id="994f4-273">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-273">No</span></span> |<span data-ttu-id="994f4-274">EndOfInterval</span><span class="sxs-lookup"><span data-stu-id="994f4-274">EndOfInterval</span></span> |
| <span data-ttu-id="994f4-275">anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="994f4-275">anchorDateTime</span></span> |<span data-ttu-id="994f4-276">Define a posição absoluta no tempo usada pelo agendador para computar limites de fatia do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-276">Defines the absolute position in time used by the scheduler to compute dataset slice boundaries.</span></span> <br/><br/><span data-ttu-id="994f4-277">Observe que, se essa propriedade tiver partes de data que são mais granulares do que a frequência especificada, as partes mais granulares serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="994f4-277">Note that if this propoerty has date parts that are more granular than the specified frequency, the more granular parts are ignored.</span></span> <span data-ttu-id="994f4-278">Por exemplo, se o **intervalo** for **por hora** (frequência: hora e intervalo: 1) e a **anchorDateTime** contiver **minutos e segundos**, as partes de minutos e segundos da **anchorDateTime** serão ignoradas.</span><span class="sxs-lookup"><span data-stu-id="994f4-278">For example, if the **interval** is **hourly** (frequency: hour and interval: 1), and the **anchorDateTime** contains **minutes and seconds**, then the minutes and seconds parts of **anchorDateTime** are ignored.</span></span> |<span data-ttu-id="994f4-279">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-279">No</span></span> |<span data-ttu-id="994f4-280">01/01/0001</span><span class="sxs-lookup"><span data-stu-id="994f4-280">01/01/0001</span></span> |
| <span data-ttu-id="994f4-281">deslocamento</span><span class="sxs-lookup"><span data-stu-id="994f4-281">offset</span></span> |<span data-ttu-id="994f4-282">O período de tempo no qual o início e o término de todas as fatias de conjunto de dados são deslocados.</span><span class="sxs-lookup"><span data-stu-id="994f4-282">Timespan by which the start and end of all dataset slices are shifted.</span></span> <br/><br/><span data-ttu-id="994f4-283">Observe que, se **anchorDateTime** e **offset** forem especificados, o resultado será um deslocamento combinado.</span><span class="sxs-lookup"><span data-stu-id="994f4-283">Note that if both **anchorDateTime** and **offset** are specified, the result is the combined shift.</span></span> |<span data-ttu-id="994f4-284">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-284">No</span></span> |<span data-ttu-id="994f4-285">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-285">NA</span></span> |

### <a name="offset-example"></a><span data-ttu-id="994f4-286">exemplo de deslocamento</span><span class="sxs-lookup"><span data-stu-id="994f4-286">offset example</span></span>
<span data-ttu-id="994f4-287">Por padrão, as fatias diárias (`"frequency": "Day", "interval": 1`) começam às 00h (meia-noite) em UTC (Tempo Universal Coordenado).</span><span class="sxs-lookup"><span data-stu-id="994f4-287">By default, daily (`"frequency": "Day", "interval": 1`) slices start at 12 AM (midnight) Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="994f4-288">Se desejar que a hora de início para hora UTC de 6 horas em vez disso, define o deslocamento, conforme mostrado no trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="994f4-288">If you want the start time to be 6 AM UTC time instead, set the offset as shown in the following snippet:</span></span> 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a><span data-ttu-id="994f4-289">Exemplo de anchorDateTime</span><span class="sxs-lookup"><span data-stu-id="994f4-289">anchorDateTime example</span></span>
<span data-ttu-id="994f4-290">No exemplo a seguir, o conjunto de dados é gerado uma vez a cada 23 horas.</span><span class="sxs-lookup"><span data-stu-id="994f4-290">In the following example, the dataset is produced once every 23 hours.</span></span> <span data-ttu-id="994f4-291">A primeira fatia começa na hora especificada pela **anchorDateTime**, que é definida como `2017-04-19T08:00:00` (UTC).</span><span class="sxs-lookup"><span data-stu-id="994f4-291">The first slice starts at the time specified by **anchorDateTime**, which is set to `2017-04-19T08:00:00` (UTC).</span></span>

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a><span data-ttu-id="994f4-292">exemplo de deslocamento/estilo</span><span class="sxs-lookup"><span data-stu-id="994f4-292">offset/style example</span></span>
<span data-ttu-id="994f4-293">O seguinte conjunto de dados é mensal e é gerado no terceiro de cada mês às 8h (`3.08:00:00`):</span><span class="sxs-lookup"><span data-stu-id="994f4-293">The following dataset is monthly, and is produced on the 3rd of every month at 8:00 AM (`3.08:00:00`):</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <span data-ttu-id="994f4-294"><a name="Policy"></a>Política de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="994f4-294"><a name="Policy"></a>Dataset policy</span></span>
<span data-ttu-id="994f4-295">A seção **política** na definição do conjunto de dados define os critérios ou a condição que as divisões de conjunto de dados devem atender.</span><span class="sxs-lookup"><span data-stu-id="994f4-295">The **policy** section in the dataset definition defines the criteria or the condition that the dataset slices must fulfill.</span></span>

### <a name="validation-policies"></a><span data-ttu-id="994f4-296">Políticas de validação</span><span class="sxs-lookup"><span data-stu-id="994f4-296">Validation policies</span></span>
| <span data-ttu-id="994f4-297">Nome da política</span><span class="sxs-lookup"><span data-stu-id="994f4-297">Policy name</span></span> | <span data-ttu-id="994f4-298">Descrição</span><span class="sxs-lookup"><span data-stu-id="994f4-298">Description</span></span> | <span data-ttu-id="994f4-299">Aplicado a</span><span class="sxs-lookup"><span data-stu-id="994f4-299">Applied to</span></span> | <span data-ttu-id="994f4-300">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="994f4-300">Required</span></span> | <span data-ttu-id="994f4-301">Padrão</span><span class="sxs-lookup"><span data-stu-id="994f4-301">Default</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="994f4-302">minimumSizeMB</span><span class="sxs-lookup"><span data-stu-id="994f4-302">minimumSizeMB</span></span> |<span data-ttu-id="994f4-303">Valida se os dados em um **armazenamento de Blobs do Azure** atendem aos requisitos de tamanho mínimo (em megabytes).</span><span class="sxs-lookup"><span data-stu-id="994f4-303">Validates that the data in **Azure Blob storage** meets the minimum size requirements (in megabytes).</span></span> |<span data-ttu-id="994f4-304">Armazenamento do Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="994f4-304">Azure Blob storage</span></span> |<span data-ttu-id="994f4-305">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-305">No</span></span> |<span data-ttu-id="994f4-306">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-306">NA</span></span> |
| <span data-ttu-id="994f4-307">minimumRows</span><span class="sxs-lookup"><span data-stu-id="994f4-307">minimumRows</span></span> |<span data-ttu-id="994f4-308">Valida que os dados em um **Banco de Dados SQL do Azure** ou uma **tabela do Azure** contêm o número mínimo de linhas.</span><span class="sxs-lookup"><span data-stu-id="994f4-308">Validates that the data in an **Azure SQL database** or an **Azure table** contains the minimum number of rows.</span></span> |<ul><li><span data-ttu-id="994f4-309">Banco de Dados SQL Azure</span><span class="sxs-lookup"><span data-stu-id="994f4-309">Azure SQL database</span></span></li><li><span data-ttu-id="994f4-310">Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="994f4-310">Azure table</span></span></li></ul> |<span data-ttu-id="994f4-311">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-311">No</span></span> |<span data-ttu-id="994f4-312">ND</span><span class="sxs-lookup"><span data-stu-id="994f4-312">NA</span></span> |

#### <a name="examples"></a><span data-ttu-id="994f4-313">Exemplos</span><span class="sxs-lookup"><span data-stu-id="994f4-313">Examples</span></span>
<span data-ttu-id="994f4-314">**minimumSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="994f4-314">**minimumSizeMB:**</span></span>

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

<span data-ttu-id="994f4-315">**minimumRows:**</span><span class="sxs-lookup"><span data-stu-id="994f4-315">**minimumRows:**</span></span>

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

### <a name="external-datasets"></a><span data-ttu-id="994f4-316">Conjuntos de dados externos</span><span class="sxs-lookup"><span data-stu-id="994f4-316">External datasets</span></span>
<span data-ttu-id="994f4-317">Conjuntos de dados externos são aqueles que não são produzidos por um pipeline em execução na data factory.</span><span class="sxs-lookup"><span data-stu-id="994f4-317">External datasets are the ones that are not produced by a running pipeline in the data factory.</span></span> <span data-ttu-id="994f4-318">Se o conjunto de dados estiver marcado como **external**, a política **ExternalData** poderá ser definida para influenciar o comportamento da disponibilidade da divisão do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="994f4-318">If the dataset is marked as **external**, the **ExternalData** policy may be defined to influence the behavior of the dataset slice availability.</span></span>

<span data-ttu-id="994f4-319">A menos que um conjunto de dados seja gerado pelo Data Factory, ele deverá ser marcado como **externo**.</span><span class="sxs-lookup"><span data-stu-id="994f4-319">Unless a dataset is being produced by Data Factory, it should be marked as **external**.</span></span> <span data-ttu-id="994f4-320">Essa configuração geralmente se aplica às entradas da primeira atividade em um pipeline, a menos que um encadeamento de atividade ou de pipeline seja usado.</span><span class="sxs-lookup"><span data-stu-id="994f4-320">This setting generally applies to the inputs of first activity in a pipeline, unless activity or pipeline chaining is being used.</span></span>

| <span data-ttu-id="994f4-321">Nome</span><span class="sxs-lookup"><span data-stu-id="994f4-321">Name</span></span> | <span data-ttu-id="994f4-322">Descrição</span><span class="sxs-lookup"><span data-stu-id="994f4-322">Description</span></span> | <span data-ttu-id="994f4-323">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="994f4-323">Required</span></span> | <span data-ttu-id="994f4-324">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="994f4-324">Default value</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="994f4-325">dataDelay</span><span class="sxs-lookup"><span data-stu-id="994f4-325">dataDelay</span></span> |<span data-ttu-id="994f4-326">O tempo de atraso da verificação da disponibilidade dos dados externos da divisão especificada.</span><span class="sxs-lookup"><span data-stu-id="994f4-326">The time to delay the check on the availability of the external data for the given slice.</span></span> <span data-ttu-id="994f4-327">Por exemplo, é possível atrasar uma verificação por hora usando essa configuração.</span><span class="sxs-lookup"><span data-stu-id="994f4-327">For example, you can delay an hourly check by using this setting.</span></span><br/><br/><span data-ttu-id="994f4-328">A configuração se aplica somente à hora atual.</span><span class="sxs-lookup"><span data-stu-id="994f4-328">The setting only applies to the present time.</span></span>  <span data-ttu-id="994f4-329">Por exemplo, se agora forem 13hs e se esse valor for 10 minutos, a validação começará às 13:10hs.</span><span class="sxs-lookup"><span data-stu-id="994f4-329">For example, if it is 1:00 PM right now and this value is 10 minutes, the validation starts at 1:10 PM.</span></span><br/><br/><span data-ttu-id="994f4-330">Observe que essa configuração não afeta as fatias do passado.</span><span class="sxs-lookup"><span data-stu-id="994f4-330">Note that this setting does not affect slices in the past.</span></span> <span data-ttu-id="994f4-331">Fatias com **Hora de Término da Fatia** + **dataDelay** < **Agora** são processadas sem atrasos.</span><span class="sxs-lookup"><span data-stu-id="994f4-331">Slices with **Slice End Time** + **dataDelay** < **Now** are processed without any delay.</span></span><br/><br/><span data-ttu-id="994f4-332">Horas maiores que 23h59 horas devem ser especificadas com o formato `day.hours:minutes:seconds`.</span><span class="sxs-lookup"><span data-stu-id="994f4-332">Times greater than 23:59 hours should be specified by using the `day.hours:minutes:seconds` format.</span></span> <span data-ttu-id="994f4-333">Por exemplo, para especificar 24 horas, não use 24:00:00.</span><span class="sxs-lookup"><span data-stu-id="994f4-333">For example, to specify 24 hours, don't use 24:00:00.</span></span> <span data-ttu-id="994f4-334">Em vez disso, use 1.00:00:00.</span><span class="sxs-lookup"><span data-stu-id="994f4-334">Instead, use 1.00:00:00.</span></span> <span data-ttu-id="994f4-335">Se você usar 24:00:00, isso será tratado como 24 dias (24.00:00:00).</span><span class="sxs-lookup"><span data-stu-id="994f4-335">If you use 24:00:00, it is treated as 24 days (24.00:00:00).</span></span> <span data-ttu-id="994f4-336">Para 1 dia e 4 horas, especifique 1:04:00:00.</span><span class="sxs-lookup"><span data-stu-id="994f4-336">For 1 day and 4 hours, specify 1:04:00:00.</span></span> |<span data-ttu-id="994f4-337">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-337">No</span></span> |<span data-ttu-id="994f4-338">0</span><span class="sxs-lookup"><span data-stu-id="994f4-338">0</span></span> |
| <span data-ttu-id="994f4-339">retryInterval</span><span class="sxs-lookup"><span data-stu-id="994f4-339">retryInterval</span></span> |<span data-ttu-id="994f4-340">O tempo de espera entre uma falha e a próxima tentativa.</span><span class="sxs-lookup"><span data-stu-id="994f4-340">The wait time between a failure and the next attempt.</span></span> <span data-ttu-id="994f4-341">Essa configuração se aplica à hora atual.</span><span class="sxs-lookup"><span data-stu-id="994f4-341">This setting applies to present time.</span></span> <span data-ttu-id="994f4-342">Se a tentativa anterior falhou, a próxima tentativa ocorrerá após o período de **retryInterval**.</span><span class="sxs-lookup"><span data-stu-id="994f4-342">If the previous try failed, the next try is after the **retryInterval** period.</span></span> <br/><br/><span data-ttu-id="994f4-343">Se agora for 1:00 PM, iniciaremos a primeira tentativa.</span><span class="sxs-lookup"><span data-stu-id="994f4-343">If it is 1:00 PM right now, we begin the first try.</span></span> <span data-ttu-id="994f4-344">Se a duração para concluir a primeira verificação de validação for 1 minuto e a operação tiver falhado, a próxima repetição será às 13h + 1min (duração) + 1min (intervalo de repetição) = 13h02.</span><span class="sxs-lookup"><span data-stu-id="994f4-344">If the duration to complete the first validation check is 1 minute and the operation failed, the next retry is at 1:00 + 1min (duration) + 1min (retry interval) = 1:02 PM.</span></span> <br/><br/><span data-ttu-id="994f4-345">Para fatias no passado, não haverá nenhum atraso.</span><span class="sxs-lookup"><span data-stu-id="994f4-345">For slices in the past, there is no delay.</span></span> <span data-ttu-id="994f4-346">A repetição acontece imediatamente.</span><span class="sxs-lookup"><span data-stu-id="994f4-346">The retry happens immediately.</span></span> |<span data-ttu-id="994f4-347">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-347">No</span></span> |<span data-ttu-id="994f4-348">00:01:00 (1 minuto)</span><span class="sxs-lookup"><span data-stu-id="994f4-348">00:01:00 (1 minute)</span></span> |
| <span data-ttu-id="994f4-349">retryTimeout</span><span class="sxs-lookup"><span data-stu-id="994f4-349">retryTimeout</span></span> |<span data-ttu-id="994f4-350">O tempo limite para cada tentativa de repetição.</span><span class="sxs-lookup"><span data-stu-id="994f4-350">The timeout for each retry attempt.</span></span><br/><br/><span data-ttu-id="994f4-351">Se essa propriedade for definida como 10 minutos, a validação deverá ser concluída em 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="994f4-351">If this property is set to 10 minutes, the validation should be completed within 10 minutes.</span></span> <span data-ttu-id="994f4-352">Se demorar mais de 10 minutos para executar a validação, a repetição atingirá o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="994f4-352">If it takes longer than 10 minutes to perform the validation, the retry times out.</span></span><br/><br/><span data-ttu-id="994f4-353">Se todas as tentativas para a validação atingirem o tempo limite, a fatia será marcada como **TimedOut**.</span><span class="sxs-lookup"><span data-stu-id="994f4-353">If all attempts for the validation time out, the slice is marked as **TimedOut**.</span></span> |<span data-ttu-id="994f4-354">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-354">No</span></span> |<span data-ttu-id="994f4-355">00:10:00 (10 minutos)</span><span class="sxs-lookup"><span data-stu-id="994f4-355">00:10:00 (10 minutes)</span></span> |
| <span data-ttu-id="994f4-356">maximumRetry</span><span class="sxs-lookup"><span data-stu-id="994f4-356">maximumRetry</span></span> |<span data-ttu-id="994f4-357">O número de vezes para verificar a disponibilidade dos dados externos.</span><span class="sxs-lookup"><span data-stu-id="994f4-357">The number of times to check for the availability of the external data.</span></span> <span data-ttu-id="994f4-358">O valor máximo permitido é 10.</span><span class="sxs-lookup"><span data-stu-id="994f4-358">The maximum allowed value is 10.</span></span> |<span data-ttu-id="994f4-359">Não</span><span class="sxs-lookup"><span data-stu-id="994f4-359">No</span></span> |<span data-ttu-id="994f4-360">3</span><span class="sxs-lookup"><span data-stu-id="994f4-360">3</span></span> |


## <a name="create-datasets"></a><span data-ttu-id="994f4-361">Criar conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="994f4-361">Create datasets</span></span>
<span data-ttu-id="994f4-362">Você pode criar conjuntos de dados usando uma destas ferramentas ou SDKs:</span><span class="sxs-lookup"><span data-stu-id="994f4-362">You can create datasets by using one of these tools or SDKs:</span></span> 

- <span data-ttu-id="994f4-363">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="994f4-363">Copy Wizard</span></span> 
- <span data-ttu-id="994f4-364">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="994f4-364">Azure portal</span></span>
- <span data-ttu-id="994f4-365">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="994f4-365">Visual Studio</span></span>
- <span data-ttu-id="994f4-366">PowerShell</span><span class="sxs-lookup"><span data-stu-id="994f4-366">PowerShell</span></span>
- <span data-ttu-id="994f4-367">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="994f4-367">Azure Resource Manager template</span></span>
- <span data-ttu-id="994f4-368">API REST</span><span class="sxs-lookup"><span data-stu-id="994f4-368">REST API</span></span>
- <span data-ttu-id="994f4-369">API do .NET</span><span class="sxs-lookup"><span data-stu-id="994f4-369">.NET API</span></span>

<span data-ttu-id="994f4-370">Consulte os seguintes tutoriais para obter instruções passo a passo para criar pipelines e conjuntos de dados usando uma destas ferramentas ou SDKs:</span><span class="sxs-lookup"><span data-stu-id="994f4-370">See the following tutorials for step-by-step instructions for creating pipelines and datasets by using one of these tools or SDKs:</span></span>
 
- [<span data-ttu-id="994f4-371">Crie um pipeline com uma atividade de transformação de dados</span><span class="sxs-lookup"><span data-stu-id="994f4-371">Build a pipeline with a data transformation activity</span></span>](data-factory-build-your-first-pipeline.md)
- [<span data-ttu-id="994f4-372">Crie um pipeline com uma atividade de movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="994f4-372">Build a pipeline with a data movement activity</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

<span data-ttu-id="994f4-373">Depois que um pipeline é criado e implantado, você pode gerenciar e monitorar seus pipelines usando as folhas do portal do Azure ou o aplicativo de Monitoramento e Gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="994f4-373">After a pipeline is created and deployed, you can manage and monitor your pipelines by using the Azure portal blades, or the Monitoring and Management app.</span></span> <span data-ttu-id="994f4-374">Consulte os seguintes tópicos para obter instruções passo a passo:</span><span class="sxs-lookup"><span data-stu-id="994f4-374">See the following topics for step-by-step instructions:</span></span> 

- [<span data-ttu-id="994f4-375">Monitorar e gerenciar pipelines usando as folhas do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="994f4-375">Monitor and manage pipelines by using Azure portal blades</span></span>](data-factory-monitor-manage-pipelines.md)
- [<span data-ttu-id="994f4-376">Monitorar e gerenciar pipelines usando o aplicativo de Monitoramento e Gerenciamento</span><span class="sxs-lookup"><span data-stu-id="994f4-376">Monitor and manage pipelines by using the Monitoring and Management app</span></span>](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a><span data-ttu-id="994f4-377">Conjuntos de dados com escopo</span><span class="sxs-lookup"><span data-stu-id="994f4-377">Scoped datasets</span></span>
<span data-ttu-id="994f4-378">Você pode criar conjuntos de dados que estão no escopo de um pipeline usando a propriedade **datasets** .</span><span class="sxs-lookup"><span data-stu-id="994f4-378">You can create datasets that are scoped to a pipeline by using the **datasets** property.</span></span> <span data-ttu-id="994f4-379">Esses conjuntos de dados só podem ser usados por atividades dentro deste pipeline, não por atividades em outros pipelines.</span><span class="sxs-lookup"><span data-stu-id="994f4-379">These datasets can only be used by activities within this pipeline, not by activities in other pipelines.</span></span> <span data-ttu-id="994f4-380">O exemplo a seguir define um pipeline com dois conjuntos de dados (InputDataset-rdc e OutputDataset-rdc) a serem usados no pipeline.</span><span class="sxs-lookup"><span data-stu-id="994f4-380">The following example defines a pipeline with two datasets (InputDataset-rdc and OutputDataset-rdc) to be used within the pipeline.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="994f4-381">Há suporte apenas para conjuntos de dados com escopo com pipelines avulsos (em que **pipelineMode** é definido como **OneTime**).</span><span class="sxs-lookup"><span data-stu-id="994f4-381">Scoped datasets are supported only with one-time pipelines (where **pipelineMode** is set to **OneTime**).</span></span> <span data-ttu-id="994f4-382">Confira [Pipeline avulso](data-factory-create-pipelines.md#onetime-pipeline) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="994f4-382">See [Onetime pipeline](data-factory-create-pipelines.md#onetime-pipeline) for details.</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="994f4-383">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="994f4-383">Next steps</span></span>
- <span data-ttu-id="994f4-384">Para obter mais informações sobre pipelines, consulte [Criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="994f4-384">For more information about pipelines, see [Create pipelines](data-factory-create-pipelines.md).</span></span> 
- <span data-ttu-id="994f4-385">Para obter mais informações sobre como os pipelines são agendados e executados, consulte [Agendamento e execução no Azure Data Factory](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="994f4-385">For more information about how pipelines are scheduled and executed, see [Scheduling and execution in Azure Data Factory](data-factory-scheduling-and-execution.md).</span></span> 
