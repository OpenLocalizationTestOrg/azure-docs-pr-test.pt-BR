---
title: aaaMove dados para/de banco de dados do Azure Cosmos | Microsoft Docs
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
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="cdbe1-103">Mover dados tooand do banco de dados do Cosmos do Azure usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cdbe1-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="cdbe1-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de banco de dados do Azure Cosmos (API de documentos).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="cdbe1-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="cdbe1-106">Você pode copiar dados de qualquer fonte com suporte de dados armazenam tooAzure Cosmos banco de dados ou de dados do banco de dados do Azure Cosmos tooany suportada coletor armazenam.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="cdbe1-107">Para obter uma lista de repositórios de dados com suporte como origens ou Coletores de atividade de cópia hello, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cdbe1-108">O conector do Azure Cosmos DB dá suporte apenas à API do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="cdbe1-109">dados de toocopy como-é de/para arquivos JSON ou outra coleção Cosmos DB, consulte [documentos JSON de importação/exportação](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="cdbe1-110">Introdução</span><span class="sxs-lookup"><span data-stu-id="cdbe1-110">Getting started</span></span>
<span data-ttu-id="cdbe1-111">Você pode criar um pipeline com uma atividade de cópia que mova dados de/para o Azure Cosmos DB usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="cdbe1-112">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="cdbe1-113">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="cdbe1-114">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cdbe1-115">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="cdbe1-116">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="cdbe1-117">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="cdbe1-118">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="cdbe1-119">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="cdbe1-120">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="cdbe1-121">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="cdbe1-122">Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de banco de dados do Cosmos, consulte [exemplos JSON](#json-examples) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="cdbe1-123">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específicas tooCosmos banco de dados:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="cdbe1-124">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="cdbe1-124">Linked service properties</span></span>
<span data-ttu-id="cdbe1-125">Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooAzure Cosmos DB vinculado de serviço.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="cdbe1-126">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-126">**Property**</span></span> | <span data-ttu-id="cdbe1-127">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-127">**Description**</span></span> | <span data-ttu-id="cdbe1-128">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cdbe1-129">type</span><span class="sxs-lookup"><span data-stu-id="cdbe1-129">type</span></span> |<span data-ttu-id="cdbe1-130">propriedade de tipo Hello deve ser definida como: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="cdbe1-131">Sim</span><span class="sxs-lookup"><span data-stu-id="cdbe1-131">Yes</span></span> |
| <span data-ttu-id="cdbe1-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="cdbe1-132">connectionString</span></span> |<span data-ttu-id="cdbe1-133">Especifique o banco de dados do banco de dados do Cosmos tooconnect tooAzure as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="cdbe1-134">Sim</span><span class="sxs-lookup"><span data-stu-id="cdbe1-134">Yes</span></span> |

