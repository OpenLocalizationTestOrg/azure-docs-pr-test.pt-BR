---
title: Mover dados de/para o Azure Cosmos DB | Microsoft Docs
description: "Saiba como mover dados de/para a coleção Azure Cosmos DB usando o Azure Data Factory"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 7a11c6ade0325b08ad520448bbf82d64a0a555f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="8c106-103">Mover dados de e para o Azure Cosmos DB usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8c106-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="8c106-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de/para o Azure Cosmos DB (API do DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="8c106-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="8c106-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="8c106-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="8c106-106">Você pode copiar dados de qualquer armazenamento de dados de origem com suporte para o Azure Cosmos DB ou do Azure Cosmos DB para qualquer armazenamento de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="8c106-106">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span></span> <span data-ttu-id="8c106-107">Para obter uma lista de repositórios de dados com suporte como fontes ou coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8c106-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8c106-108">O conector do Azure Cosmos DB dá suporte apenas à API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="8c106-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="8c106-109">Para copiar os dados como estão de/para arquivos JSON ou outra coleção do Cosmos DB, confira [Importação/exportação de documentos JSON](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="8c106-109">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="8c106-110">Introdução</span><span class="sxs-lookup"><span data-stu-id="8c106-110">Getting started</span></span>
<span data-ttu-id="8c106-111">Você pode criar um pipeline com uma atividade de cópia que mova dados de/para o Azure Cosmos DB usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="8c106-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="8c106-112">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="8c106-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="8c106-113">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="8c106-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="8c106-114">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="8c106-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8c106-115">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="8c106-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8c106-116">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="8c106-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="8c106-117">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="8c106-117">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="8c106-118">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="8c106-118">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="8c106-119">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="8c106-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8c106-120">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="8c106-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="8c106-121">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="8c106-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="8c106-122">Para obter exemplos com definições de JSON das entidades do Data Factory usadas para copiar dados de/para o Cosmos DB, consulte a seção [Exemplos de JSON](#json-examples) desse artigo.</span><span class="sxs-lookup"><span data-stu-id="8c106-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="8c106-123">As seções a seguir fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas para o Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="8c106-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="8c106-124">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8c106-124">Linked service properties</span></span>
<span data-ttu-id="8c106-125">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c106-125">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span></span>

| <span data-ttu-id="8c106-126">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="8c106-126">**Property**</span></span> | <span data-ttu-id="8c106-127">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8c106-127">**Description**</span></span> | <span data-ttu-id="8c106-128">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="8c106-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8c106-129">type</span><span class="sxs-lookup"><span data-stu-id="8c106-129">type</span></span> |<span data-ttu-id="8c106-130">A propriedade type deve ser definida como: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="8c106-130">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="8c106-131">Sim</span><span class="sxs-lookup"><span data-stu-id="8c106-131">Yes</span></span> |
| <span data-ttu-id="8c106-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="8c106-132">connectionString</span></span> |<span data-ttu-id="8c106-133">Especifique as informações necessárias para se conectar ao banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c106-133">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="8c106-134">Sim</span><span class="sxs-lookup"><span data-stu-id="8c106-134">Yes</span></span> |

<span data-ttu-id="8c106-135">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8c106-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="8c106-136">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8c106-136">Dataset properties</span></span>
<span data-ttu-id="8c106-137">Para obter uma lista completa das seções e propriedades disponíveis para definição de conjuntos de dados, consulte o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="8c106-137">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8c106-138">Seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="8c106-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8c106-139">A seção typeProperties é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="8c106-139">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="8c106-140">A seção typeProperties para o conjunto de dados do tipo **DocumentDbCollection** tem as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="8c106-140">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="8c106-141">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="8c106-141">**Property**</span></span> | <span data-ttu-id="8c106-142">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8c106-142">**Description**</span></span> | <span data-ttu-id="8c106-143">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="8c106-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8c106-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="8c106-144">collectionName</span></span> |<span data-ttu-id="8c106-145">Nome da coleção de documentos do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c106-145">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="8c106-146">Sim</span><span class="sxs-lookup"><span data-stu-id="8c106-146">Yes</span></span> |

<span data-ttu-id="8c106-147">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8c106-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="8c106-148">Esquema do Data Factory</span><span class="sxs-lookup"><span data-stu-id="8c106-148">Schema by Data Factory</span></span>
<span data-ttu-id="8c106-149">Para armazenamentos de dados sem esquema, como o Azure Cosmos DB, o serviço do Data Factory infere o esquema em uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="8c106-149">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="8c106-150">Se você especificar a estrutura dos dados usando a propriedade **structure** na definição de conjunto de dados, o serviço do Data Factory respeitará essa estrutura do esquema.</span><span class="sxs-lookup"><span data-stu-id="8c106-150">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="8c106-151">Nesse caso, se uma linha não contiver um valor de uma coluna, um valor nulo será fornecido para ele.</span><span class="sxs-lookup"><span data-stu-id="8c106-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="8c106-152">Se você não especificar a estrutura dos dados usando a propriedade **structure** na definição de conjunto de dados, o serviço do Data Factory inferirá o esquema usando a primeira linha dos dados.</span><span class="sxs-lookup"><span data-stu-id="8c106-152">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="8c106-153">Nesse caso, se a primeira linha não contiver o esquema completo, algumas colunas estarão ausentes no resultado da operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="8c106-153">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="8c106-154">Portanto, para fontes de dados sem esquema, a prática recomendada é especificar a estrutura de dados usando a propriedade **structure** .</span><span class="sxs-lookup"><span data-stu-id="8c106-154">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="8c106-155">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="8c106-155">Copy activity properties</span></span>
<span data-ttu-id="8c106-156">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, veja o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="8c106-156">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8c106-157">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="8c106-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="8c106-158">A Atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="8c106-158">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="8c106-159">As propriedades disponíveis na seção typeProperties da atividade, por outro lado, variam de acordo com cada tipo de atividade e, no caso de Atividade de cópia, variam dependendo dos tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="8c106-159">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="8c106-160">No caso da Atividade de cópia, quando a fonte é do tipo **DocumentDbCollectionSource**, as seguintes propriedades estão disponíveis na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8c106-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="8c106-161">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="8c106-161">**Property**</span></span> | <span data-ttu-id="8c106-162">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8c106-162">**Description**</span></span> | <span data-ttu-id="8c106-163">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="8c106-163">**Allowed values**</span></span> | <span data-ttu-id="8c106-164">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="8c106-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8c106-165">query</span><span class="sxs-lookup"><span data-stu-id="8c106-165">query</span></span> |<span data-ttu-id="8c106-166">Especifique a consulta para ler dados.</span><span class="sxs-lookup"><span data-stu-id="8c106-166">Specify the query to read data.</span></span> |<span data-ttu-id="8c106-167">Cadeia de consulta com suporte no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c106-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="8c106-168">Exemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="8c106-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="8c106-169">Não</span><span class="sxs-lookup"><span data-stu-id="8c106-169">No</span></span> <br/><br/><span data-ttu-id="8c106-170">Se não for especificada, a instrução SQL executada será: `select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="8c106-170">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="8c106-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="8c106-171">nestingSeparator</span></span> |<span data-ttu-id="8c106-172">Caractere especial para indicar que o documento está aninhado</span><span class="sxs-lookup"><span data-stu-id="8c106-172">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="8c106-173">Qualquer caractere.</span><span class="sxs-lookup"><span data-stu-id="8c106-173">Any character.</span></span> <br/><br/><span data-ttu-id="8c106-174">O Azure Cosmos DB é um repositório NoSQL para documentos JSON, em que estruturas aninhadas são permitidas.</span><span class="sxs-lookup"><span data-stu-id="8c106-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="8c106-175">O Azure Data Factory permite que o usuário indique a hierarquia via nestingSeparator, que é "."</span><span class="sxs-lookup"><span data-stu-id="8c106-175">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="8c106-176">nos exemplos acima.</span><span class="sxs-lookup"><span data-stu-id="8c106-176">in the above examples.</span></span> <span data-ttu-id="8c106-177">Com o separador, a atividade de cópia vai gerar o objeto "Name" com três elementos filhos First, Middle e Last, de acordo com "Name.First", "Name.Middle" e "Name.Last" na definição da tabela.</span><span class="sxs-lookup"><span data-stu-id="8c106-177">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="8c106-178">Não</span><span class="sxs-lookup"><span data-stu-id="8c106-178">No</span></span> |

<span data-ttu-id="8c106-179">**DocumentDbCollectionSink** dá suporte às seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="8c106-179">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="8c106-180">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="8c106-180">**Property**</span></span> | <span data-ttu-id="8c106-181">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="8c106-181">**Description**</span></span> | <span data-ttu-id="8c106-182">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="8c106-182">**Allowed values**</span></span> | <span data-ttu-id="8c106-183">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="8c106-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8c106-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="8c106-184">nestingSeparator</span></span> |<span data-ttu-id="8c106-185">Um caractere especial no nome da coluna de fonte para indicar que esse documento aninhado é necessário.</span><span class="sxs-lookup"><span data-stu-id="8c106-185">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="8c106-186">No exemplo acima: `Name.First` na tabela de saída produz a seguinte estrutura JSON no documento do Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="8c106-186">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="8c106-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="8c106-187">"Name": {</span></span><br/>    <span data-ttu-id="8c106-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="8c106-188">"First": "John"</span></span><br/><span data-ttu-id="8c106-189">},</span><span class="sxs-lookup"><span data-stu-id="8c106-189">},</span></span> |<span data-ttu-id="8c106-190">Caractere que é usado para separar os níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="8c106-190">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="8c106-191">O valor padrão é `.` (ponto).</span><span class="sxs-lookup"><span data-stu-id="8c106-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="8c106-192">Caractere que é usado para separar os níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="8c106-192">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="8c106-193">O valor padrão é `.` (ponto).</span><span class="sxs-lookup"><span data-stu-id="8c106-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="8c106-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8c106-194">writeBatchSize</span></span> |<span data-ttu-id="8c106-195">Número de solicitações paralelas ao serviço Azure Cosmos DB para criar documentos.</span><span class="sxs-lookup"><span data-stu-id="8c106-195">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="8c106-196">Você pode ajustar o desempenho ao copiar dados de/para o Cosmos DB usando essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="8c106-196">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="8c106-197">Você pode esperar um melhor desempenho ao aumentar writeBatchSize, pois mais solicitações paralelas para o Cosmos DB são enviadas.</span><span class="sxs-lookup"><span data-stu-id="8c106-197">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span></span> <span data-ttu-id="8c106-198">No entanto, será necessário evitar a limitação que pode gerar a mensagem de erro: "A taxa de solicitação é grande".</span><span class="sxs-lookup"><span data-stu-id="8c106-198">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="8c106-199">A limitação é decida por uma série de fatores, incluindo o tamanho dos documentos, o número de termos incluídos, a política de indexação da coleção de destino, etc. Para operações de cópia, você pode usar uma coleção melhor (por exemplo, S3) para ter mais taxa de transferência disponível (solicitação de 2.500 unidades/segundo).</span><span class="sxs-lookup"><span data-stu-id="8c106-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="8c106-200">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="8c106-200">Integer</span></span> |<span data-ttu-id="8c106-201">Não (padrão: 5)</span><span class="sxs-lookup"><span data-stu-id="8c106-201">No (default: 5)</span></span> |
| <span data-ttu-id="8c106-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8c106-202">writeBatchTimeout</span></span> |<span data-ttu-id="8c106-203">Tempo de espera para a operação ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="8c106-203">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="8c106-204">timespan</span><span class="sxs-lookup"><span data-stu-id="8c106-204">timespan</span></span><br/><br/> <span data-ttu-id="8c106-205">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="8c106-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="8c106-206">Não</span><span class="sxs-lookup"><span data-stu-id="8c106-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="8c106-207">Importar/Exportar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="8c106-207">Import/Export JSON documents</span></span>
<span data-ttu-id="8c106-208">Usando esse conector do Cosmos DB, você pode facilmente</span><span class="sxs-lookup"><span data-stu-id="8c106-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="8c106-209">Importar documentos JSON de várias fontes para o Cosmos DB, incluindo Blobs do Azure, Azure Data Lake, Sistema de Arquivos local ou outros repositórios com base em arquivos com suporte pelo Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8c106-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="8c106-210">Exportar documentos JSON da coleção do Cosmos DB para vários repositórios com base em arquivo.</span><span class="sxs-lookup"><span data-stu-id="8c106-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="8c106-211">Migrar dados entre duas coleções do Cosmos DB no estado em que se encontram.</span><span class="sxs-lookup"><span data-stu-id="8c106-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="8c106-212">Para atingir essa cópia independente de esquema,</span><span class="sxs-lookup"><span data-stu-id="8c106-212">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="8c106-213">Ao usar o assistente de cópia, marque a opção **"Exportar como estão para arquivos JSON ou uma coleção Cosmos DB"**.</span><span class="sxs-lookup"><span data-stu-id="8c106-213">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="8c106-214">Ao usar a edição de JSON, não especifique a seção "structure" nos conjuntos de dados do Cosmos DB nem a propriedade "nestingSeparator" na fonte/coletor do Cosmos DB na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="8c106-214">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="8c106-215">Para importar/exportar para arquivos JSON, no conjunto de dados do armazenamento de arquivo especifique o tipo de formato, como "JsonFormat," configure "filePattern" e ignore as configurações de formato restantes, consulte a seção [Formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="8c106-215">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="8c106-216">Exemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="8c106-216">JSON examples</span></span>
<span data-ttu-id="8c106-217">Os exemplos a seguir fornecem amostras de definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8c106-217">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8c106-218">Eles mostram como copiar dados de e para o Azure Cosmos DB e Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c106-218">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="8c106-219">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8c106-219">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a><span data-ttu-id="8c106-220">Exemplo: copiar dados do Azure Cosmos DB para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="8c106-220">Example: Copy data from Azure Cosmos DB to Azure Blob</span></span>
<span data-ttu-id="8c106-221">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="8c106-221">The sample below shows:</span></span>

1. <span data-ttu-id="8c106-222">Um serviço vinculado do tipo [DocumentDB](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="8c106-223">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8c106-224">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="8c106-225">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8c106-226">Um [pipeline](data-factory-create-pipelines.md) com Atividade de cópia que usa [DocumentDbCollectionSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8c106-227">O exemplo copia dados no Azure Cosmos DB para o Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c106-227">The sample copies data in Azure Cosmos DB to Azure Blob.</span></span> <span data-ttu-id="8c106-228">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="8c106-228">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="8c106-229">**Serviço vinculado do Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="8c106-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="8c106-230">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="8c106-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="8c106-231">**Conjunto de dados de entrada do Azure DocumentDB:**</span><span class="sxs-lookup"><span data-stu-id="8c106-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="8c106-232">O exemplo pressupõe que você tem uma coleção chamada **Person** em um banco de dados do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c106-232">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="8c106-233">Definir “external”: ”true” e especificar a política externalData informa o serviço Azure Data Factory que essa é uma tabela externa à fábrica de dados e não é produzida por uma atividade nessa fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="8c106-233">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="8c106-234">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="8c106-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8c106-235">Dados são copiados para um novo blob a cada hora com o caminho para o blob que reflete a data e hora específicas com granularidade de hora.</span><span class="sxs-lookup"><span data-stu-id="8c106-235">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="8c106-236">Documento JSON de exemplo na coleção Person em um banco de dados do Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="8c106-236">Sample JSON document in the Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="8c106-237">O Cosmos DB dá suporte a consultas de documentos usando um SQL como sintaxe nos documentos JSON hierárquicos.</span><span class="sxs-lookup"><span data-stu-id="8c106-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="8c106-238">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8c106-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="8c106-239">O pipeline a seguir copia dados da coleção Person no banco de dados no Azure Cosmos DB para um Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c106-239">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span></span> <span data-ttu-id="8c106-240">Como parte da atividade de cópia, os conjuntos de dados de entrada e saída foram especificados.</span><span class="sxs-lookup"><span data-stu-id="8c106-240">As part of the copy activity the input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a><span data-ttu-id="8c106-241">Exemplo: copiar dados do Blob do Azure para o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8c106-241">Example: Copy data from Azure Blob to Azure Cosmos DB</span></span> 
<span data-ttu-id="8c106-242">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="8c106-242">The sample below shows:</span></span>

1. <span data-ttu-id="8c106-243">Um serviço vinculado do tipo [DocumentDB](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="8c106-244">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8c106-245">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8c106-246">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="8c106-247">O [pipeline](data-factory-create-pipelines.md) com a Atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="8c106-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="8c106-248">O exemplo copia dados do Blob do Azure para o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c106-248">The sample copies data from Azure blob to Azure Cosmos DB.</span></span> <span data-ttu-id="8c106-249">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="8c106-249">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="8c106-250">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="8c106-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="8c106-251">**Serviço vinculado do Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="8c106-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="8c106-252">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="8c106-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="8c106-253">**Conjunto de dados de saída do Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="8c106-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="8c106-254">O exemplo copia dados para uma coleção chamada "Person".</span><span class="sxs-lookup"><span data-stu-id="8c106-254">The sample copies data to a collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="8c106-255">O pipeline a seguir copia dados do Blob do Azure para a coleção Person no Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c106-255">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span></span> <span data-ttu-id="8c106-256">Como parte da atividade de cópia, os conjuntos de dados de entrada e saída foram especificados.</span><span class="sxs-lookup"><span data-stu-id="8c106-256">As part of the copy activity the input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="8c106-257">Se a entrada de blob de exemplo for</span><span class="sxs-lookup"><span data-stu-id="8c106-257">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="8c106-258">Então, a saída JSON no Cosmos DB será:</span><span class="sxs-lookup"><span data-stu-id="8c106-258">Then the output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="8c106-259">O Azure Cosmos DB é um repositório NoSQL para documentos JSON, em que estruturas aninhadas são permitidas.</span><span class="sxs-lookup"><span data-stu-id="8c106-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="8c106-260">O Azure Data Factory permite que o usuário indique a hierarquia via **nestingSeparator**, que é "."</span><span class="sxs-lookup"><span data-stu-id="8c106-260">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="8c106-261">neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="8c106-261">in this example.</span></span> <span data-ttu-id="8c106-262">Com o separador, a atividade de cópia vai gerar o objeto "Name" com três elementos filhos First, Middle e Last, de acordo com "Name.First", "Name.Middle" e "Name.Last" na definição da tabela.</span><span class="sxs-lookup"><span data-stu-id="8c106-262">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="8c106-263">Apêndice</span><span class="sxs-lookup"><span data-stu-id="8c106-263">Appendix</span></span>
1. <span data-ttu-id="8c106-264">**Pergunta:** a atividade de cópia dá suporte à atualização de registros existentes?</span><span class="sxs-lookup"><span data-stu-id="8c106-264">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="8c106-265">**Resposta:** Não.</span><span class="sxs-lookup"><span data-stu-id="8c106-265">**Answer:** No.</span></span>
2. <span data-ttu-id="8c106-266">**Pergunta:** como faz uma nova tentativa de uma cópia de banco de dados do Azure Cosmos para tratar já copiados registros?</span><span class="sxs-lookup"><span data-stu-id="8c106-266">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="8c106-267">**Resposta:** se os registros têm um campo "ID" e a operação de cópia tenta inserir um registro com a mesma ID, a operação de cópia gerará um erro.</span><span class="sxs-lookup"><span data-stu-id="8c106-267">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="8c106-268">**Pergunta:** dá suporte a fábrica de dados [intervalo ou o particionamento de dados com base em hash](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="8c106-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="8c106-269">**Resposta:** Não.</span><span class="sxs-lookup"><span data-stu-id="8c106-269">**Answer:** No.</span></span>
4. <span data-ttu-id="8c106-270">**Pergunta:** posso especificar mais de uma coleção de banco de dados do Azure Cosmos para uma tabela?</span><span class="sxs-lookup"><span data-stu-id="8c106-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="8c106-271">**Resposta:** Não.</span><span class="sxs-lookup"><span data-stu-id="8c106-271">**Answer:** No.</span></span> <span data-ttu-id="8c106-272">Somente uma coleção pode ser especificada no momento.</span><span class="sxs-lookup"><span data-stu-id="8c106-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8c106-273">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="8c106-273">Performance and Tuning</span></span>
<span data-ttu-id="8c106-274">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="8c106-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
