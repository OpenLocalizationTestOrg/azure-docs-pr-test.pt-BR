---
title: Mover dados de/para a Tabela do Azure | Microsoft Docs
description: Saiba como mover dados para/do Armazenamento de Tabela do Azure usando o Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 792a551ae3dae46c503e5f0dda74cd0ac3a69c3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="29765-103">Mover dados para e da Tabela do Azure | Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="29765-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="29765-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados bidirecionalmente no Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="29765-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="29765-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="29765-106">Você pode copiar dados de qualquer repositório de dados de origem com suporte para o Armazenamento de Tabelas do Azure ou do Armazenamento de Tabelas do Azure para qualquer repositório de dados do coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="29765-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="29765-107">Para obter uma lista de repositórios de dados com suporte como fontes ou coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="29765-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="29765-108">Introdução</span><span class="sxs-lookup"><span data-stu-id="29765-108">Getting started</span></span>
<span data-ttu-id="29765-109">Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente de um Armazenamento de Tabelas do Azure usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="29765-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="29765-110">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="29765-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="29765-111">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="29765-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="29765-112">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="29765-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="29765-113">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="29765-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="29765-114">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="29765-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="29765-115">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="29765-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="29765-116">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="29765-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="29765-117">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="29765-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="29765-118">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="29765-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="29765-119">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="29765-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="29765-120">Para obter exemplos com definições de JSON das entidades do Data Factory usadas para copiar dados bidirecionalmente em um Armazenamento de Tabelas do Azure, confira a seção [Exemplos de JSON](#json-examples) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="29765-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="29765-121">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao Armazenamento de Tabelas do Azure:</span><span class="sxs-lookup"><span data-stu-id="29765-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="29765-122">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="29765-122">Linked service properties</span></span>
<span data-ttu-id="29765-123">Existem dois tipos de serviço vinculado que você pode usar para vincular um armazenamento de blobs do Azure a um data factory do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="29765-124">São eles: o serviço vinculado **AzureStorage** e o serviço vinculado **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="29765-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="29765-125">O serviço vinculado do Armazenamento do Azure fornece o data factory com acesso global ao Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="29765-126">Já o serviço vinculado SAS (Assinatura de Acesso Compartilhado) do Armazenamento do Azure fornece o data factory com acesso restrito/associado ao tempo ao Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="29765-127">Não há outras diferenças entre esses dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="29765-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="29765-128">Escolha o serviço vinculado que atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="29765-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="29765-129">As seções a seguir fornecem mais detalhes sobre esses dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="29765-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="29765-130">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="29765-130">Dataset properties</span></span>
<span data-ttu-id="29765-131">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="29765-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="29765-132">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="29765-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="29765-133">A seção typeProperties é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="29765-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="29765-134">A seção **typeProperties** para o conjunto de dados do tipo **AzureTable** tem as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="29765-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="29765-135">Propriedade</span><span class="sxs-lookup"><span data-stu-id="29765-135">Property</span></span> | <span data-ttu-id="29765-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="29765-136">Description</span></span> | <span data-ttu-id="29765-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="29765-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29765-138">tableName</span><span class="sxs-lookup"><span data-stu-id="29765-138">tableName</span></span> |<span data-ttu-id="29765-139">Nome da tabela na instância do Banco de Dados da Tabela do Azure à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="29765-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="29765-140">Sim.</span><span class="sxs-lookup"><span data-stu-id="29765-140">Yes.</span></span> <span data-ttu-id="29765-141">Quando um nome de tabela é especificado sem uma azureTableSourceQuery, todos os registros da tabela são copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="29765-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="29765-142">Se uma azureTableSourceQuery também for especificada, os registros da tabela que atende à consulta são copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="29765-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="29765-143">Esquema do Data Factory</span><span class="sxs-lookup"><span data-stu-id="29765-143">Schema by Data Factory</span></span>
<span data-ttu-id="29765-144">Para armazenamentos de dados sem esquema, como a Tabela do Azure, o serviço do Data Factory infere o esquema usando uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="29765-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="29765-145">Se você especificar a estrutura dos dados usando a propriedade **structure** na definição de conjunto de dados, o serviço do Data Factory respeitará essa estrutura do esquema.</span><span class="sxs-lookup"><span data-stu-id="29765-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="29765-146">Nesse caso, se uma linha não contiver um valor de uma coluna, um valor nulo será fornecido para ele.</span><span class="sxs-lookup"><span data-stu-id="29765-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="29765-147">Se você não especificar a estrutura dos dados usando a propriedade **structure** na definição de conjunto de dados, o Data Factory inferirá o esquema usando a primeira linha dos dados.</span><span class="sxs-lookup"><span data-stu-id="29765-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="29765-148">Nesse caso, se a primeira linha não contém o esquema completo, algumas colunas não estão presentes no resultado da operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="29765-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="29765-149">Portanto, para fontes de dados sem esquema, a prática recomendada é especificar a estrutura de dados usando a propriedade **structure** .</span><span class="sxs-lookup"><span data-stu-id="29765-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="29765-150">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="29765-150">Copy activity properties</span></span>
<span data-ttu-id="29765-151">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="29765-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="29765-152">As propriedades, como nome, descrição, conjuntos de dados de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="29765-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="29765-153">As propriedades disponíveis na seção typeProperties da atividade, por outro lado, variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="29765-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="29765-154">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="29765-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="29765-155">**AzureTableSource** dá suporte às seguintes propriedades na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="29765-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="29765-156">Propriedade</span><span class="sxs-lookup"><span data-stu-id="29765-156">Property</span></span> | <span data-ttu-id="29765-157">Descrição</span><span class="sxs-lookup"><span data-stu-id="29765-157">Description</span></span> | <span data-ttu-id="29765-158">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="29765-158">Allowed values</span></span> | <span data-ttu-id="29765-159">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="29765-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="29765-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="29765-160">azureTableSourceQuery</span></span> |<span data-ttu-id="29765-161">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="29765-161">Use the custom query to read data.</span></span> |<span data-ttu-id="29765-162">Cadeia de caracteres de consulta de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-162">Azure table query string.</span></span> <span data-ttu-id="29765-163">Veja exemplos na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="29765-163">See examples in the next section.</span></span> |<span data-ttu-id="29765-164">Não.</span><span class="sxs-lookup"><span data-stu-id="29765-164">No.</span></span> <span data-ttu-id="29765-165">Quando um nome de tabela é especificado sem uma azureTableSourceQuery, todos os registros da tabela são copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="29765-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="29765-166">Se uma azureTableSourceQuery também for especificada, os registros da tabela que atende à consulta são copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="29765-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="29765-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="29765-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="29765-168">Indique se assimilar a exceção da tabela não existe.</span><span class="sxs-lookup"><span data-stu-id="29765-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="29765-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="29765-169">TRUE</span></span><br/><span data-ttu-id="29765-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="29765-170">FALSE</span></span> |<span data-ttu-id="29765-171">Não</span><span class="sxs-lookup"><span data-stu-id="29765-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="29765-172">Exemplos do azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="29765-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="29765-173">Se a coluna Tabela do Azure é do tipo cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="29765-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="29765-174">Se a coluna Tabela do Azure é do tipo datetime:</span><span class="sxs-lookup"><span data-stu-id="29765-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="29765-175">**AzureTableSink** dá suporte às seguintes propriedades na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="29765-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="29765-176">Propriedade</span><span class="sxs-lookup"><span data-stu-id="29765-176">Property</span></span> | <span data-ttu-id="29765-177">Descrição</span><span class="sxs-lookup"><span data-stu-id="29765-177">Description</span></span> | <span data-ttu-id="29765-178">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="29765-178">Allowed values</span></span> | <span data-ttu-id="29765-179">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="29765-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="29765-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="29765-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="29765-181">Valor de chave de partição padrão que pode ser utilizado pelo coletor.</span><span class="sxs-lookup"><span data-stu-id="29765-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="29765-182">Um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="29765-182">A string value.</span></span> |<span data-ttu-id="29765-183">Não</span><span class="sxs-lookup"><span data-stu-id="29765-183">No</span></span> |
| <span data-ttu-id="29765-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="29765-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="29765-185">Especifique o nome da coluna cujos valores são usados como chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="29765-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="29765-186">Se não especificado, AzureTableDefaultPartitionKeyValue será utilizado como a chave da partição.</span><span class="sxs-lookup"><span data-stu-id="29765-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="29765-187">Um nome de coluna.</span><span class="sxs-lookup"><span data-stu-id="29765-187">A column name.</span></span> |<span data-ttu-id="29765-188">Não</span><span class="sxs-lookup"><span data-stu-id="29765-188">No</span></span> |
| <span data-ttu-id="29765-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="29765-189">azureTableRowKeyName</span></span> |<span data-ttu-id="29765-190">Especifique o nome da coluna cujos valores são usados como chaves de linha.</span><span class="sxs-lookup"><span data-stu-id="29765-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="29765-191">Se não especificado, um GUID é usado para cada linha.</span><span class="sxs-lookup"><span data-stu-id="29765-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="29765-192">Um nome de coluna.</span><span class="sxs-lookup"><span data-stu-id="29765-192">A column name.</span></span> |<span data-ttu-id="29765-193">Não</span><span class="sxs-lookup"><span data-stu-id="29765-193">No</span></span> |
| <span data-ttu-id="29765-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="29765-194">azureTableInsertType</span></span> |<span data-ttu-id="29765-195">O modo para inserir dados na tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="29765-196">Essa propriedade controla se linhas existentes na tabela de saída com a partição correspondente e as chaves de linha terão seus valores substituídos ou mesclados.</span><span class="sxs-lookup"><span data-stu-id="29765-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="29765-197">Para saber mais sobre como essas configurações (mesclagem e substituição) funcionam, consulte os tópicos [Inserir ou Mesclar Entidade](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [Inserir ou Substituir Entidade](https://msdn.microsoft.com/library/azure/hh452242.aspx).</span><span class="sxs-lookup"><span data-stu-id="29765-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="29765-198">Essa configuração se aplica ao nível de linha e não ao nível de tabela e nenhuma das opções excluirá as linhas na tabela de saída que não existirem na entrada.</span><span class="sxs-lookup"><span data-stu-id="29765-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="29765-199">mesclar (padrão)</span><span class="sxs-lookup"><span data-stu-id="29765-199">merge (default)</span></span><br/><span data-ttu-id="29765-200">substituir</span><span class="sxs-lookup"><span data-stu-id="29765-200">replace</span></span> |<span data-ttu-id="29765-201">Não</span><span class="sxs-lookup"><span data-stu-id="29765-201">No</span></span> |
| <span data-ttu-id="29765-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="29765-202">writeBatchSize</span></span> |<span data-ttu-id="29765-203">Insere dados na tabela do Azure quando o writeBatchSize ou writeBatchTimeout for atingido.</span><span class="sxs-lookup"><span data-stu-id="29765-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="29765-204">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="29765-204">Integer (number of rows)</span></span> |<span data-ttu-id="29765-205">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="29765-205">No (default: 10000)</span></span> |
| <span data-ttu-id="29765-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="29765-206">writeBatchTimeout</span></span> |<span data-ttu-id="29765-207">Insere dados na tabela do Azure quando o writeBatchSize ou writeBatchTimeout for atingido</span><span class="sxs-lookup"><span data-stu-id="29765-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="29765-208">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="29765-208">timespan</span></span><br/><br/><span data-ttu-id="29765-209">Exemplo: "00:20:00" (20 minutos)</span><span class="sxs-lookup"><span data-stu-id="29765-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="29765-210">Não (padrão para 90 seg. de valor de tempo padrão de cliente de armazenamento)</span><span class="sxs-lookup"><span data-stu-id="29765-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="29765-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="29765-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="29765-212">Antes de poder usar a coluna de destino como o azureTablePartitionKeyName, será necessário mapear uma coluna de origem para uma coluna de destino usando a propriedade JSON do conversor.</span><span class="sxs-lookup"><span data-stu-id="29765-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="29765-213">No exemplo a seguir, a coluna de origem DivisionID é mapeada para a coluna de destino: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="29765-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="29765-214">DivisionID é especificada como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="29765-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="29765-215">Exemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="29765-215">JSON examples</span></span>
<span data-ttu-id="29765-216">Os exemplos a seguir fornecem amostras de definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="29765-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="29765-217">Tais exemplos mostram como copiar dados de/para o Armazenamento de Tabela do Azure e o Banco de Dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="29765-218">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes para qualquer um dos coletores com suporte.</span><span class="sxs-lookup"><span data-stu-id="29765-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="29765-219">Para obter mais informações, consulte a seção "Formatos e armazenamentos de dados com suporte" em [Mover dados usando a Atividade de Cópia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="29765-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="29765-220">Exemplo: Copiar dados da Tabela do Azure para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="29765-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="29765-221">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="29765-221">The following sample shows:</span></span>

1. <span data-ttu-id="29765-222">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabela e blob).</span><span class="sxs-lookup"><span data-stu-id="29765-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="29765-223">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="29765-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="29765-224">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="29765-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="29765-225">O [pipeline](data-factory-create-pipelines.md) com a Atividade de cópia que usa [AzureTableSource](#activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="29765-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="29765-226">O exemplo copia dados pertencentes à partição padrão em uma tabela do Azure para um blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="29765-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="29765-227">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="29765-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="29765-228">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="29765-228">**Azure storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="29765-229">O Azure Data Factory oferece suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="29765-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="29765-230">Para o primeiro, você especifica a cadeia de conexão que inclui a chave de conta, e para o mais recente, você especifica o URI de SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="29765-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="29765-231">Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="29765-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="29765-232">**Conjunto de dados de entrada da Tabela do Azure:**</span><span class="sxs-lookup"><span data-stu-id="29765-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="29765-233">O exemplo pressupõe que você tenha criado uma tabela "MyTable" na Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="29765-234">Configurar “external”: “true” informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="29765-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
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

<span data-ttu-id="29765-235">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="29765-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="29765-236">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="29765-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="29765-237">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="29765-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="29765-238">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="29765-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="29765-239">**Atividade de cópia em um pipeline com AzureTableSource e BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="29765-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="29765-240">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="29765-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="29765-241">Na definição JSON do pipeline, o tipo **source** está definido como **AzureTableSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="29765-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="29765-242">A consulta SQL especificada com a propriedade **AzureTableSourceQuery** seleciona os dados da partição padrão na última hora a serem copiados.</span><span class="sxs-lookup"><span data-stu-id="29765-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },                
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="29765-243">Exemplo: Copiar dados do Blob do Azure para a Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="29765-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="29765-244">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="29765-244">The following sample shows:</span></span>

1. <span data-ttu-id="29765-245">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabela e blob)</span><span class="sxs-lookup"><span data-stu-id="29765-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="29765-246">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="29765-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="29765-247">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="29765-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="29765-248">O [pipeline](data-factory-create-pipelines.md) com a Atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="29765-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="29765-249">O exemplo copia os dados de série temporal de um blob do Azure para uma tabela do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="29765-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="29765-250">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="29765-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="29765-251">**Serviço de armazenamento vinculado do Azure (para Tabela e Blob do Azure):**</span><span class="sxs-lookup"><span data-stu-id="29765-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="29765-252">O Azure Data Factory oferece suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="29765-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="29765-253">Para o primeiro, você especifica a cadeia de conexão que inclui a chave de conta, e para o mais recente, você especifica o URI de SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="29765-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="29765-254">Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="29765-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="29765-255">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="29765-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="29765-256">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="29765-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="29765-257">O caminho de pasta e nome de arquivo para o blob são avaliados dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="29765-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="29765-258">O caminho da pasta usa parte da hora de início do dia, mês e ano e o nome de arquivo usa a parte da hora de início.</span><span class="sxs-lookup"><span data-stu-id="29765-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="29765-259">A configuração "external": "true" informa o serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="29765-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
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