<span data-ttu-id="cdbe1-135">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-135">Example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="cdbe1-136">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="cdbe1-136">Dataset properties</span></span>
<span data-ttu-id="cdbe1-137">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte toohello [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="cdbe1-138">Seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="cdbe1-139">seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="cdbe1-140">Olá typeProperties seção de conjunto de dados de saudação do tipo **DocumentDbCollection** tem Olá propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="cdbe1-141">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-141">**Property**</span></span> | <span data-ttu-id="cdbe1-142">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-142">**Description**</span></span> | <span data-ttu-id="cdbe1-143">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cdbe1-144">collectionName</span><span class="sxs-lookup"><span data-stu-id="cdbe1-144">collectionName</span></span> |<span data-ttu-id="cdbe1-145">Nome da saudação coleção de documentos do banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="cdbe1-146">Sim</span><span class="sxs-lookup"><span data-stu-id="cdbe1-146">Yes</span></span> |

<span data-ttu-id="cdbe1-147">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-147">Example:</span></span>

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
### <a name="schema-by-data-factory"></a><span data-ttu-id="cdbe1-148">Esquema do Data Factory</span><span class="sxs-lookup"><span data-stu-id="cdbe1-148">Schema by Data Factory</span></span>
<span data-ttu-id="cdbe1-149">Para repositórios de dados sem esquema, como o banco de dados do Azure Cosmos, Olá serviço da fábrica de dados infere o esquema Olá em uma saudação maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="cdbe1-150">Se você especificar a estrutura de saudação de dados usando Olá **estrutura** propriedade na definição de conjunto de dados hello, Olá serviço da fábrica de dados honra essa estrutura como esquema de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="cdbe1-151">Nesse caso, se uma linha não contiver um valor de uma coluna, um valor nulo será fornecido para ele.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="cdbe1-152">Se você não especificar a estrutura Olá dos dados usando Olá **estrutura** propriedade na definição de conjunto de dados hello, Olá serviço da fábrica de dados infere o esquema de saudação usando a primeira linha de saudação nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="cdbe1-153">Nesse caso, se a primeira linha de saudação não contém um esquema completo hello, algumas colunas serão ausentes no resultado de saudação da operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="cdbe1-154">Portanto, para fontes de dados sem esquema prática recomendada Olá é toospecify estrutura de saudação de dados usando Olá **estrutura** propriedade.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="cdbe1-155">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="cdbe1-155">Copy activity properties</span></span>
<span data-ttu-id="cdbe1-156">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte toohello [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="cdbe1-157">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="cdbe1-158">Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="cdbe1-159">Propriedades disponíveis na seção de typeProperties Olá de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade e, em caso de atividade de cópia que variam de acordo com os tipos de saudação de origens e coletores.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="cdbe1-160">No caso de atividade de cópia quando a fonte é do tipo **DocumentDbCollectionSource** Olá propriedades a seguir está disponível em **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="cdbe1-161">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-161">**Property**</span></span> | <span data-ttu-id="cdbe1-162">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-162">**Description**</span></span> | <span data-ttu-id="cdbe1-163">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-163">**Allowed values**</span></span> | <span data-ttu-id="cdbe1-164">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cdbe1-165">query</span><span class="sxs-lookup"><span data-stu-id="cdbe1-165">query</span></span> |<span data-ttu-id="cdbe1-166">Especifica Olá consulta tooread dados.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="cdbe1-167">Cadeia de consulta com suporte no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="cdbe1-168">Exemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="cdbe1-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="cdbe1-169">Não</span><span class="sxs-lookup"><span data-stu-id="cdbe1-169">No</span></span> <br/><br/><span data-ttu-id="cdbe1-170">Se não for especificado, Olá instrução SQL executada:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="cdbe1-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="cdbe1-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="cdbe1-171">nestingSeparator</span></span> |<span data-ttu-id="cdbe1-172">Caractere especial tooindicate que Olá documento está aninhado</span><span class="sxs-lookup"><span data-stu-id="cdbe1-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="cdbe1-173">Qualquer caractere.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-173">Any character.</span></span> <br/><br/><span data-ttu-id="cdbe1-174">O Azure Cosmos DB é um repositório NoSQL para documentos JSON, em que estruturas aninhadas são permitidas.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="cdbe1-175">A fábrica de dados do Azure permite que a hierarquia de toodenote de usuário por meio de nestingSeparator, que é "."</span><span class="sxs-lookup"><span data-stu-id="cdbe1-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="cdbe1-176">em hello acima exemplos.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-176">in hello above examples.</span></span> <span data-ttu-id="cdbe1-177">Separador hello, atividade de cópia Olá irá gerar objeto de "Nome" hello com elementos de três filhos too"Name.First primeiro, intermediária e último, acordo", "Name.Middle" e ". Sobrenome" hello definição da tabela.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="cdbe1-178">Não</span><span class="sxs-lookup"><span data-stu-id="cdbe1-178">No</span></span> |

<span data-ttu-id="cdbe1-179">**DocumentDbCollectionSink** dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="cdbe1-180">**Propriedade**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-180">**Property**</span></span> | <span data-ttu-id="cdbe1-181">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-181">**Description**</span></span> | <span data-ttu-id="cdbe1-182">**Valores permitidos**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-182">**Allowed values**</span></span> | <span data-ttu-id="cdbe1-183">**Obrigatório**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cdbe1-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="cdbe1-184">nestingSeparator</span></span> |<span data-ttu-id="cdbe1-185">Um caractere especial em Olá fonte coluna Nome tooindicate que aninhada documento é necessário.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="cdbe1-186">Por exemplo acima: `Name.First` na saída de hello tabela produz Olá estrutura JSON no documento de banco de dados do Cosmos Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="cdbe1-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="cdbe1-187">"Name": {</span></span><br/>    <span data-ttu-id="cdbe1-188">"First": "John"</span><span class="sxs-lookup"><span data-stu-id="cdbe1-188">"First": "John"</span></span><br/><span data-ttu-id="cdbe1-189">},</span><span class="sxs-lookup"><span data-stu-id="cdbe1-189">},</span></span> |<span data-ttu-id="cdbe1-190">Caractere usado tooseparate níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="cdbe1-191">O valor padrão é `.` (ponto).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="cdbe1-192">Caractere usado tooseparate níveis de aninhamento.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="cdbe1-193">O valor padrão é `.` (ponto).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="cdbe1-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="cdbe1-194">writeBatchSize</span></span> |<span data-ttu-id="cdbe1-195">Número de paralelo solicitações tooAzure documentos de toocreate do serviço de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="cdbe1-196">Você pode ajustar o desempenho de saudação ao copiar dados de banco de dados do Cosmos usando essa propriedade.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="cdbe1-197">Você pode esperar um desempenho melhor quando você aumenta writeBatchSize porque mais solicitações paralelas tooCosmos banco de dados são enviados.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="cdbe1-198">No entanto, você precisará tooavoid limitação que pode gerar a mensagem de saudação do erro: "Solicitação de taxa for grande".</span><span class="sxs-lookup"><span data-stu-id="cdbe1-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="cdbe1-199">A limitação é decida por uma série de fatores, incluindo o tamanho dos documentos, o número de termos incluídos, a política de indexação da coleção de destino, etc. Para operações de cópia, você pode usar uma saudação de toohave de coleção (por exemplo, S3) melhor taxa de transferência mais disponível (2.500 solicitação unidades/segundo).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="cdbe1-200">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="cdbe1-200">Integer</span></span> |<span data-ttu-id="cdbe1-201">Não (padrão: 5)</span><span class="sxs-lookup"><span data-stu-id="cdbe1-201">No (default: 5)</span></span> |
| <span data-ttu-id="cdbe1-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="cdbe1-202">writeBatchTimeout</span></span> |<span data-ttu-id="cdbe1-203">Tempo de espera para Olá operação toocomplete antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="cdbe1-204">timespan</span><span class="sxs-lookup"><span data-stu-id="cdbe1-204">timespan</span></span><br/><br/> <span data-ttu-id="cdbe1-205">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="cdbe1-206">Não</span><span class="sxs-lookup"><span data-stu-id="cdbe1-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="cdbe1-207">Importar/Exportar documentos JSON</span><span class="sxs-lookup"><span data-stu-id="cdbe1-207">Import/Export JSON documents</span></span>
<span data-ttu-id="cdbe1-208">Usando esse conector do Cosmos DB, você pode facilmente</span><span class="sxs-lookup"><span data-stu-id="cdbe1-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="cdbe1-209">Importar documentos JSON de várias fontes para o Cosmos DB, incluindo Blobs do Azure, Azure Data Lake, Sistema de Arquivos local ou outros repositórios com base em arquivos com suporte pelo Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="cdbe1-210">Exportar documentos JSON da coleção do Cosmos DB para vários repositórios com base em arquivo.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="cdbe1-211">Migrar dados entre duas coleções do Cosmos DB no estado em que se encontram.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="cdbe1-212">Copiar de tais independentes de esquema tooachieve,</span><span class="sxs-lookup"><span data-stu-id="cdbe1-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="cdbe1-213">Ao usar o Assistente para cópia, marque Olá **"Exportar como-é tooJSON arquivos ou uma coleção de banco de dados do Cosmos"** opção.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="cdbe1-214">Quando usando a edição de JSON, não especifique seção de "structure" hello no conjunto de dados do banco de dados do Cosmos nem a propriedade "nestingSeparator" no banco de dados do Cosmos fonte/coletor na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="cdbe1-215">tooimport de / tooJSON arquivos de exportação, no conjunto de dados de repositório de arquivo hello especificar tipo de formato como "JsonFormat", "filePattern" de configuração e ignorar as configurações de formato Olá rest, consulte [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) seção em detalhes.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="cdbe1-216">Exemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="cdbe1-216">JSON examples</span></span>
<span data-ttu-id="cdbe1-217">Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="cdbe1-218">Eles mostram como toocopy tooand de dados do banco de dados do Azure Cosmos e armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="cdbe1-219">No entanto, os dados podem ser copiados **diretamente** de qualquer um dos Olá fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="cdbe1-220">Exemplo: Dados de cópia do banco de dados do Azure Cosmos tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="cdbe1-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="cdbe1-221">exemplo Hello abaixo mostra:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-221">hello sample below shows:</span></span>

1. <span data-ttu-id="cdbe1-222">Um serviço vinculado do tipo [DocumentDB](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="cdbe1-223">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cdbe1-224">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="cdbe1-225">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="cdbe1-226">Um [pipeline](data-factory-create-pipelines.md) com Atividade de cópia que usa [DocumentDbCollectionSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="cdbe1-227">exemplo Hello copia dados no banco de dados do Azure Cosmos tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="cdbe1-228">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cdbe1-229">**Serviço vinculado do Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-229">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="cdbe1-230">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="cdbe1-231">**Conjunto de dados de entrada do Azure DocumentDB:**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="cdbe1-232">exemplo Hello pressupõe que você tenha uma coleção denominada **pessoa** em um banco de dados do banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="cdbe1-233">Definindo "externo": "true" e especificando externalData informações da política de saudação do Azure Data Factory do serviço tabela Olá toohello externo fábrica de dados e não são produzidos por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="cdbe1-234">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="cdbe1-235">Dados são copiado tooa novo blob a cada hora com caminho Olá blob Olá refletindo Olá data e hora específicas com granularidade de hora.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

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
<span data-ttu-id="cdbe1-236">Documento JSON de exemplo no hello coleção pessoa em um banco de dados do banco de dados do Cosmos:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

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
<span data-ttu-id="cdbe1-237">O Cosmos DB dá suporte a consultas de documentos usando um SQL como sintaxe nos documentos JSON hierárquicos.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="cdbe1-238">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="cdbe1-239">a seguir Olá pipeline copia dados da saudação coleta de pessoa Olá tooan de banco de dados do banco de dados do Azure Cosmos BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="cdbe1-240">Como parte da saudação de atividade de cópia Olá conjuntos de dados de entrada e saídos foi especificados.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

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
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="cdbe1-241">Exemplo: Copiar dados de Blob do Azure tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cdbe1-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="cdbe1-242">exemplo Hello abaixo mostra:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-242">hello sample below shows:</span></span>

1. <span data-ttu-id="cdbe1-243">Um serviço vinculado do tipo [DocumentDB](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="cdbe1-244">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="cdbe1-245">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="cdbe1-246">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="cdbe1-247">O [pipeline](data-factory-create-pipelines.md) com a Atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="cdbe1-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="cdbe1-248">exemplo Hello copia dados de blob do Azure tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="cdbe1-249">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="cdbe1-250">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="cdbe1-251">**Serviço vinculado do Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-251">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="cdbe1-252">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-252">**Azure Blob input dataset:**</span></span>

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
<span data-ttu-id="cdbe1-253">**Conjunto de dados de saída do Azure Cosmos DB:**</span><span class="sxs-lookup"><span data-stu-id="cdbe1-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="cdbe1-254">exemplo Hello copia a coleção de tooa de dados denominada "Pessoa".</span><span class="sxs-lookup"><span data-stu-id="cdbe1-254">hello sample copies data tooa collection named “Person”.</span></span>

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
<span data-ttu-id="cdbe1-255">a seguir Olá pipeline copia dados de Blob do Azure toohello coleta de pessoa Olá Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="cdbe1-256">Como parte da saudação de atividade de cópia Olá conjuntos de dados de entrada e saídos foi especificados.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

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
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
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
<span data-ttu-id="cdbe1-257">Se a entrada de blob de exemplo hello como</span><span class="sxs-lookup"><span data-stu-id="cdbe1-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="cdbe1-258">Olá, em seguida, a saída que será JSON no banco de dados do Cosmos como:</span><span class="sxs-lookup"><span data-stu-id="cdbe1-258">Then hello output JSON in Cosmos DB will be as:</span></span>

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
<span data-ttu-id="cdbe1-259">O Azure Cosmos DB é um repositório NoSQL para documentos JSON, em que estruturas aninhadas são permitidas.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="cdbe1-260">A fábrica de dados do Azure permite que a hierarquia de toodenote de usuário por meio de **nestingSeparator**, que é "."</span><span class="sxs-lookup"><span data-stu-id="cdbe1-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="cdbe1-261">neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-261">in this example.</span></span> <span data-ttu-id="cdbe1-262">Separador hello, atividade de cópia Olá irá gerar objeto de "Nome" hello com elementos de três filhos too"Name.First primeiro, intermediária e último, acordo", "Name.Middle" e ". Sobrenome" hello definição da tabela.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="cdbe1-263">Apêndice</span><span class="sxs-lookup"><span data-stu-id="cdbe1-263">Appendix</span></span>
1. <span data-ttu-id="cdbe1-264">**Pergunta:** Olá a atualização de suporte a atividade de cópia de registros existentes?</span><span class="sxs-lookup"><span data-stu-id="cdbe1-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="cdbe1-265">**Resposta:** Não.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-265">**Answer:** No.</span></span>
2. <span data-ttu-id="cdbe1-266">**Pergunta:** como faz uma nova tentativa de uma cópia tooAzure Cosmos DB para tratar já copiados registros?</span><span class="sxs-lookup"><span data-stu-id="cdbe1-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="cdbe1-267">**Resposta:** se registros têm um campo "ID" e a operação de cópia Olá tenta tooinsert um registro com hello mesmo ID de operação de cópia hello gera um erro.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="cdbe1-268">**Pergunta:** o Data Factory dá suporte ao [intervalo ou particionamento de dados com base em hash](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="cdbe1-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="cdbe1-269">**Resposta:** Não.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-269">**Answer:** No.</span></span>
4. <span data-ttu-id="cdbe1-270">**Pergunta:** posso especificar mais de uma coleção do Azure Cosmos DB para uma tabela?</span><span class="sxs-lookup"><span data-stu-id="cdbe1-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="cdbe1-271">**Resposta:** Não.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-271">**Answer:** No.</span></span> <span data-ttu-id="cdbe1-272">Somente uma coleção pode ser especificada no momento.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="cdbe1-273">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="cdbe1-273">Performance and Tuning</span></span>
<span data-ttu-id="cdbe1-274">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="cdbe1-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
