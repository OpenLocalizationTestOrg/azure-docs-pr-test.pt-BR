---
title: aaaMove dados na tabela do Azure | Microsoft Docs
description: Saiba como toomove dados para/do armazenamento de tabela do Azure usando o Azure Data Factory.
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
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="f28a6-103">Mover tooand de dados de tabela do Azure usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f28a6-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="f28a6-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de/para o armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28a6-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="f28a6-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="f28a6-106">Você pode copiar dados de qualquer fonte com suporte de dados armazenam tooAzure armazenamento de tabela ou de dados do armazenamento de tabela do Azure tooany suportada coletor armazenam.</span><span class="sxs-lookup"><span data-stu-id="f28a6-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="f28a6-107">Para obter uma lista de repositórios de dados com suporte como origens ou Coletores de atividade de cópia hello, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="f28a6-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="f28a6-108">Introdução</span><span class="sxs-lookup"><span data-stu-id="f28a6-108">Getting started</span></span>
<span data-ttu-id="f28a6-109">Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente de um Armazenamento de Tabelas do Azure usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="f28a6-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="f28a6-110">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="f28a6-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="f28a6-111">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="f28a6-112">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="f28a6-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f28a6-113">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="f28a6-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f28a6-114">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="f28a6-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="f28a6-115">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="f28a6-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="f28a6-116">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="f28a6-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="f28a6-117">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="f28a6-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f28a6-118">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="f28a6-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="f28a6-119">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="f28a6-120">Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um armazenamento de tabela do Azure, consulte [exemplos JSON](#json-examples) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="f28a6-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="f28a6-121">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure armazenamento de tabela:</span><span class="sxs-lookup"><span data-stu-id="f28a6-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="f28a6-122">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="f28a6-122">Linked service properties</span></span>
<span data-ttu-id="f28a6-123">Há dois tipos de serviços vinculados, você pode usar toolink uma fábrica de dados do Azure de tooan de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28a6-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="f28a6-124">São eles: o serviço vinculado **AzureStorage** e o serviço vinculado **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="f28a6-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="f28a6-125">Olá serviço vinculado do armazenamento do Azure fornece a fábrica de dados Olá com acesso global toohello armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28a6-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="f28a6-126">Enquanto o hello Azure armazenamento SAS (assinatura de acesso compartilhado) vinculado serviço fornece a fábrica de dados Olá com acesso restrito/tempo-limite toohello armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28a6-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="f28a6-127">Não há outras diferenças entre esses dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="f28a6-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="f28a6-128">Escolha o serviço de saudação vinculado que atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="f28a6-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="f28a6-129">Olá seções a seguir fornecem mais detalhes sobre esses dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="f28a6-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="f28a6-130">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="f28a6-130">Dataset properties</span></span>
<span data-ttu-id="f28a6-131">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f28a6-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f28a6-132">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="f28a6-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f28a6-133">seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="f28a6-134">Olá **typeProperties** seção de conjunto de dados de saudação do tipo **AzureTable** tem Olá propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="f28a6-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="f28a6-135">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f28a6-135">Property</span></span> | <span data-ttu-id="f28a6-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="f28a6-136">Description</span></span> | <span data-ttu-id="f28a6-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f28a6-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f28a6-138">tableName</span><span class="sxs-lookup"><span data-stu-id="f28a6-138">tableName</span></span> |<span data-ttu-id="f28a6-139">Nome da tabela de saudação na instância de banco de dados de tabela do Azure Olá que serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="f28a6-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="f28a6-140">Sim.</span><span class="sxs-lookup"><span data-stu-id="f28a6-140">Yes.</span></span> <span data-ttu-id="f28a6-141">Quando um nome de tabela é especificado sem um azureTableSourceQuery, todos os registros da tabela de saudação são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="f28a6-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="f28a6-142">Se um azureTableSourceQuery também for especificado, registros da tabela de saudação que atenda a consulta de saudação são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="f28a6-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="f28a6-143">Esquema do Data Factory</span><span class="sxs-lookup"><span data-stu-id="f28a6-143">Schema by Data Factory</span></span>
<span data-ttu-id="f28a6-144">Para repositórios de dados sem esquema como tabelas do Azure, Olá serviço da fábrica de dados infere o esquema Olá em uma saudação maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="f28a6-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="f28a6-145">Se você especificar a estrutura de saudação de dados usando Olá **estrutura** propriedade na definição de conjunto de dados hello, Olá serviço da fábrica de dados honra essa estrutura como esquema de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="f28a6-146">Nesse caso, se uma linha não contiver um valor de uma coluna, um valor nulo será fornecido para ele.</span><span class="sxs-lookup"><span data-stu-id="f28a6-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="f28a6-147">Se você não especificar a estrutura de saudação de dados usando Olá **estrutura** propriedade na definição de conjunto de dados hello, Data Factory infere o esquema de saudação usando a primeira linha de saudação nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="f28a6-148">Nesse caso, se a primeira linha de saudação não contém um esquema completo hello, algumas colunas estão ausentes no resultado de saudação da operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="f28a6-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="f28a6-149">Portanto, para fontes de dados sem esquema prática recomendada Olá é toospecify estrutura de saudação de dados usando Olá **estrutura** propriedade.</span><span class="sxs-lookup"><span data-stu-id="f28a6-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="f28a6-150">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="f28a6-150">Copy activity properties</span></span>
<span data-ttu-id="f28a6-151">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f28a6-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f28a6-152">As propriedades, como nome, descrição, conjuntos de dados de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="f28a6-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="f28a6-153">Propriedades disponíveis na seção de typeProperties Olá de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="f28a6-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="f28a6-154">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="f28a6-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="f28a6-155">**AzureTableSource** dá suporte a saudação propriedades typeProperties seção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f28a6-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="f28a6-156">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f28a6-156">Property</span></span> | <span data-ttu-id="f28a6-157">Descrição</span><span class="sxs-lookup"><span data-stu-id="f28a6-157">Description</span></span> | <span data-ttu-id="f28a6-158">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="f28a6-158">Allowed values</span></span> | <span data-ttu-id="f28a6-159">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f28a6-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f28a6-160">AzureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="f28a6-160">azureTableSourceQuery</span></span> |<span data-ttu-id="f28a6-161">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="f28a6-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="f28a6-162">Cadeia de caracteres de consulta de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28a6-162">Azure table query string.</span></span> <span data-ttu-id="f28a6-163">Consulte os exemplos na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="f28a6-163">See examples in hello next section.</span></span> |<span data-ttu-id="f28a6-164">Não.</span><span class="sxs-lookup"><span data-stu-id="f28a6-164">No.</span></span> <span data-ttu-id="f28a6-165">Quando um nome de tabela é especificado sem um azureTableSourceQuery, todos os registros da tabela de saudação são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="f28a6-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="f28a6-166">Se um azureTableSourceQuery também for especificado, registros da tabela de saudação que atenda a consulta de saudação são copiados toohello destino.</span><span class="sxs-lookup"><span data-stu-id="f28a6-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="f28a6-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="f28a6-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="f28a6-168">Indique se a exceção de Olá de assimilação da tabela não existe.</span><span class="sxs-lookup"><span data-stu-id="f28a6-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="f28a6-169">TRUE</span><span class="sxs-lookup"><span data-stu-id="f28a6-169">TRUE</span></span><br/><span data-ttu-id="f28a6-170">FALSE</span><span class="sxs-lookup"><span data-stu-id="f28a6-170">FALSE</span></span> |<span data-ttu-id="f28a6-171">Não</span><span class="sxs-lookup"><span data-stu-id="f28a6-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="f28a6-172">Exemplos do azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="f28a6-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="f28a6-173">Se a coluna Tabela do Azure é do tipo cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="f28a6-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="f28a6-174">Se a coluna Tabela do Azure é do tipo datetime:</span><span class="sxs-lookup"><span data-stu-id="f28a6-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="f28a6-175">**AzureTableSink** dá suporte a saudação propriedades typeProperties seção a seguir:</span><span class="sxs-lookup"><span data-stu-id="f28a6-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="f28a6-176">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f28a6-176">Property</span></span> | <span data-ttu-id="f28a6-177">Descrição</span><span class="sxs-lookup"><span data-stu-id="f28a6-177">Description</span></span> | <span data-ttu-id="f28a6-178">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="f28a6-178">Allowed values</span></span> | <span data-ttu-id="f28a6-179">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f28a6-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f28a6-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="f28a6-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="f28a6-181">Partição chave valor padrão que pode ser usado pelo coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="f28a6-182">Um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f28a6-182">A string value.</span></span> |<span data-ttu-id="f28a6-183">Não</span><span class="sxs-lookup"><span data-stu-id="f28a6-183">No</span></span> |
| <span data-ttu-id="f28a6-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="f28a6-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="f28a6-185">Especifique o nome da coluna Olá cujos valores são usados como chaves de partição.</span><span class="sxs-lookup"><span data-stu-id="f28a6-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="f28a6-186">Se não especificado, AzureTableDefaultPartitionKeyValue será usado como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="f28a6-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="f28a6-187">Um nome de coluna.</span><span class="sxs-lookup"><span data-stu-id="f28a6-187">A column name.</span></span> |<span data-ttu-id="f28a6-188">Não</span><span class="sxs-lookup"><span data-stu-id="f28a6-188">No</span></span> |
| <span data-ttu-id="f28a6-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="f28a6-189">azureTableRowKeyName</span></span> |<span data-ttu-id="f28a6-190">Especifique o nome da coluna Olá cujos valores de coluna são usados como chave de linha.</span><span class="sxs-lookup"><span data-stu-id="f28a6-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="f28a6-191">Se não especificado, um GUID é usado para cada linha.</span><span class="sxs-lookup"><span data-stu-id="f28a6-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="f28a6-192">Um nome de coluna.</span><span class="sxs-lookup"><span data-stu-id="f28a6-192">A column name.</span></span> |<span data-ttu-id="f28a6-193">Não</span><span class="sxs-lookup"><span data-stu-id="f28a6-193">No</span></span> |
| <span data-ttu-id="f28a6-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="f28a6-194">azureTableInsertType</span></span> |<span data-ttu-id="f28a6-195">dados de tooinsert de modo de saudação na tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28a6-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="f28a6-196">Essa propriedade controla se as linhas existentes na tabela de saída de hello com correspondência de chaves de partição e de linha têm seus valores substituídos ou mesclados.</span><span class="sxs-lookup"><span data-stu-id="f28a6-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="f28a6-197">toolearn sobre como essas configurações (mesclagem e substituir) funcionam, consulte [inserir ou mesclar entidade](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [inserir ou substituir entidade](https://msdn.microsoft.com/library/azure/hh452242.aspx) tópicos.</span><span class="sxs-lookup"><span data-stu-id="f28a6-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="f28a6-198">Essa configuração se aplica no nível de linha hello, não os nível de tabela Olá, e nenhuma opção exclui linhas na tabela de saída de saudação que não existem na entrada hello.</span><span class="sxs-lookup"><span data-stu-id="f28a6-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="f28a6-199">mesclar (padrão)</span><span class="sxs-lookup"><span data-stu-id="f28a6-199">merge (default)</span></span><br/><span data-ttu-id="f28a6-200">substituir</span><span class="sxs-lookup"><span data-stu-id="f28a6-200">replace</span></span> |<span data-ttu-id="f28a6-201">Não</span><span class="sxs-lookup"><span data-stu-id="f28a6-201">No</span></span> |
| <span data-ttu-id="f28a6-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="f28a6-202">writeBatchSize</span></span> |<span data-ttu-id="f28a6-203">Insere dados em Olá tabela do Azure quando Olá writeBatchSize ou writeBatchTimeout é atingido.</span><span class="sxs-lookup"><span data-stu-id="f28a6-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="f28a6-204">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="f28a6-204">Integer (number of rows)</span></span> |<span data-ttu-id="f28a6-205">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="f28a6-205">No (default: 10000)</span></span> |
| <span data-ttu-id="f28a6-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="f28a6-206">writeBatchTimeout</span></span> |<span data-ttu-id="f28a6-207">Insere dados na Olá tabela do Azure quando Olá writeBatchSize ou writeBatchTimeout é atingido</span><span class="sxs-lookup"><span data-stu-id="f28a6-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="f28a6-208">timespan</span><span class="sxs-lookup"><span data-stu-id="f28a6-208">timespan</span></span><br/><br/><span data-ttu-id="f28a6-209">Exemplo: "00:20:00" (20 minutos)</span><span class="sxs-lookup"><span data-stu-id="f28a6-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="f28a6-210">Não (valor de tempo limite padrão de cliente de toostorage padrão 90 segundos)</span><span class="sxs-lookup"><span data-stu-id="f28a6-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="f28a6-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="f28a6-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="f28a6-212">Mapear uma coluna de destino do código-fonte coluna tooa usando a propriedade JSON do tradutor Olá antes que você pode usar a coluna de destino hello como Olá azureTablePartitionKeyName.</span><span class="sxs-lookup"><span data-stu-id="f28a6-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="f28a6-213">Em Olá exemplo a seguir, a coluna de origem DivisionID é mapeada toohello coluna de destino: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="f28a6-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="f28a6-214">Olá DivisionID é especificado como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="f28a6-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="f28a6-215">Exemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="f28a6-215">JSON examples</span></span>
<span data-ttu-id="f28a6-216">Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f28a6-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f28a6-217">Eles mostram como toocopy tooand de dados do armazenamento de tabela do Azure e banco de dados de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28a6-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="f28a6-218">No entanto, os dados podem ser copiados **diretamente** de qualquer um dos Olá fontes tooany de Coletores de saudação com suporte.</span><span class="sxs-lookup"><span data-stu-id="f28a6-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="f28a6-219">Para obter mais informações, consulte a seção de hello "e formatos de armazenamentos de dados com suporte" em [mover dados usando a atividade de cópia](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f28a6-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="f28a6-220">Exemplo: Copiar dados de tabela do Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="f28a6-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="f28a6-221">Olá mostra de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f28a6-221">hello following sample shows:</span></span>

1. <span data-ttu-id="f28a6-222">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabela e blob).</span><span class="sxs-lookup"><span data-stu-id="f28a6-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="f28a6-223">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f28a6-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="f28a6-224">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f28a6-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="f28a6-225">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [AzureTableSource](#activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f28a6-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f28a6-226">exemplo Hello copia os dados pertencentes a partição padrão de toohello em um blob de tooa de tabela do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f28a6-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="f28a6-227">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="f28a6-228">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f28a6-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="f28a6-229">O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="f28a6-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="f28a6-230">Para Olá primeiro, você especificar a cadeia de caracteres de conexão de saudação que inclui a chave da conta hello e hello mais recente, você especificar Olá Uri de assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="f28a6-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="f28a6-231">Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f28a6-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="f28a6-232">**Conjunto de dados de entrada da Tabela do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f28a6-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="f28a6-233">exemplo Hello pressupõe que você tenha criado uma tabela "MyTable" na tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28a6-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="f28a6-234">Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="f28a6-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="f28a6-235">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f28a6-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f28a6-236">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="f28a6-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f28a6-237">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="f28a6-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f28a6-238">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="f28a6-239">**Atividade de cópia em um pipeline com AzureTableSource e BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="f28a6-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="f28a6-240">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f28a6-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="f28a6-241">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**AzureTableSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f28a6-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="f28a6-242">consulta SQL Olá especificada com **AzureTableSourceQuery** propriedade seleciona dados da saudação da partição padrão de saudação toocopy cada hora.</span><span class="sxs-lookup"><span data-stu-id="f28a6-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="f28a6-243">Exemplo: Copiar dados de Blob do Azure tooAzure tabela</span><span class="sxs-lookup"><span data-stu-id="f28a6-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="f28a6-244">Olá mostra de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f28a6-244">hello following sample shows:</span></span>

1. <span data-ttu-id="f28a6-245">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabela e blob)</span><span class="sxs-lookup"><span data-stu-id="f28a6-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="f28a6-246">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f28a6-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="f28a6-247">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f28a6-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="f28a6-248">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f28a6-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="f28a6-249">exemplo Hello copia dados de série de tempo de uma tabela do Azure de tooan de BLOBs do Azure por hora.</span><span class="sxs-lookup"><span data-stu-id="f28a6-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="f28a6-250">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="f28a6-251">**Serviço de armazenamento vinculado do Azure (para Tabela e Blob do Azure):**</span><span class="sxs-lookup"><span data-stu-id="f28a6-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="f28a6-252">O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="f28a6-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="f28a6-253">Para Olá primeiro, você especificar a cadeia de caracteres de conexão de saudação que inclui a chave da conta hello e hello mais recente, você especificar Olá Uri de assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="f28a6-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="f28a6-254">Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f28a6-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="f28a6-255">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f28a6-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="f28a6-256">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="f28a6-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f28a6-257">Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="f28a6-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f28a6-258">caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="f28a6-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="f28a6-259">"externo": "verdadeira" configuração informa o serviço de fábrica de dados de Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="f28a6-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="f28a6-260">**Conjunto de dados de saída de Tabela do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f28a6-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="f28a6-261">exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" na tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="f28a6-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="f28a6-262">Criar uma tabela do Azure com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello.</span><span class="sxs-lookup"><span data-stu-id="f28a6-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="f28a6-263">Novas linhas são adicionadas a tabela de toohello a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f28a6-263">New rows are added toohello table every hour.</span></span>

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

<span data-ttu-id="f28a6-264">**Atividade de cópia em um pipeline com BlobSource e AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="f28a6-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="f28a6-265">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f28a6-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="f28a6-266">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="f28a6-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="f28a6-267">Mapeamento de tipo de Tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="f28a6-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="f28a6-268">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f28a6-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="f28a6-269">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="f28a6-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="f28a6-270">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="f28a6-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="f28a6-271">Ao mover dados muito & da tabela do Azure, Olá após [mapeamentos definidos pelo serviço de tabela do Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) são usados com o tipo de too.NET de tipos do OData de tabela do Azure e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="f28a6-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="f28a6-272">Tipo de dados OData</span><span class="sxs-lookup"><span data-stu-id="f28a6-272">OData Data Type</span></span> | <span data-ttu-id="f28a6-273">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="f28a6-273">.NET Type</span></span> | <span data-ttu-id="f28a6-274">Detalhes</span><span class="sxs-lookup"><span data-stu-id="f28a6-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f28a6-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="f28a6-275">Edm.Binary</span></span> |<span data-ttu-id="f28a6-276">byte[]</span><span class="sxs-lookup"><span data-stu-id="f28a6-276">byte[]</span></span> |<span data-ttu-id="f28a6-277">Uma matriz de bytes de too64 KB.</span><span class="sxs-lookup"><span data-stu-id="f28a6-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="f28a6-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="f28a6-278">Edm.Boolean</span></span> |<span data-ttu-id="f28a6-279">bool</span><span class="sxs-lookup"><span data-stu-id="f28a6-279">bool</span></span> |<span data-ttu-id="f28a6-280">Um valor booliano.</span><span class="sxs-lookup"><span data-stu-id="f28a6-280">A Boolean value.</span></span> |
| <span data-ttu-id="f28a6-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="f28a6-281">Edm.DateTime</span></span> |<span data-ttu-id="f28a6-282">DateTime</span><span class="sxs-lookup"><span data-stu-id="f28a6-282">DateTime</span></span> |<span data-ttu-id="f28a6-283">Um valor de 64 bits expressado como Tempo Universal Coordenado (UTC).</span><span class="sxs-lookup"><span data-stu-id="f28a6-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="f28a6-284">Olá suporte para DateTime intervalo começa de 12:00 meia-noite de 1º de janeiro de 1601 D.C.</span><span class="sxs-lookup"><span data-stu-id="f28a6-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="f28a6-285">(C.E.), UTC.</span><span class="sxs-lookup"><span data-stu-id="f28a6-285">(C.E.), UTC.</span></span> <span data-ttu-id="f28a6-286">intervalo de saudação termina em 31 de dezembro de 9999.</span><span class="sxs-lookup"><span data-stu-id="f28a6-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="f28a6-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="f28a6-287">Edm.Double</span></span> |<span data-ttu-id="f28a6-288">double</span><span class="sxs-lookup"><span data-stu-id="f28a6-288">double</span></span> |<span data-ttu-id="f28a6-289">Um valor de ponto flutuante de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="f28a6-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="f28a6-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="f28a6-290">Edm.Guid</span></span> |<span data-ttu-id="f28a6-291">Guid</span><span class="sxs-lookup"><span data-stu-id="f28a6-291">Guid</span></span> |<span data-ttu-id="f28a6-292">Um identificador global exclusivo de 128 bits.</span><span class="sxs-lookup"><span data-stu-id="f28a6-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="f28a6-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="f28a6-293">Edm.Int32</span></span> |<span data-ttu-id="f28a6-294">Int32</span><span class="sxs-lookup"><span data-stu-id="f28a6-294">Int32</span></span> |<span data-ttu-id="f28a6-295">Um inteiro de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="f28a6-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="f28a6-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="f28a6-296">Edm.Int64</span></span> |<span data-ttu-id="f28a6-297">Int64</span><span class="sxs-lookup"><span data-stu-id="f28a6-297">Int64</span></span> |<span data-ttu-id="f28a6-298">Um inteiro de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="f28a6-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="f28a6-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="f28a6-299">Edm.String</span></span> |<span data-ttu-id="f28a6-300">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f28a6-300">String</span></span> |<span data-ttu-id="f28a6-301">Um valor codificado em UTF-16.</span><span class="sxs-lookup"><span data-stu-id="f28a6-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="f28a6-302">Valores de cadeia de caracteres podem ser up too64 KB.</span><span class="sxs-lookup"><span data-stu-id="f28a6-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="f28a6-303">Exemplo de conversão de tipo</span><span class="sxs-lookup"><span data-stu-id="f28a6-303">Type Conversion Sample</span></span>
<span data-ttu-id="f28a6-304">saudação de exemplo a seguir é copiar dados de uma tabela de tooAzure de BLOBs do Azure com conversões de tipo.</span><span class="sxs-lookup"><span data-stu-id="f28a6-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="f28a6-305">Suponha que o conjunto de dados de Blob hello está em formato CSV e contém três colunas.</span><span class="sxs-lookup"><span data-stu-id="f28a6-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="f28a6-306">Um deles é uma coluna de data e hora com um formato de data e hora personalizado usando nomes abreviados de francês para o dia da semana hello.</span><span class="sxs-lookup"><span data-stu-id="f28a6-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="f28a6-307">Define o conjunto de dados de fonte de Blob de saudação da seguinte maneira juntamente com definições de tipo para colunas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f28a6-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

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
<span data-ttu-id="f28a6-308">Dado o mapeamento de tipo de saudação de too.NET de tipo de OData de tabela do Azure, você deve definir tabela Olá na tabela do Azure com hello esquema a seguir.</span><span class="sxs-lookup"><span data-stu-id="f28a6-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="f28a6-309">**Esquema da tabela do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f28a6-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="f28a6-310">Nome da coluna</span><span class="sxs-lookup"><span data-stu-id="f28a6-310">Column name</span></span> | <span data-ttu-id="f28a6-311">Tipo</span><span class="sxs-lookup"><span data-stu-id="f28a6-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="f28a6-312">userid</span><span class="sxs-lookup"><span data-stu-id="f28a6-312">userid</span></span> |<span data-ttu-id="f28a6-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="f28a6-313">Edm.Int64</span></span> |
| <span data-ttu-id="f28a6-314">name</span><span class="sxs-lookup"><span data-stu-id="f28a6-314">name</span></span> |<span data-ttu-id="f28a6-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="f28a6-315">Edm.String</span></span> |
| <span data-ttu-id="f28a6-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="f28a6-316">lastlogindate</span></span> |<span data-ttu-id="f28a6-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="f28a6-317">Edm.DateTime</span></span> |

<span data-ttu-id="f28a6-318">Em seguida, defina o conjunto de dados de tabela do Azure Olá da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="f28a6-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="f28a6-319">Seção de "structure" toospecify com informações de tipo hello não é necessário porque as informações de tipo de saudação já estão especificadas em Olá subjacente de repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="f28a6-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

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

<span data-ttu-id="f28a6-320">Nesse caso, a fábrica de dados automaticamente conversões de tipo incluindo o campo de data/hora de saudação com formato de data e hora personalizado hello usando a cultura de hello "fr-fr" quando a movimentação de dados de Blob tooAzure tabela.</span><span class="sxs-lookup"><span data-stu-id="f28a6-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="f28a6-321">colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f28a6-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f28a6-322">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="f28a6-322">Performance and Tuning</span></span>
<span data-ttu-id="f28a6-323">toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias maneiras, consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="f28a6-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
