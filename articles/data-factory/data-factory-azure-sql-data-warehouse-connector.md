---
title: Copiar dados bidirecionalmente no SQL Data Warehouse do Azure | Microsoft Docs
description: Saiba como copiar dados bidirecionalmente no SQL Data Warehouse do Azure usando o Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 8cba89e0947646b498af07aa484511bf07bf7b0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="f457d-103">Copiar dados bidirecionalmente no SQL Data Warehouse do Azure usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f457d-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="f457d-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados bidirecionalmente no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="f457d-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f457d-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="f457d-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="f457d-106">Para obter melhor desempenho, use o PolyBase para carregar dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f457d-106">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f457d-107">A seção [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) (Usar o PolyBase para carregar dados para o Azure SQL Data Warehouse) apresenta os detalhes.</span><span class="sxs-lookup"><span data-stu-id="f457d-107">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="f457d-108">Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="f457d-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="f457d-109">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="f457d-109">Supported scenarios</span></span>
<span data-ttu-id="f457d-110">Você pode copiar dados **de um SQL Data Warehouse do Azure** para os seguintes armazenamentos de dados:</span><span class="sxs-lookup"><span data-stu-id="f457d-110">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="f457d-111">Você pode copiar dados dos armazenamentos de dados a seguir **para um SQL Data Warehouse do Azure**:</span><span class="sxs-lookup"><span data-stu-id="f457d-111">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="f457d-112">Ao copiar dados do SQL Server ou do Banco de Dados SQL do Azure para o SQL Data Warehouse do Azure, se a tabela não existir no repositório de destino, o Data Factory poderá criar a tabela automaticamente no SQL Data Warehouse usando o esquema da tabela no armazenamento de dados de origem.</span><span class="sxs-lookup"><span data-stu-id="f457d-112">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="f457d-113">Consulte [Criação automática de tabela](#auto-table-creation) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f457d-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="f457d-114">Tipos de autenticação com suporte</span><span class="sxs-lookup"><span data-stu-id="f457d-114">Supported authentication type</span></span>
<span data-ttu-id="f457d-115">O conector do SQL Data Warehouse do Azure dá suporte à autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="f457d-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f457d-116">Introdução</span><span class="sxs-lookup"><span data-stu-id="f457d-116">Getting started</span></span>
<span data-ttu-id="f457d-117">Você pode criar um pipeline com uma atividade de cópia que mova dados de um banco de dados bidirecionalmente em um SQL Data Warehouse do Azure usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="f457d-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="f457d-118">A maneira mais fácil de criar um pipeline que copia dados de/para o Azure SQL Data Warehouse é usar o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="f457d-118">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="f457d-119">Consulte o [Tutorial: carregar dados no SQL Data Warehouse com o Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) para ver uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="f457d-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="f457d-120">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="f457d-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f457d-121">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="f457d-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="f457d-122">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="f457d-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="f457d-123">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="f457d-123">Create a **data factory**.</span></span> <span data-ttu-id="f457d-124">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="f457d-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="f457d-125">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="f457d-125">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="f457d-126">Por exemplo, se você está copiando dados de um Armazenamento de Blobs do Azure para um SQL Data Warehouse do Azure, crie dois serviços vinculados para vincular seu SQL Data Warehouse do Azure e sua conta de Armazenamento do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="f457d-126">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="f457d-127">Para propriedades do serviço vinculado que são específicas do SQL Data Warehouse do Azure, consulte a seção [propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-127">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="f457d-128">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="f457d-128">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="f457d-129">No exemplo mencionado na última etapa, você cria um conjunto de dados para especificar o contêiner de blob e a pasta que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="f457d-129">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="f457d-130">Em seguida, você cria outro conjunto de dados para especificar a tabela no SQL Data Warehouse do Azure que contém os dados copiados do Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="f457d-130">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="f457d-131">Para propriedades do conjunto de dados que são específicas do SQL Data Warehouse do Azure, consulte a seção [propriedades do conjunto de dados](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-131">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="f457d-132">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="f457d-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="f457d-133">No exemplo mencionado anteriormente, você usa BlobSource como fonte e SqlDWSink como coletor para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="f457d-133">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="f457d-134">De modo similar, se você estiver copiando do SQL Data Warehouse do Azure para o Armazenamento de Blobs do Azure, você usará SqlDWSource e BlobSink na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="f457d-134">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="f457d-135">Para propriedades da atividade de cópia que são específicas do SQL Data Warehouse do Azure, consulte a seção [propriedades da atividade de cópia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-135">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="f457d-136">Para obter detalhes sobre como usar um armazenamento de dados como uma origem ou um coletor, clique no link na seção anterior para o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f457d-136">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="f457d-137">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="f457d-137">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="f457d-138">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="f457d-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="f457d-139">Para obter exemplos com definições de JSON das entidades do Data Factory usadas para copiar dados bidirecionalmente em um SQL Data Warehouse do Azure, confira a seção [Exemplos de JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f457d-139">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="f457d-140">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao SQL Data Warehouse do Azure:</span><span class="sxs-lookup"><span data-stu-id="f457d-140">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="f457d-141">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="f457d-141">Linked service properties</span></span>
<span data-ttu-id="f457d-142">A tabela a seguir fornece a descrição para elementos JSON específicas para o serviço vinculado do SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="f457d-142">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="f457d-143">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f457d-143">Property</span></span> | <span data-ttu-id="f457d-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="f457d-144">Description</span></span> | <span data-ttu-id="f457d-145">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f457d-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f457d-146">type</span><span class="sxs-lookup"><span data-stu-id="f457d-146">type</span></span> |<span data-ttu-id="f457d-147">A propriedade type deve ser definida como: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="f457d-147">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="f457d-148">Sim</span><span class="sxs-lookup"><span data-stu-id="f457d-148">Yes</span></span> |
| <span data-ttu-id="f457d-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="f457d-149">connectionString</span></span> |<span data-ttu-id="f457d-150">Especifique as informações necessárias para se conectar à instância do SQL Data Warehouse do Azure para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="f457d-150">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="f457d-151">Há suporte somente para autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="f457d-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="f457d-152">Sim</span><span class="sxs-lookup"><span data-stu-id="f457d-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f457d-153">Configure o [Firewall do Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) e o servidor do banco de dados para [permitir que os Serviços do Azure acessem o servidor](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="f457d-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="f457d-154">Além disso, se você estiver copiando os dados para o Azure SQL Data Warehouse de fora do Azure, inclusive a partir das fontes de dados locais com o gateway do data factory, configure o devido intervalo de endereços IP do computador que está enviando os dados para o Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f457d-154">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="f457d-155">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="f457d-155">Dataset properties</span></span>
<span data-ttu-id="f457d-156">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="f457d-156">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f457d-157">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="f457d-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f457d-158">A seção typeProperties é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="f457d-158">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="f457d-159">A seção **typeProperties** do conjunto de dados do tipo **AzureSqlDWTable** tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="f457d-159">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="f457d-160">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f457d-160">Property</span></span> | <span data-ttu-id="f457d-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="f457d-161">Description</span></span> | <span data-ttu-id="f457d-162">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f457d-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f457d-163">tableName</span><span class="sxs-lookup"><span data-stu-id="f457d-163">tableName</span></span> |<span data-ttu-id="f457d-164">Nome da tabela ou exibição no banco de dados SQL Data Warehouse do Azure ao qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="f457d-164">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="f457d-165">Sim</span><span class="sxs-lookup"><span data-stu-id="f457d-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f457d-166">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="f457d-166">Copy activity properties</span></span>
<span data-ttu-id="f457d-167">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f457d-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f457d-168">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="f457d-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="f457d-169">A Atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="f457d-169">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="f457d-170">Por outro lado, as propriedades disponíveis na seção typeProperties da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="f457d-170">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="f457d-171">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="f457d-171">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="f457d-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="f457d-172">SqlDWSource</span></span>
<span data-ttu-id="f457d-173">Quando a fonte é do tipo **SqlDWSource**, as seguintes propriedades estão disponíveis na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="f457d-173">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="f457d-174">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f457d-174">Property</span></span> | <span data-ttu-id="f457d-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="f457d-175">Description</span></span> | <span data-ttu-id="f457d-176">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="f457d-176">Allowed values</span></span> | <span data-ttu-id="f457d-177">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f457d-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f457d-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="f457d-178">sqlReaderQuery</span></span> |<span data-ttu-id="f457d-179">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="f457d-179">Use the custom query to read data.</span></span> |<span data-ttu-id="f457d-180">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="f457d-180">SQL query string.</span></span> <span data-ttu-id="f457d-181">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="f457d-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="f457d-182">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-182">No</span></span> |
| <span data-ttu-id="f457d-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="f457d-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="f457d-184">Nome do procedimento armazenado que lê os dados da tabela de origem.</span><span class="sxs-lookup"><span data-stu-id="f457d-184">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="f457d-185">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="f457d-185">Name of the stored procedure.</span></span> <span data-ttu-id="f457d-186">A última instrução SQL deve ser uma instrução SELECT no procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="f457d-186">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="f457d-187">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-187">No</span></span> |
| <span data-ttu-id="f457d-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="f457d-188">storedProcedureParameters</span></span> |<span data-ttu-id="f457d-189">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="f457d-189">Parameters for the stored procedure.</span></span> |<span data-ttu-id="f457d-190">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="f457d-190">Name/value pairs.</span></span> <span data-ttu-id="f457d-191">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="f457d-191">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="f457d-192">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-192">No</span></span> |

<span data-ttu-id="f457d-193">Se **sqlReaderQuery** for especificado para SqlDWSource, a Atividade de Cópia executará essa consulta na fonte do SQL Data Warehouse do Azure para obter os dados.</span><span class="sxs-lookup"><span data-stu-id="f457d-193">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="f457d-194">Como alternativa, você pode especificar um procedimento armazenado especificando o **sqlReaderStoredProcedureName** e o **storedProcedureParameters** (se o procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="f457d-194">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="f457d-195">Se você não especificar sqlReaderQuery nem sqlReaderStoredProcedureName, as colunas definidas na seção da estrutura do JSON do conjunto de dados serão usadas para compilar uma consulta para executar no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f457d-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f457d-196">Exemplo: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="f457d-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="f457d-197">Se a definição de conjunto de dados não tem a estrutura, todas as colunas serão selecionadas da tabela.</span><span class="sxs-lookup"><span data-stu-id="f457d-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="f457d-198">Exemplo de SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="f457d-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="f457d-199">**A definição do procedimento armazenado:**</span><span class="sxs-lookup"><span data-stu-id="f457d-199">**The stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a><span data-ttu-id="f457d-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="f457d-200">SqlDWSink</span></span>
<span data-ttu-id="f457d-201">**SqlDWSink** dá suporte às seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="f457d-201">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="f457d-202">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f457d-202">Property</span></span> | <span data-ttu-id="f457d-203">Descrição</span><span class="sxs-lookup"><span data-stu-id="f457d-203">Description</span></span> | <span data-ttu-id="f457d-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="f457d-204">Allowed values</span></span> | <span data-ttu-id="f457d-205">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f457d-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f457d-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="f457d-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="f457d-207">Especifique uma consulta da Atividade de Cópia a executar para que os dados de uma fatia específica sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="f457d-207">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="f457d-208">Para obter detalhes, consulte a [seção de repetição](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="f457d-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="f457d-209">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="f457d-209">A query statement.</span></span> |<span data-ttu-id="f457d-210">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-210">No</span></span> |
| <span data-ttu-id="f457d-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="f457d-211">allowPolyBase</span></span> |<span data-ttu-id="f457d-212">Indica se o PolyBase (quando aplicável) deve ser utilizado em vez do mecanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="f457d-212">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="f457d-213">**Usar o PolyBase é a maneira recomendada para carregar dados no SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="f457d-213">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="f457d-214">Confira a seção [Usar o PolyBase para carregar dados no Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) para obter os detalhes e as restrições.</span><span class="sxs-lookup"><span data-stu-id="f457d-214">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="f457d-215">True </span><span class="sxs-lookup"><span data-stu-id="f457d-215">True</span></span> <br/><span data-ttu-id="f457d-216">False (padrão)</span><span class="sxs-lookup"><span data-stu-id="f457d-216">False (default)</span></span> |<span data-ttu-id="f457d-217">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-217">No</span></span> |
| <span data-ttu-id="f457d-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="f457d-218">polyBaseSettings</span></span> |<span data-ttu-id="f457d-219">Um grupo de propriedades que pode ser especificado quando a propriedade **allowPolybase** está definida como **true**.</span><span class="sxs-lookup"><span data-stu-id="f457d-219">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="f457d-220">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-220">No</span></span> |
| <span data-ttu-id="f457d-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="f457d-221">rejectValue</span></span> |<span data-ttu-id="f457d-222">Especifica o número ou o percentual de linhas que podem ser rejeitadas antes de a consulta falhar.</span><span class="sxs-lookup"><span data-stu-id="f457d-222">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="f457d-223">Saiba mais sobre as opções de rejeição do PolyBase na seção **Argumentos** do tópico [CRIAR TABELA EXTERNA (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f457d-223">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="f457d-224">0 (padrão), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="f457d-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="f457d-225">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-225">No</span></span> |
| <span data-ttu-id="f457d-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="f457d-226">rejectType</span></span> |<span data-ttu-id="f457d-227">Especifica se a opção rejectValue é especificada como um valor literal ou um percentual.</span><span class="sxs-lookup"><span data-stu-id="f457d-227">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="f457d-228">Valor (padrão), Percentual</span><span class="sxs-lookup"><span data-stu-id="f457d-228">Value (default), Percentage</span></span> |<span data-ttu-id="f457d-229">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-229">No</span></span> |
| <span data-ttu-id="f457d-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="f457d-230">rejectSampleValue</span></span> |<span data-ttu-id="f457d-231">Determina o número de linhas a serem recuperadas antes de o PolyBase recalcular o percentual de linhas rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="f457d-231">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="f457d-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="f457d-232">1, 2, …</span></span> |<span data-ttu-id="f457d-233">Sim, se **rejectType** for **percentual**</span><span class="sxs-lookup"><span data-stu-id="f457d-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="f457d-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="f457d-234">useTypeDefault</span></span> |<span data-ttu-id="f457d-235">Especifica como tratar valores ausentes nos arquivos de texto delimitados quando PolyBase recupera dados do arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="f457d-235">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="f457d-236">Saiba mais sobre essa propriedade na seção Argumentos em [CRIAR FORMATO DE ARQUIVO EXTERNO (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="f457d-236">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="f457d-237">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="f457d-237">True, False (default)</span></span> |<span data-ttu-id="f457d-238">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-238">No</span></span> |
| <span data-ttu-id="f457d-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="f457d-239">writeBatchSize</span></span> |<span data-ttu-id="f457d-240">Insere dados na tabela SQL quando o tamanho do buffer atinge writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="f457d-240">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="f457d-241">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="f457d-241">Integer (number of rows)</span></span> |<span data-ttu-id="f457d-242">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="f457d-242">No (default: 10000)</span></span> |
| <span data-ttu-id="f457d-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="f457d-243">writeBatchTimeout</span></span> |<span data-ttu-id="f457d-244">Tempo de espera para a operação de inserção em lotes ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="f457d-244">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="f457d-245">timespan</span><span class="sxs-lookup"><span data-stu-id="f457d-245">timespan</span></span><br/><br/> <span data-ttu-id="f457d-246">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="f457d-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="f457d-247">Não</span><span class="sxs-lookup"><span data-stu-id="f457d-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="f457d-248">Exemplo de SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="f457d-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="f457d-249">Use PolyBase to load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f457d-249">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f457d-250">Usar o **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** é uma maneira eficiente de carregar grandes quantidades de dados no SQL Data Warehouse do Azure com alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="f457d-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="f457d-251">Você pode notar um grande ganho na taxa de transferência usando PolyBase em vez do mecanismo BULKINSERT padrão.</span><span class="sxs-lookup"><span data-stu-id="f457d-251">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="f457d-252">Veja [número de referência do desempenho de cópia](data-factory-copy-activity-performance.md#performance-reference) com comparação detalhada.</span><span class="sxs-lookup"><span data-stu-id="f457d-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="f457d-253">Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="f457d-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="f457d-254">Se os dados de origem estiverem no **Blob do Azure ou no Azure Data Lake Store** e o formato for compatível com o PolyBase, você poderá copiar diretamente para o SQL Data Warehouse do Azure usando PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f457d-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="f457d-255">Veja **[Cópia direta usando o PolyBase](#direct-copy-using-polybase)** com detalhes.</span><span class="sxs-lookup"><span data-stu-id="f457d-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="f457d-256">Se o armazenamento de dados de origem e seu formato não tiver suporte originalmente no PolyBase, você poderá usar o recurso **[Cópia em etapas usando o PolyBase](#staged-copy-using-polybase)**.</span><span class="sxs-lookup"><span data-stu-id="f457d-256">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="f457d-257">Ele também fornece uma melhor produtividade convertendo automaticamente os dados em um formato compatível com o PolyBase e armazenando os dados no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f457d-257">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="f457d-258">Em seguida, ele carrega os dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f457d-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="f457d-259">Defina a propriedade `allowPolyBase` como **true**, conforme mostrado no exemplo a seguir para o Azure Data Factory usar o PolyBase para copiar dados para o Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f457d-259">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f457d-260">Quando você definir allowPolyBase para true, poderá especificar determinadas propriedades do PolyBase usando o grupo de propriedades `polyBaseSettings`.</span><span class="sxs-lookup"><span data-stu-id="f457d-260">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="f457d-261">Consulte a seção [SqlDWSink](#SqlDWSink) para obter detalhes sobre as propriedades que você pode usar com polyBaseSettings.</span><span class="sxs-lookup"><span data-stu-id="f457d-261">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="f457d-262">Cópia direta usando o PolyBase</span><span class="sxs-lookup"><span data-stu-id="f457d-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="f457d-263">O SQL Data Warehouse PolyBase dá suporte diretamente ao Blob do Azure e ao Azure Data Lake Store (usando a entidade de serviço) como origem e com os requisitos de formato de arquivo específico.</span><span class="sxs-lookup"><span data-stu-id="f457d-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="f457d-264">Se os dados de origem atenderem aos critérios descritos nesta seção, você poderá copiar diretamente do armazenamento de dados de origem para o Azure SQL Data Warehouse usando o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f457d-264">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="f457d-265">Caso contrário, poderá aproveitar a [Cópia de preparo usando o PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="f457d-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="f457d-266">Para copiar dados do Data Lake Store para o SQL Data Warehouse com eficiência, saiba mais sobre como o [Azure Data Factory torna ainda mais fácil e conveniente revelar informações de dados usando o Data Lake Store com o SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="f457d-266">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="f457d-267">Se os requisitos não forem atendidos, o Azure Data Factory verificará as configurações e automaticamente reverterá para o mecanismo BULKINSERT da movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="f457d-267">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="f457d-268">O **serviço vinculado de origem** é do tipo: **AzureStorage** ou **AzureDataLakeStore com autenticação da entidade de serviço**.</span><span class="sxs-lookup"><span data-stu-id="f457d-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="f457d-269">O **conjunto de dados de entrada** é do tipo: **AzureBlob** ou **AzureDataLakeStore**, e o tipo de formato nas propriedades `type` é **OrcFormat** ou **TextFormat** com as configurações abaixo:</span><span class="sxs-lookup"><span data-stu-id="f457d-269">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="f457d-270">`rowDelimiter` deve ser **\n**.</span><span class="sxs-lookup"><span data-stu-id="f457d-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="f457d-271">`nullValue` é definido como **cadeia de caracteres vazia** ("") ou `treatEmptyAsNull` é definido como **true**.</span><span class="sxs-lookup"><span data-stu-id="f457d-271">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="f457d-272">`encodingName` é definido como **utf-8**, que é o valor **padrão**.</span><span class="sxs-lookup"><span data-stu-id="f457d-272">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="f457d-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` e `skipLineCount` não foram especificados.</span><span class="sxs-lookup"><span data-stu-id="f457d-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="f457d-274">`compression` pode ser **sem compactação**, **GZip** ou **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="f457d-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="f457d-275">Não há uma configuração `skipHeaderLineCount` em **BlobSource** ou **AzureDataLakeStore** para a atividade de cópia no pipeline.</span><span class="sxs-lookup"><span data-stu-id="f457d-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="f457d-276">Não há nenhuma configuração `sliceIdentifierColumnName` em **SqlDWSink** para a atividade de Cópia no pipeline.</span><span class="sxs-lookup"><span data-stu-id="f457d-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="f457d-277">(O PolyBase garante que todos os dados são atualizados ou que nada é atualizado em uma execução única.</span><span class="sxs-lookup"><span data-stu-id="f457d-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="f457d-278">Para obter **repetibilidade**, você pode usar `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="f457d-278">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="f457d-279">Não há nenhum `columnMapping` sendo usado na atividade de Cópia associada.</span><span class="sxs-lookup"><span data-stu-id="f457d-279">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="f457d-280">Cópia de preparo usando o PolyBase</span><span class="sxs-lookup"><span data-stu-id="f457d-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="f457d-281">Quando os dados de origem não atenderem aos critérios introduzidos na seção anterior, você poderá habilitar a cópia dos dados via Armazenamento de Blobs do Azure de preparo provisório (não pode ser Armazenamento Premium).</span><span class="sxs-lookup"><span data-stu-id="f457d-281">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="f457d-282">Neste caso, o Azure Data Factory executa automaticamente transformações nos dados para atender aos requisitos do formato de dados do PolyBase, em seguida, use o PolyBase para carregar os dados no SQL Data Warehouse e, por fim, limpe os dados temporários do Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="f457d-282">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="f457d-283">Confira [Cópia de Preparo](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes sobre como copiar dados por meio de um trabalho de preparo do Blob do Azure em geral.</span><span class="sxs-lookup"><span data-stu-id="f457d-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="f457d-284">Ao copiar dados de um armazenamento de dados local para o SQL Data Warehouse do Azure usando o PolyBase e o preparo, se a versão do Gateway de Gerenciamento de Dados for inferior a 2.4, o JRE (Java Runtime Environment) será necessário no computador do gateway que é usado para transformar os dados de origem em um formato adequado.</span><span class="sxs-lookup"><span data-stu-id="f457d-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="f457d-285">Sugerimos que você faça upgrade do gateway para a versão mais recente para evitar essa dependência.</span><span class="sxs-lookup"><span data-stu-id="f457d-285">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="f457d-286">Para usar esse recurso, crie um [serviço vinculado de Armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) que se refere à Conta de Armazenamento do Azure que tem o armazenamento de blobs provisório, então, especifique as propriedades `enableStaging` e `stagingSettings` para a Atividade de Cópia, como mostrado no código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f457d-286">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="f457d-287">Práticas recomendadas ao usar o PolyBase</span><span class="sxs-lookup"><span data-stu-id="f457d-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="f457d-288">As seções a seguir fornecem práticas recomendadas adicionais àquelas mencionadas em [Práticas recomendadas para o SQL Data Warehouse do Azure](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="f457d-288">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="f457d-289">Permissão de banco de dados obrigatória</span><span class="sxs-lookup"><span data-stu-id="f457d-289">Required database permission</span></span>
<span data-ttu-id="f457d-290">Para usar o PolyBase, é preciso que o usuário que está sendo usado para carregar dados no SQL Data Warehouse tenha a [permissão "CONTROLE"](https://msdn.microsoft.com/library/ms191291.aspx) no banco de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="f457d-290">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="f457d-291">Para isso, adicione esse usuário como um membro da função "db_owner".</span><span class="sxs-lookup"><span data-stu-id="f457d-291">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="f457d-292">Saiba como fazer isso seguindo [esta seção](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="f457d-292">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="f457d-293">Limitação de tamanho da linha e tipo de dados</span><span class="sxs-lookup"><span data-stu-id="f457d-293">Row size and data type limitation</span></span>
<span data-ttu-id="f457d-294">As cargas do Polybase estão limitadas a carregar linhas com menos de **1 MB** e que não podem ser carregadas para VARCHR(MAX), NVARCHAR(MAX) nem VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="f457d-294">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="f457d-295">Confira [aqui](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="f457d-295">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="f457d-296">Caso você tenha dados de origem com linhas maiores que 1 MB, talvez você deseje dividir as tabelas de origem verticalmente em várias pequenas, em que o maior tamanho de linha de cada uma delas não excede o limite.</span><span class="sxs-lookup"><span data-stu-id="f457d-296">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="f457d-297">As tabelas menores podem ser carregadas usando o PolyBase e mescladas no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f457d-297">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="f457d-298">Classe de recursos do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f457d-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="f457d-299">Para obter a melhor produtividade possível, considere atribuir a maior classe de recursos ao usuário que está sendo usado para carregar dados no SQL Data Warehouse por meio do PolyBase.</span><span class="sxs-lookup"><span data-stu-id="f457d-299">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="f457d-300">Saiba como fazer isso seguindo [Alterar um exemplo de classe de recurso de usuário](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="f457d-300">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="f457d-301">tableName no Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f457d-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f457d-302">A tabela a seguir fornece exemplos de como especificar a propriedade **tableName** no conjunto de dados JSON para várias combinações de nome de esquema e de tabela.</span><span class="sxs-lookup"><span data-stu-id="f457d-302">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="f457d-303">Esquema do BD</span><span class="sxs-lookup"><span data-stu-id="f457d-303">DB Schema</span></span> | <span data-ttu-id="f457d-304">Nome da tabela</span><span class="sxs-lookup"><span data-stu-id="f457d-304">Table name</span></span> | <span data-ttu-id="f457d-305">Propriedade JSON tableName</span><span class="sxs-lookup"><span data-stu-id="f457d-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f457d-306">dbo</span><span class="sxs-lookup"><span data-stu-id="f457d-306">dbo</span></span> |<span data-ttu-id="f457d-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="f457d-307">MyTable</span></span> |<span data-ttu-id="f457d-308">MyTable ou dbo.MyTable ou [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="f457d-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="f457d-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="f457d-309">dbo1</span></span> |<span data-ttu-id="f457d-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="f457d-310">MyTable</span></span> |<span data-ttu-id="f457d-311">dbo1.MyTable ou [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="f457d-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="f457d-312">dbo</span><span class="sxs-lookup"><span data-stu-id="f457d-312">dbo</span></span> |<span data-ttu-id="f457d-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="f457d-313">My.Table</span></span> |<span data-ttu-id="f457d-314">[My.Table] ou [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="f457d-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="f457d-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="f457d-315">dbo1</span></span> |<span data-ttu-id="f457d-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="f457d-316">My.Table</span></span> |<span data-ttu-id="f457d-317">[dbo1]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="f457d-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="f457d-318">Se você vir o erro a seguir, pode ser um problema com o valor especificado para a propriedade tableName.</span><span class="sxs-lookup"><span data-stu-id="f457d-318">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="f457d-319">Consulte a tabela para ver a maneira correta de especificar os valores para a propriedade JSON tableName.</span><span class="sxs-lookup"><span data-stu-id="f457d-319">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="f457d-320">Colunas com valores padrão</span><span class="sxs-lookup"><span data-stu-id="f457d-320">Columns with default values</span></span>
<span data-ttu-id="f457d-321">Atualmente, o recurso PolyBase no Data Factory só aceita o mesmo número de colunas da tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="f457d-321">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="f457d-322">Digamos que você tenha uma tabela com quatro colunas e uma delas esteja definida com um valor padrão.</span><span class="sxs-lookup"><span data-stu-id="f457d-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="f457d-323">Os dados de entrada ainda devem conter quatro colunas.</span><span class="sxs-lookup"><span data-stu-id="f457d-323">The input data should still contain four columns.</span></span> <span data-ttu-id="f457d-324">Fornecer um conjunto de dados de entrada com três colunas produziria um erro parecido com a mensagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="f457d-324">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="f457d-325">O valor NULL é uma forma especial do valor padrão.</span><span class="sxs-lookup"><span data-stu-id="f457d-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="f457d-326">Se a coluna for anulável, os dados de entrada (no blob) para essa coluna poderão estar vazios (não poderão estar ausentes no conjunto de dados de entrada).</span><span class="sxs-lookup"><span data-stu-id="f457d-326">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="f457d-327">O PolyBase insere NULL para eles no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f457d-327">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="f457d-328">Criação automática de tabela</span><span class="sxs-lookup"><span data-stu-id="f457d-328">Auto table creation</span></span>
<span data-ttu-id="f457d-329">Se você estiver usando o Assistente de Cópia para copiar dados do SQL Server ou do Banco de Dados SQL do Azure para o SQL Data Warehouse do Azure e a tabela que corresponde à tabela de origem não existir no repositório de destino, o Data Factory poderá criar automaticamente a tabela no data warehouse usando o esquema da tabela de origem.</span><span class="sxs-lookup"><span data-stu-id="f457d-329">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="f457d-330">O Data Factory cria a tabela no repositório de destino com o mesmo nome de tabela no armazenamento de dados de origem.</span><span class="sxs-lookup"><span data-stu-id="f457d-330">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="f457d-331">Os tipos de dados das colunas são escolhidos de acordo com o mapeamento de tipo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f457d-331">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="f457d-332">Se necessário, ele executa conversões de tipo para corrigir todas as incompatibilidades entre os repositórios de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="f457d-332">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="f457d-333">Ele também usa a distribuição de tabelas em um Round Robin.</span><span class="sxs-lookup"><span data-stu-id="f457d-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="f457d-334">Tipo de coluna do Banco de Dados SQL da origem</span><span class="sxs-lookup"><span data-stu-id="f457d-334">Source SQL Database column type</span></span> | <span data-ttu-id="f457d-335">Tipo de coluna do SQL DW de destino (limitação de tamanho)</span><span class="sxs-lookup"><span data-stu-id="f457d-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="f457d-336">int</span><span class="sxs-lookup"><span data-stu-id="f457d-336">Int</span></span> | <span data-ttu-id="f457d-337">int</span><span class="sxs-lookup"><span data-stu-id="f457d-337">Int</span></span> |
| <span data-ttu-id="f457d-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="f457d-338">BigInt</span></span> | <span data-ttu-id="f457d-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="f457d-339">BigInt</span></span> |
| <span data-ttu-id="f457d-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="f457d-340">SmallInt</span></span> | <span data-ttu-id="f457d-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="f457d-341">SmallInt</span></span> |
| <span data-ttu-id="f457d-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="f457d-342">TinyInt</span></span> | <span data-ttu-id="f457d-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="f457d-343">TinyInt</span></span> |
| <span data-ttu-id="f457d-344">Bit</span><span class="sxs-lookup"><span data-stu-id="f457d-344">Bit</span></span> | <span data-ttu-id="f457d-345">Bit</span><span class="sxs-lookup"><span data-stu-id="f457d-345">Bit</span></span> |
| <span data-ttu-id="f457d-346">Decimal</span><span class="sxs-lookup"><span data-stu-id="f457d-346">Decimal</span></span> | <span data-ttu-id="f457d-347">Decimal</span><span class="sxs-lookup"><span data-stu-id="f457d-347">Decimal</span></span> |
| <span data-ttu-id="f457d-348">Numérico</span><span class="sxs-lookup"><span data-stu-id="f457d-348">Numeric</span></span> | <span data-ttu-id="f457d-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="f457d-349">Decimal</span></span> |
| <span data-ttu-id="f457d-350">Float</span><span class="sxs-lookup"><span data-stu-id="f457d-350">Float</span></span> | <span data-ttu-id="f457d-351">Float</span><span class="sxs-lookup"><span data-stu-id="f457d-351">Float</span></span> |
| <span data-ttu-id="f457d-352">Money</span><span class="sxs-lookup"><span data-stu-id="f457d-352">Money</span></span> | <span data-ttu-id="f457d-353">Money</span><span class="sxs-lookup"><span data-stu-id="f457d-353">Money</span></span> |
| <span data-ttu-id="f457d-354">Real</span><span class="sxs-lookup"><span data-stu-id="f457d-354">Real</span></span> | <span data-ttu-id="f457d-355">Real</span><span class="sxs-lookup"><span data-stu-id="f457d-355">Real</span></span> |
| <span data-ttu-id="f457d-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="f457d-356">SmallMoney</span></span> | <span data-ttu-id="f457d-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="f457d-357">SmallMoney</span></span> |
| <span data-ttu-id="f457d-358">Binário</span><span class="sxs-lookup"><span data-stu-id="f457d-358">Binary</span></span> | <span data-ttu-id="f457d-359">Binário</span><span class="sxs-lookup"><span data-stu-id="f457d-359">Binary</span></span> |
| <span data-ttu-id="f457d-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="f457d-360">Varbinary</span></span> | <span data-ttu-id="f457d-361">Varbinary (até 8.000)</span><span class="sxs-lookup"><span data-stu-id="f457d-361">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="f457d-362">Data</span><span class="sxs-lookup"><span data-stu-id="f457d-362">Date</span></span> | <span data-ttu-id="f457d-363">Data</span><span class="sxs-lookup"><span data-stu-id="f457d-363">Date</span></span> |
| <span data-ttu-id="f457d-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="f457d-364">DateTime</span></span> | <span data-ttu-id="f457d-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="f457d-365">DateTime</span></span> |
| <span data-ttu-id="f457d-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="f457d-366">DateTime2</span></span> | <span data-ttu-id="f457d-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="f457d-367">DateTime2</span></span> |
| <span data-ttu-id="f457d-368">Hora</span><span class="sxs-lookup"><span data-stu-id="f457d-368">Time</span></span> | <span data-ttu-id="f457d-369">Hora</span><span class="sxs-lookup"><span data-stu-id="f457d-369">Time</span></span> |
| <span data-ttu-id="f457d-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f457d-370">DateTimeOffset</span></span> | <span data-ttu-id="f457d-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f457d-371">DateTimeOffset</span></span> |
| <span data-ttu-id="f457d-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="f457d-372">SmallDateTime</span></span> | <span data-ttu-id="f457d-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="f457d-373">SmallDateTime</span></span> |
| <span data-ttu-id="f457d-374">Texto</span><span class="sxs-lookup"><span data-stu-id="f457d-374">Text</span></span> | <span data-ttu-id="f457d-375">Varchar (até 8.000)</span><span class="sxs-lookup"><span data-stu-id="f457d-375">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="f457d-376">NText</span><span class="sxs-lookup"><span data-stu-id="f457d-376">NText</span></span> | <span data-ttu-id="f457d-377">NVarChar (até 4.000)</span><span class="sxs-lookup"><span data-stu-id="f457d-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="f457d-378">Imagem</span><span class="sxs-lookup"><span data-stu-id="f457d-378">Image</span></span> | <span data-ttu-id="f457d-379">VarBinary (até 8.000)</span><span class="sxs-lookup"><span data-stu-id="f457d-379">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="f457d-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="f457d-380">UniqueIdentifier</span></span> | <span data-ttu-id="f457d-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="f457d-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="f457d-382">Char</span><span class="sxs-lookup"><span data-stu-id="f457d-382">Char</span></span> | <span data-ttu-id="f457d-383">Char</span><span class="sxs-lookup"><span data-stu-id="f457d-383">Char</span></span> |
| <span data-ttu-id="f457d-384">NChar</span><span class="sxs-lookup"><span data-stu-id="f457d-384">NChar</span></span> | <span data-ttu-id="f457d-385">NChar</span><span class="sxs-lookup"><span data-stu-id="f457d-385">NChar</span></span> |
| <span data-ttu-id="f457d-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="f457d-386">VarChar</span></span> | <span data-ttu-id="f457d-387">VarChar (até 8.000)</span><span class="sxs-lookup"><span data-stu-id="f457d-387">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="f457d-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="f457d-388">NVarChar</span></span> | <span data-ttu-id="f457d-389">NVarChar (até 4.000)</span><span class="sxs-lookup"><span data-stu-id="f457d-389">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="f457d-390">xml</span><span class="sxs-lookup"><span data-stu-id="f457d-390">Xml</span></span> | <span data-ttu-id="f457d-391">Varchar (até 8.000)</span><span class="sxs-lookup"><span data-stu-id="f457d-391">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="f457d-392">Mapeamento de tipo do SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="f457d-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f457d-393">Como mencionado no artigo sobre as [Atividades de Movimentação de Dados](data-factory-data-movement-activities.md) , a atividade de Cópia executa conversões automáticas dos tipos de fonte nos tipos de coletor com a seguinte abordagem de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="f457d-393">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="f457d-394">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="f457d-394">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="f457d-395">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="f457d-395">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="f457d-396">Ao mover dados bidirecionalmente no SQL Data Warehouse do Azure, os mapeamentos a seguir são usados do tipo SQL para o tipo .NET e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="f457d-396">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="f457d-397">O mapeamento é o mesmo que o [Mapeamento de tipo de dados do SQL Server para o ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="f457d-397">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="f457d-398">Tipo de mecanismo do Banco de Dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f457d-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="f457d-399">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f457d-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="f457d-400">bigint</span><span class="sxs-lookup"><span data-stu-id="f457d-400">bigint</span></span> |<span data-ttu-id="f457d-401">Int64</span><span class="sxs-lookup"><span data-stu-id="f457d-401">Int64</span></span> |
| <span data-ttu-id="f457d-402">binário</span><span class="sxs-lookup"><span data-stu-id="f457d-402">binary</span></span> |<span data-ttu-id="f457d-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f457d-403">Byte[]</span></span> |
| <span data-ttu-id="f457d-404">bit</span><span class="sxs-lookup"><span data-stu-id="f457d-404">bit</span></span> |<span data-ttu-id="f457d-405">Booliano</span><span class="sxs-lookup"><span data-stu-id="f457d-405">Boolean</span></span> |
| <span data-ttu-id="f457d-406">char</span><span class="sxs-lookup"><span data-stu-id="f457d-406">char</span></span> |<span data-ttu-id="f457d-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f457d-407">String, Char[]</span></span> |
| <span data-ttu-id="f457d-408">data</span><span class="sxs-lookup"><span data-stu-id="f457d-408">date</span></span> |<span data-ttu-id="f457d-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="f457d-409">DateTime</span></span> |
| <span data-ttu-id="f457d-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="f457d-410">Datetime</span></span> |<span data-ttu-id="f457d-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="f457d-411">DateTime</span></span> |
| <span data-ttu-id="f457d-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="f457d-412">datetime2</span></span> |<span data-ttu-id="f457d-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="f457d-413">DateTime</span></span> |
| <span data-ttu-id="f457d-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f457d-414">Datetimeoffset</span></span> |<span data-ttu-id="f457d-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="f457d-415">DateTimeOffset</span></span> |
| <span data-ttu-id="f457d-416">Decimal</span><span class="sxs-lookup"><span data-stu-id="f457d-416">Decimal</span></span> |<span data-ttu-id="f457d-417">Decimal</span><span class="sxs-lookup"><span data-stu-id="f457d-417">Decimal</span></span> |
| <span data-ttu-id="f457d-418">Atributo FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="f457d-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="f457d-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f457d-419">Byte[]</span></span> |
| <span data-ttu-id="f457d-420">Float</span><span class="sxs-lookup"><span data-stu-id="f457d-420">Float</span></span> |<span data-ttu-id="f457d-421">Duplo</span><span class="sxs-lookup"><span data-stu-id="f457d-421">Double</span></span> |
| <span data-ttu-id="f457d-422">imagem</span><span class="sxs-lookup"><span data-stu-id="f457d-422">image</span></span> |<span data-ttu-id="f457d-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f457d-423">Byte[]</span></span> |
| <span data-ttu-id="f457d-424">int</span><span class="sxs-lookup"><span data-stu-id="f457d-424">int</span></span> |<span data-ttu-id="f457d-425">Int32</span><span class="sxs-lookup"><span data-stu-id="f457d-425">Int32</span></span> |
| <span data-ttu-id="f457d-426">money</span><span class="sxs-lookup"><span data-stu-id="f457d-426">money</span></span> |<span data-ttu-id="f457d-427">Decimal</span><span class="sxs-lookup"><span data-stu-id="f457d-427">Decimal</span></span> |
| <span data-ttu-id="f457d-428">nchar</span><span class="sxs-lookup"><span data-stu-id="f457d-428">nchar</span></span> |<span data-ttu-id="f457d-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f457d-429">String, Char[]</span></span> |
| <span data-ttu-id="f457d-430">ntext</span><span class="sxs-lookup"><span data-stu-id="f457d-430">ntext</span></span> |<span data-ttu-id="f457d-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f457d-431">String, Char[]</span></span> |
| <span data-ttu-id="f457d-432">numérico</span><span class="sxs-lookup"><span data-stu-id="f457d-432">numeric</span></span> |<span data-ttu-id="f457d-433">Decimal</span><span class="sxs-lookup"><span data-stu-id="f457d-433">Decimal</span></span> |
| <span data-ttu-id="f457d-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="f457d-434">nvarchar</span></span> |<span data-ttu-id="f457d-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f457d-435">String, Char[]</span></span> |
| <span data-ttu-id="f457d-436">real</span><span class="sxs-lookup"><span data-stu-id="f457d-436">real</span></span> |<span data-ttu-id="f457d-437">Single</span><span class="sxs-lookup"><span data-stu-id="f457d-437">Single</span></span> |
| <span data-ttu-id="f457d-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="f457d-438">rowversion</span></span> |<span data-ttu-id="f457d-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f457d-439">Byte[]</span></span> |
| <span data-ttu-id="f457d-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="f457d-440">smalldatetime</span></span> |<span data-ttu-id="f457d-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="f457d-441">DateTime</span></span> |
| <span data-ttu-id="f457d-442">smallint</span><span class="sxs-lookup"><span data-stu-id="f457d-442">smallint</span></span> |<span data-ttu-id="f457d-443">Int16</span><span class="sxs-lookup"><span data-stu-id="f457d-443">Int16</span></span> |
| <span data-ttu-id="f457d-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="f457d-444">smallmoney</span></span> |<span data-ttu-id="f457d-445">Decimal</span><span class="sxs-lookup"><span data-stu-id="f457d-445">Decimal</span></span> |
| <span data-ttu-id="f457d-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="f457d-446">sql_variant</span></span> |<span data-ttu-id="f457d-447">Objeto *</span><span class="sxs-lookup"><span data-stu-id="f457d-447">Object *</span></span> |
| <span data-ttu-id="f457d-448">texto</span><span class="sxs-lookup"><span data-stu-id="f457d-448">text</span></span> |<span data-ttu-id="f457d-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f457d-449">String, Char[]</span></span> |
| <span data-ttu-id="f457d-450">tempo real</span><span class="sxs-lookup"><span data-stu-id="f457d-450">time</span></span> |<span data-ttu-id="f457d-451">timespan</span><span class="sxs-lookup"><span data-stu-id="f457d-451">TimeSpan</span></span> |
| <span data-ttu-id="f457d-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="f457d-452">timestamp</span></span> |<span data-ttu-id="f457d-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f457d-453">Byte[]</span></span> |
| <span data-ttu-id="f457d-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="f457d-454">tinyint</span></span> |<span data-ttu-id="f457d-455">Byte</span><span class="sxs-lookup"><span data-stu-id="f457d-455">Byte</span></span> |
| <span data-ttu-id="f457d-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="f457d-456">uniqueidentifier</span></span> |<span data-ttu-id="f457d-457">Guid</span><span class="sxs-lookup"><span data-stu-id="f457d-457">Guid</span></span> |
| <span data-ttu-id="f457d-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="f457d-458">varbinary</span></span> |<span data-ttu-id="f457d-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="f457d-459">Byte[]</span></span> |
| <span data-ttu-id="f457d-460">varchar</span><span class="sxs-lookup"><span data-stu-id="f457d-460">varchar</span></span> |<span data-ttu-id="f457d-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="f457d-461">String, Char[]</span></span> |
| <span data-ttu-id="f457d-462">xml</span><span class="sxs-lookup"><span data-stu-id="f457d-462">xml</span></span> |<span data-ttu-id="f457d-463">xml</span><span class="sxs-lookup"><span data-stu-id="f457d-463">Xml</span></span> |

<span data-ttu-id="f457d-464">Você também pode mapear colunas do conjunto de dados de origem para colunas do conjunto de dados de coletor na definição da atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="f457d-464">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="f457d-465">Para obter detalhes, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapear colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="f457d-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="f457d-466">Exemplos JSON para cópia de dados de e para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f457d-466">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="f457d-467">Os exemplos a seguir fornecem amostras de definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f457d-467">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f457d-468">Eles mostram como copiar dados entre o Azure SQL Data Warehouse e o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f457d-468">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="f457d-469">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f457d-469">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="f457d-470">Exemplo: Copiar dados do SQL Data Warehouse do Azure para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="f457d-470">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="f457d-471">O exemplo define as entidades do Data Factory a seguir:</span><span class="sxs-lookup"><span data-stu-id="f457d-471">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="f457d-472">Um serviço vinculado do tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="f457d-473">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f457d-474">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="f457d-475">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f457d-476">O [pipeline](data-factory-create-pipelines.md) com a Atividade de cópia que usa [SqlDWSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f457d-477">O exemplo copia os dados da série temporal (por hora, dia etc.) de uma tabela no banco de dados do Azure SQL Data Warehouse para um blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f457d-477">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="f457d-478">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="f457d-478">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f457d-479">**Serviço vinculado do SQL Data Warehouse do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f457d-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="f457d-480">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f457d-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="f457d-481">**Conjunto de dados de entrada do SQL Data Warehouse do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f457d-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="f457d-482">O exemplo supõe que você criou uma tabela "MyTable" no SQL Data Warehouse do Azure e que ela contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="f457d-482">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="f457d-483">Configurar “external”: “true” informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f457d-483">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="f457d-484">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f457d-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="f457d-485">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="f457d-485">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f457d-486">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="f457d-486">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f457d-487">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="f457d-487">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="f457d-488">**Atividade de cópia em um pipeline com SqlDWSource e BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="f457d-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="f457d-489">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f457d-489">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f457d-490">Na definição JSON do pipeline, o tipo **source** está definido como **SqlDWSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f457d-490">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="f457d-491">A consulta SQL especificada para a propriedade **SqlReaderQuery** seleciona os dados na última hora a serem copiados.</span><span class="sxs-lookup"><span data-stu-id="f457d-491">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> <span data-ttu-id="f457d-492">No exemplo, **sqlReaderQuery** é especificada para o SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="f457d-492">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="f457d-493">A Atividade de Cópia executa essa consulta em relação à fonte de SQL Data Warehouse do Azure para obter os dados.</span><span class="sxs-lookup"><span data-stu-id="f457d-493">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="f457d-494">Como alternativa, você pode especificar um procedimento armazenado especificando o **sqlReaderStoredProcedureName** e o **storedProcedureParameters** (se o procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="f457d-494">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="f457d-495">Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, as colunas definidas na seção de estrutura do conjunto de dados JSON são usadas para criar uma consulta (selecione column1, column2 de mytable) para executar o SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="f457d-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f457d-496">Se a definição de conjunto de dados não tem a estrutura, todas as colunas serão selecionadas da tabela.</span><span class="sxs-lookup"><span data-stu-id="f457d-496">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="f457d-497">Exemplo: Copiar dados do Blob do Azure para o SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="f457d-497">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f457d-498">O exemplo define as entidades do Data Factory a seguir:</span><span class="sxs-lookup"><span data-stu-id="f457d-498">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="f457d-499">Um serviço vinculado do tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="f457d-500">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f457d-501">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="f457d-502">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="f457d-503">Um [pipeline](data-factory-create-pipelines.md) com Atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f457d-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="f457d-504">O exemplo copia os dados da série temporal (por hora, dia etc.) de um blob do Azure para uma tabela no banco de dados do Azure SQL Data Warehouse a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f457d-504">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="f457d-505">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="f457d-505">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="f457d-506">**Serviço vinculado do SQL Data Warehouse do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f457d-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="f457d-507">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f457d-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="f457d-508">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f457d-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="f457d-509">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="f457d-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f457d-510">O caminho de pasta e nome de arquivo para o blob são avaliados dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="f457d-510">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="f457d-511">O caminho da pasta usa a parte do ano, mês e dia da hora de início e o nome de arquivo usa a parte da hora de início.</span><span class="sxs-lookup"><span data-stu-id="f457d-511">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="f457d-512">A configuração “external”: ”true” informa ao serviço Data Factory que essa é uma tabela externa do data factory e não é produzida por uma atividade no data factory.</span><span class="sxs-lookup"><span data-stu-id="f457d-512">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="f457d-513">**Conjunto de dados de saída do SQL Data Warehouse do Azure:**</span><span class="sxs-lookup"><span data-stu-id="f457d-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="f457d-514">O exemplo copia os dados em uma tabela chamada "MyTable" no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="f457d-514">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f457d-515">Crie a tabela no Azure SQL Data Warehouse com o mesmo número de colunas que você espera que o arquivo CSV de Blob contenha.</span><span class="sxs-lookup"><span data-stu-id="f457d-515">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="f457d-516">Novas linhas são adicionadas à tabela a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f457d-516">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="f457d-517">**Atividade de cópia em um pipeline com BlobSource e SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="f457d-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="f457d-518">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f457d-518">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="f457d-519">Na definição de JSON do pipeline, o tipo **source** está definido como **BlobSource** e o tipo **sink** está definido como **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="f457d-519">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="f457d-520">Para obter instruções, consulte a [carregar 1 TB no depósito de dados do SQL Azure em 15 minutos com o Azure Data Factory](data-factory-load-sql-data-warehouse.md) e [carregar dados com o Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artigo na documentação do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f457d-520">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f457d-521">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="f457d-521">Performance and Tuning</span></span>
<span data-ttu-id="f457d-522">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="f457d-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