<span data-ttu-id="29765-260">**Conjunto de dados de saída de Tabela do Azure:**</span><span class="sxs-lookup"><span data-stu-id="29765-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="29765-261">O exemplo copia dados para uma tabela chamada "MyTable" na Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="29765-262">Crie uma tabela do Azure com o mesmo número de colunas que você espera que o arquivo CSV de Blob contenha.</span><span class="sxs-lookup"><span data-stu-id="29765-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="29765-263">Novas linhas são adicionadas à tabela a cada hora.</span><span class="sxs-lookup"><span data-stu-id="29765-263">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="29765-264">**Atividade de cópia em um pipeline com BlobSource e AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="29765-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="29765-265">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="29765-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="29765-266">Na definição JSON do pipeline, o tipo **source** está definido como **BlobSource** e o tipo **sink** está definido como **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="29765-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
          }
        },
        "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },                        
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="29765-267">Mapeamento de tipo de Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="29765-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="29765-268">Como mencionado no artigo sobre as [atividades de movimentação de dados](data-factory-data-movement-activities.md) , a atividade de Cópia executa conversões automáticas dos tipos de fonte nos tipos de coletor com a seguinte abordagem de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="29765-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="29765-269">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="29765-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="29765-270">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="29765-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="29765-271">Quando dados forem movidos para e da Tabela do Azure, os seguintes [mapeamentos definidos pelo serviço Tabela do Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) serão usados nos tipos OData da Tabela do Azure para o tipo .NET e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="29765-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="29765-272">Tipo de dados OData</span><span class="sxs-lookup"><span data-stu-id="29765-272">OData Data Type</span></span> | <span data-ttu-id="29765-273">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="29765-273">.NET Type</span></span> | <span data-ttu-id="29765-274">Detalhes</span><span class="sxs-lookup"><span data-stu-id="29765-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29765-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="29765-275">Edm.Binary</span></span> |<span data-ttu-id="29765-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="29765-276">byte[]</span></span> |<span data-ttu-id="29765-277">Uma matriz de bytes de até 64 KB.</span><span class="sxs-lookup"><span data-stu-id="29765-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="29765-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="29765-278">Edm.Boolean</span></span> |<span data-ttu-id="29765-279">bool</span><span class="sxs-lookup"><span data-stu-id="29765-279">bool</span></span> |<span data-ttu-id="29765-280">Um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="29765-280">A Boolean value.</span></span> |
| <span data-ttu-id="29765-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="29765-281">Edm.DateTime</span></span> |<span data-ttu-id="29765-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="29765-282">DateTime</span></span> |<span data-ttu-id="29765-283">Um valor de 64 bits expressado como Tempo Universal Coordenado (UTC).</span><span class="sxs-lookup"><span data-stu-id="29765-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="29765-284">O intervalo de data e hora com suporte começa à 00:00 de 1º de janeiro de 1601 D.C.</span><span class="sxs-lookup"><span data-stu-id="29765-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="29765-285">(C.E.), UTC.</span><span class="sxs-lookup"><span data-stu-id="29765-285">(C.E.), UTC.</span></span> <span data-ttu-id="29765-286">O intervalo termina em 31 de dezembro de 9999.</span><span class="sxs-lookup"><span data-stu-id="29765-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="29765-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="29765-287">Edm.Double</span></span> |<span data-ttu-id="29765-288">double</span><span class="sxs-lookup"><span data-stu-id="29765-288">double</span></span> |<span data-ttu-id="29765-289">Um valor de ponto flutuante de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="29765-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="29765-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="29765-290">Edm.Guid</span></span> |<span data-ttu-id="29765-291">Guid</span><span class="sxs-lookup"><span data-stu-id="29765-291">Guid</span></span> |<span data-ttu-id="29765-292">Um identificador global exclusivo de 128 bits.</span><span class="sxs-lookup"><span data-stu-id="29765-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="29765-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="29765-293">Edm.Int32</span></span> |<span data-ttu-id="29765-294">Int32</span><span class="sxs-lookup"><span data-stu-id="29765-294">Int32</span></span> |<span data-ttu-id="29765-295">Um inteiro de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="29765-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="29765-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="29765-296">Edm.Int64</span></span> |<span data-ttu-id="29765-297">Int64</span><span class="sxs-lookup"><span data-stu-id="29765-297">Int64</span></span> |<span data-ttu-id="29765-298">Um inteiro de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="29765-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="29765-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="29765-299">Edm.String</span></span> |<span data-ttu-id="29765-300">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="29765-300">String</span></span> |<span data-ttu-id="29765-301">Um valor codificado em UTF-16.</span><span class="sxs-lookup"><span data-stu-id="29765-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="29765-302">Valores de cadeia de caracteres podem ter até 64 KB.</span><span class="sxs-lookup"><span data-stu-id="29765-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="29765-303">Exemplo de conversão de tipo</span><span class="sxs-lookup"><span data-stu-id="29765-303">Type Conversion Sample</span></span>
<span data-ttu-id="29765-304">O exemplo a seguir é para copiar dados de um Blob do Azure para Tabela do Azure com conversões de tipo.</span><span class="sxs-lookup"><span data-stu-id="29765-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="29765-305">Suponha que o conjunto de dados de Blob está no formato CSV e contém três colunas.</span><span class="sxs-lookup"><span data-stu-id="29765-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="29765-306">Uma delas é uma coluna de data e hora com um formato de data e hora personalizado usando nomes abreviados em francês para o dia da semana.</span><span class="sxs-lookup"><span data-stu-id="29765-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="29765-307">Defina o conjunto de dados de origem de Blob conforme demonstrado a seguir, juntamente com definições de tipo para as colunas.</span><span class="sxs-lookup"><span data-stu-id="29765-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
<span data-ttu-id="29765-308">Dado o mapeamento de tipo OData da Tabela do Azure para o tipo .NET, você definiria a tabela na Tabela do Azure com o esquema a seguir.</span><span class="sxs-lookup"><span data-stu-id="29765-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="29765-309">**Esquema da tabela do Azure:**</span><span class="sxs-lookup"><span data-stu-id="29765-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="29765-310">Nome da coluna</span><span class="sxs-lookup"><span data-stu-id="29765-310">Column name</span></span> | <span data-ttu-id="29765-311">Tipo</span><span class="sxs-lookup"><span data-stu-id="29765-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="29765-312">userid</span><span class="sxs-lookup"><span data-stu-id="29765-312">userid</span></span> |<span data-ttu-id="29765-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="29765-313">Edm.Int64</span></span> |
| <span data-ttu-id="29765-314">name</span><span class="sxs-lookup"><span data-stu-id="29765-314">name</span></span> |<span data-ttu-id="29765-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="29765-315">Edm.String</span></span> |
| <span data-ttu-id="29765-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="29765-316">lastlogindate</span></span> |<span data-ttu-id="29765-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="29765-317">Edm.DateTime</span></span> |

<span data-ttu-id="29765-318">Em seguida, defina o conjunto de dados de Tabela do Azure conforme demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="29765-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="29765-319">Você não precisa especificar a seção "estrutura" com as informações de tipo, pois o tipo de informação já está especificado no armazenamento de dados subjacente.</span><span class="sxs-lookup"><span data-stu-id="29765-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="29765-320">Nesse caso, o Data Factory fará automaticamente as conversões de tipo, inclusive o campo Data e hora com o formato de data e hora personalizado usando a cultura "fr-fr" ao mover dados de Blob para a Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="29765-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="29765-321">Para mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="29765-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="29765-322">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="29765-322">Performance and Tuning</span></span>
<span data-ttu-id="29765-323">Consulte o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="29765-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
