---
title: Copiar dados de/para o Banco de Dados SQL do Azure | Microsoft Docs
description: Saiba como copiar dados para/do Banco de Dados SQL do Azure usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: a64d13fa7dc5f50c259b98774be80b603dce400a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-to-and-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="ffb65-103">Copiar dados de e para o Banco de Dados SQL do Azure usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ffb65-103">Copy data to and from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="ffb65-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados bidirecionalmente de e para o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb65-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to and from Azure SQL Database.</span></span> <span data-ttu-id="ffb65-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ffb65-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="ffb65-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="ffb65-106">Supported scenarios</span></span>
<span data-ttu-id="ffb65-107">Você pode copiar dados **de um Banco de Dados SQL do Azure** para os seguintes armazenamentos de dados:</span><span class="sxs-lookup"><span data-stu-id="ffb65-107">You can copy data **from Azure SQL Database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="ffb65-108">Você pode copiar dados dos armazenamentos de dados a seguir **para um Banco de Dados SQL do Azure**:</span><span class="sxs-lookup"><span data-stu-id="ffb65-108">You can copy data from the following data stores **to Azure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="ffb65-109">Tipos de autenticação com suporte</span><span class="sxs-lookup"><span data-stu-id="ffb65-109">Supported authentication type</span></span>
<span data-ttu-id="ffb65-110">O conector do Banco de Dados SQL do Azure dá suporte à autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="ffb65-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ffb65-111">Introdução</span><span class="sxs-lookup"><span data-stu-id="ffb65-111">Getting started</span></span>
<span data-ttu-id="ffb65-112">Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente de um Banco de Dados SQL do Azure usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="ffb65-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="ffb65-113">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="ffb65-113">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="ffb65-114">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="ffb65-115">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="ffb65-115">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ffb65-116">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ffb65-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ffb65-117">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="ffb65-117">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="ffb65-118">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="ffb65-118">Create a **data factory**.</span></span> <span data-ttu-id="ffb65-119">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="ffb65-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="ffb65-120">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="ffb65-120">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="ffb65-121">Por exemplo, se você está copiando dados de um Armazenamento de Blobs do Azure para um banco de dados SQL do Azure, crie dois serviços vinculados para vincular seu banco de dados do SQL do Azure e conta de Armazenamento do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="ffb65-121">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="ffb65-122">Para propriedades do serviço vinculado que são específicas do Banco de Dados SQL do Azure, consulte a seção [propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-122">For linked service properties that are specific to Azure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="ffb65-123">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="ffb65-123">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="ffb65-124">No exemplo mencionado na última etapa, você cria um conjunto de dados para especificar o contêiner de blob e a pasta que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ffb65-124">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="ffb65-125">Em seguida, você cria outro conjunto de dados para especificar a tabela SQL no banco de dados SQL do Azure que contém os dados copiados do Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="ffb65-125">And, you create another dataset to specify the SQL table in the Azure SQL database  that holds the data copied from the blob storage.</span></span> <span data-ttu-id="ffb65-126">Para propriedades do conjunto de dados que são específicas do Azure Data Lake Store, consulte a seção [propriedades do conjunto de dados](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-126">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="ffb65-127">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="ffb65-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="ffb65-128">No exemplo mencionado anteriormente, você usa BlobSource como fonte e SqlSink como coletor para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ffb65-128">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="ffb65-129">De modo similar, se você estiver copiando do Banco de Dados SQL do Azure para o Armazenamento de Blobs do Azure, você usará SqlSource e BlobSink na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ffb65-129">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="ffb65-130">Para propriedades da atividade de cópia que são específicas do Banco de Dados SQL do Azure, consulte a seção [propriedades da atividade de cópia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-130">For copy activity properties that are specific to Azure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="ffb65-131">Para obter detalhes sobre como usar um armazenamento de dados como uma origem ou um coletor, clique no link na seção anterior para o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-131">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="ffb65-132">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="ffb65-132">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="ffb65-133">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ffb65-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="ffb65-134">Para obter exemplos com definições de JSON das entidades do Data Factory usadas para copiar dados bidirecionalmente em um Banco de Dados SQL do Azure, confira a seção [Exemplos de JSON](#json-examples-for-copying-data-to-and-from-sql-database) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ffb65-134">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="ffb65-135">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas para um Banco de Dados SQL do Azure:</span><span class="sxs-lookup"><span data-stu-id="ffb65-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="ffb65-136">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ffb65-136">Linked service properties</span></span>
<span data-ttu-id="ffb65-137">Um serviço vinculado do SQL do Azure vincula um banco de dados SQL do Azure ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="ffb65-137">An Azure SQL linked service links an Azure SQL database to your data factory.</span></span> <span data-ttu-id="ffb65-138">A tabela a seguir fornece a descrição para elementos JSON específicas para o serviço de vinculado de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb65-138">The following table provides description for JSON elements specific to Azure SQL linked service.</span></span>

| <span data-ttu-id="ffb65-139">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ffb65-139">Property</span></span> | <span data-ttu-id="ffb65-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="ffb65-140">Description</span></span> | <span data-ttu-id="ffb65-141">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ffb65-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffb65-142">type</span><span class="sxs-lookup"><span data-stu-id="ffb65-142">type</span></span> |<span data-ttu-id="ffb65-143">A propriedade type deve ser definida como: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="ffb65-143">The type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="ffb65-144">Sim</span><span class="sxs-lookup"><span data-stu-id="ffb65-144">Yes</span></span> |
| <span data-ttu-id="ffb65-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="ffb65-145">connectionString</span></span> |<span data-ttu-id="ffb65-146">Especifique as informações necessárias para se conectar à instância do Banco de Dados SQL Azure para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="ffb65-146">Specify information needed to connect to the Azure SQL Database instance for the connectionString property.</span></span> <span data-ttu-id="ffb65-147">Há suporte somente para autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="ffb65-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="ffb65-148">Sim</span><span class="sxs-lookup"><span data-stu-id="ffb65-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ffb65-149">Configure o [Firewall do Banco de Dados SQL do Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) do servidor de banco de dados para [permitir que os Serviços do Azure acessem o servidor](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="ffb65-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="ffb65-150">Além disso, se você estiver copiando os dados para o Banco de Dados SQL do Azure de fora do Azure, inclusive a partir das fontes de dados locais com o gateway do data factory, configure o devido intervalo de endereços IP do computador que está enviando os dados para o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb65-150">Additionally, if you are copying data to Azure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="ffb65-151">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ffb65-151">Dataset properties</span></span>
<span data-ttu-id="ffb65-152">Para especificar um conjunto de dados de modo a representar dados de entrada ou saída em um banco de dados SQL Azure, defina a propriedade de tipo do conjunto de dados para: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="ffb65-152">To specify a dataset to represent input or output data in an Azure SQL database, you set the type property of the dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="ffb65-153">Defina a propriedade **linkedServiceName** do conjunto de dados para o nome do serviço vinculado do SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb65-153">Set the **linkedServiceName** property of the dataset to the name of the Azure SQL linked service.</span></span>  

<span data-ttu-id="ffb65-154">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="ffb65-154">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ffb65-155">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="ffb65-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ffb65-156">A seção typeProperties é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-156">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="ffb65-157">A seção **typeProperties** do conjunto de dados do tipo **AzureSqlTable** tem as propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb65-157">The **typeProperties** section for the dataset of type **AzureSqlTable** has the following properties:</span></span>

| <span data-ttu-id="ffb65-158">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ffb65-158">Property</span></span> | <span data-ttu-id="ffb65-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="ffb65-159">Description</span></span> | <span data-ttu-id="ffb65-160">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ffb65-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffb65-161">tableName</span><span class="sxs-lookup"><span data-stu-id="ffb65-161">tableName</span></span> |<span data-ttu-id="ffb65-162">Nome da tabela ou exibição na instância do Banco de Dados SQL Azure à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="ffb65-162">Name of the table or view in the Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="ffb65-163">Sim</span><span class="sxs-lookup"><span data-stu-id="ffb65-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ffb65-164">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="ffb65-164">Copy activity properties</span></span>
<span data-ttu-id="ffb65-165">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ffb65-165">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ffb65-166">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="ffb65-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb65-167">A Atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="ffb65-167">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="ffb65-168">Por outro lado, as propriedades disponíveis na seção **typeProperties** da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="ffb65-168">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="ffb65-169">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="ffb65-169">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="ffb65-170">Se você estiver movendo dados de um banco de dados SQL do Azure, defina o tipo de origem na atividade de cópia como **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="ffb65-170">If you are moving data from an Azure SQL database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="ffb65-171">Da mesma forma você estiver movendo dados para um banco de dados SQL do Azure, defina o tipo de coletor na atividade de cópia como **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ffb65-171">Similarly, if you are moving data to an Azure SQL database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="ffb65-172">Esta seção fornece uma lista das propriedades com suporte de SqlSource e SqlSink.</span><span class="sxs-lookup"><span data-stu-id="ffb65-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="ffb65-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="ffb65-173">SqlSource</span></span>
<span data-ttu-id="ffb65-174">Na atividade de cópia, quando a fonte é do tipo **SqlSource**, as seguintes propriedades estão disponíveis na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="ffb65-174">In copy activity, when the source is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="ffb65-175">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ffb65-175">Property</span></span> | <span data-ttu-id="ffb65-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="ffb65-176">Description</span></span> | <span data-ttu-id="ffb65-177">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ffb65-177">Allowed values</span></span> | <span data-ttu-id="ffb65-178">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ffb65-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ffb65-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ffb65-179">sqlReaderQuery</span></span> |<span data-ttu-id="ffb65-180">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-180">Use the custom query to read data.</span></span> |<span data-ttu-id="ffb65-181">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ffb65-181">SQL query string.</span></span> <span data-ttu-id="ffb65-182">Exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ffb65-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="ffb65-183">Não</span><span class="sxs-lookup"><span data-stu-id="ffb65-183">No</span></span> |
| <span data-ttu-id="ffb65-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ffb65-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ffb65-185">Nome do procedimento armazenado que lê os dados da tabela de origem.</span><span class="sxs-lookup"><span data-stu-id="ffb65-185">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="ffb65-186">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-186">Name of the stored procedure.</span></span> <span data-ttu-id="ffb65-187">A última instrução SQL deve ser uma instrução SELECT no procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-187">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="ffb65-188">Não</span><span class="sxs-lookup"><span data-stu-id="ffb65-188">No</span></span> |
| <span data-ttu-id="ffb65-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ffb65-189">storedProcedureParameters</span></span> |<span data-ttu-id="ffb65-190">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-190">Parameters for the stored procedure.</span></span> |<span data-ttu-id="ffb65-191">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ffb65-191">Name/value pairs.</span></span> <span data-ttu-id="ffb65-192">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-192">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="ffb65-193">Não</span><span class="sxs-lookup"><span data-stu-id="ffb65-193">No</span></span> |

<span data-ttu-id="ffb65-194">Se **sqlReaderQuery** for especificado para SqlSource, a Atividade de Cópia executa essa consulta em relação à fonte do Banco de Dados SQL do Azure para obter os dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-194">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="ffb65-195">Como alternativa, você pode especificar um procedimento armazenado especificando o **sqlReaderStoredProcedureName** e o **storedProcedureParameters** (se o procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="ffb65-195">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="ffb65-196">Se você não especificar sqlReaderQuery nem sqlReaderStoredProcedureName, as colunas definidas na seção da estrutura do JSON do conjunto de dados serão usadas para compilar uma consulta (`select column1, column2 from mytable`) para executar no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb65-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (`select column1, column2 from mytable`) to run against the Azure SQL Database.</span></span> <span data-ttu-id="ffb65-197">Se a definição de conjunto de dados não tem a estrutura, todas as colunas serão selecionadas da tabela.</span><span class="sxs-lookup"><span data-stu-id="ffb65-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="ffb65-198">Quando você usa **sqlReaderStoredProcedureName**, ainda é necessário especificar um valor para a propriedade **tableName** no JSON do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-198">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="ffb65-199">Contudo, não há nenhuma validação executada nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="ffb65-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="ffb65-200">Exemplo de SqlSource</span><span class="sxs-lookup"><span data-stu-id="ffb65-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="ffb65-201">**A definição do procedimento armazenado:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-201">**The stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="ffb65-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="ffb65-202">SqlSink</span></span>
<span data-ttu-id="ffb65-203">**SqlSink** dá suporte às seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="ffb65-203">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="ffb65-204">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ffb65-204">Property</span></span> | <span data-ttu-id="ffb65-205">Descrição</span><span class="sxs-lookup"><span data-stu-id="ffb65-205">Description</span></span> | <span data-ttu-id="ffb65-206">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ffb65-206">Allowed values</span></span> | <span data-ttu-id="ffb65-207">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ffb65-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ffb65-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ffb65-208">writeBatchTimeout</span></span> |<span data-ttu-id="ffb65-209">Tempo de espera para a operação de inserção em lotes ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="ffb65-209">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="ffb65-210">timespan</span><span class="sxs-lookup"><span data-stu-id="ffb65-210">timespan</span></span><br/><br/> <span data-ttu-id="ffb65-211">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="ffb65-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ffb65-212">Não</span><span class="sxs-lookup"><span data-stu-id="ffb65-212">No</span></span> |
| <span data-ttu-id="ffb65-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ffb65-213">writeBatchSize</span></span> |<span data-ttu-id="ffb65-214">Insere dados na tabela SQL quando o tamanho do buffer atinge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="ffb65-214">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="ffb65-215">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="ffb65-215">Integer (number of rows)</span></span> |<span data-ttu-id="ffb65-216">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="ffb65-216">No (default: 10000)</span></span> |
| <span data-ttu-id="ffb65-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ffb65-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ffb65-218">Especifique uma consulta da Atividade de Cópia a executar para que os dados de uma fatia específica sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="ffb65-218">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="ffb65-219">Para saber mais, consulte [cópia repetida](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ffb65-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ffb65-220">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="ffb65-220">A query statement.</span></span> |<span data-ttu-id="ffb65-221">Não</span><span class="sxs-lookup"><span data-stu-id="ffb65-221">No</span></span> |
| <span data-ttu-id="ffb65-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="ffb65-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="ffb65-223">Especifique um nome de coluna para a Atividade de Cópia a preencher com o identificador de fatias gerado automaticamente, que é usado para limpar os dados de uma fatia específica ao executar novamente.</span><span class="sxs-lookup"><span data-stu-id="ffb65-223">Specify a column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="ffb65-224">Para saber mais, consulte [cópia repetida](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ffb65-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ffb65-225">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="ffb65-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="ffb65-226">Não</span><span class="sxs-lookup"><span data-stu-id="ffb65-226">No</span></span> |
| <span data-ttu-id="ffb65-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ffb65-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="ffb65-228">Nome do procedimento armazenado que upserts (atualiza/insere) na tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="ffb65-228">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="ffb65-229">Nome do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-229">Name of the stored procedure.</span></span> |<span data-ttu-id="ffb65-230">Não</span><span class="sxs-lookup"><span data-stu-id="ffb65-230">No</span></span> |
| <span data-ttu-id="ffb65-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ffb65-231">storedProcedureParameters</span></span> |<span data-ttu-id="ffb65-232">Parâmetros para o procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-232">Parameters for the stored procedure.</span></span> |<span data-ttu-id="ffb65-233">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ffb65-233">Name/value pairs.</span></span> <span data-ttu-id="ffb65-234">Nomes e uso de maiúsculas e minúsculas de parâmetros devem corresponder aos nomes e o uso de maiúsculas e minúsculas dos parâmetros do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-234">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="ffb65-235">Não</span><span class="sxs-lookup"><span data-stu-id="ffb65-235">No</span></span> |
| <span data-ttu-id="ffb65-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="ffb65-236">sqlWriterTableType</span></span> |<span data-ttu-id="ffb65-237">Especifique um nome do tipo de tabela a ser usado no procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-237">Specify a table type name to be used in the stored procedure.</span></span> <span data-ttu-id="ffb65-238">A atividade de cópia disponibiliza aqueles dados sendo movidos em uma tabela temporária com esse tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="ffb65-238">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="ffb65-239">O código de procedimento armazenado pode mesclar os dados sendo copiados com dados existentes.</span><span class="sxs-lookup"><span data-stu-id="ffb65-239">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="ffb65-240">Um nome de tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="ffb65-240">A table type name.</span></span> |<span data-ttu-id="ffb65-241">Não</span><span class="sxs-lookup"><span data-stu-id="ffb65-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="ffb65-242">Exemplo de SqlSink</span><span class="sxs-lookup"><span data-stu-id="ffb65-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-to-and-from-sql-database"></a><span data-ttu-id="ffb65-243">Exemplos JSON para cópia de dados do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="ffb65-243">JSON examples for copying data to and from SQL Database</span></span>
<span data-ttu-id="ffb65-244">Os exemplos a seguir fornecem amostras de definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ffb65-244">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ffb65-245">Eles mostram como copiar dados entre o Banco de Dados SQL e o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb65-245">They show how to copy data to and from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="ffb65-246">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ffb65-246">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-to-azure-blob"></a><span data-ttu-id="ffb65-247">Exemplo: Copiar dados do Banco de Dados SQL do Azure para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="ffb65-247">Example: Copy data from Azure SQL Database to Azure Blob</span></span>
<span data-ttu-id="ffb65-248">O mesmo define as entidades do Data Factory a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb65-248">The same defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="ffb65-249">Um serviço vinculado do tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ffb65-250">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ffb65-251">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ffb65-252">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ffb65-253">Um [pipeline](data-factory-create-pipelines.md) com uma Atividade de Cópia que usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ffb65-254">O exemplo copia os dados da série temporal (por hora, dia etc.) de uma tabela no banco de dados SQL do Azure para um blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffb65-254">The sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database to a blob every hour.</span></span> <span data-ttu-id="ffb65-255">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="ffb65-255">The JSON properties used in these samples are described in sections following the samples.</span></span>  

<span data-ttu-id="ffb65-256">**Serviço vinculado do Banco de Dados SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-256">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="ffb65-257">Consulte a seção [Serviço vinculado do SQL Azure](#linked-service) para obter a lista de propriedades com o suporte deste serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-257">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="ffb65-258">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ffb65-259">Consulte o artigo [Blob do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter a lista de propriedades com o suporte deste serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-259">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="ffb65-260">**Conjunto de dados de entrada do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="ffb65-261">O exemplo supõe que você criou uma tabela "MyTable" no SQL Azure e que ela contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="ffb65-261">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="ffb65-262">A configuração "external": "true" informa ao serviço Azure Data Factory que o conjunto de dados é externo ao data factory e não é produzido por uma atividade no data factory.</span><span class="sxs-lookup"><span data-stu-id="ffb65-262">Setting “external”: ”true” informs the Azure Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="ffb65-263">Consulte a seção [Propriedades do tipo de conjunto de dados do SQL Azure](#dataset) para obter a lista de propriedades com o suporte deste tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-263">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ffb65-264">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ffb65-265">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="ffb65-265">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ffb65-266">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="ffb65-266">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ffb65-267">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="ffb65-267">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
<span data-ttu-id="ffb65-268">Consulte a seção [Propriedades do tipo de conjunto de dados do Blog do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter a lista de propriedades com o suporte deste tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-268">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ffb65-269">**Uma atividade de cópia em um pipeline com origem SQL e coletor Blob:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="ffb65-270">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffb65-270">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ffb65-271">Na definição de JSON do pipeline, o tipo de **fonte** está definido como **SqlSource** e o tipo de **coletor** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ffb65-271">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="ffb65-272">A consulta SQL especificada para a propriedade **SqlReaderQuery** seleciona os dados na última hora a serem copiados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-272">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="ffb65-273">Neste exemplo, **sqlReaderQuery** é especificada para SqlSource.</span><span class="sxs-lookup"><span data-stu-id="ffb65-273">In the example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="ffb65-274">A Atividade de Cópia executa essa consulta em relação à fonte do Banco de Dados SQL do Azure para obter os dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-274">The Copy Activity runs this query against the Azure SQL Database source to get the data.</span></span> <span data-ttu-id="ffb65-275">Como alternativa, você pode especificar um procedimento armazenado especificando o **sqlReaderStoredProcedureName** e o **storedProcedureParameters** (se o procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="ffb65-275">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="ffb65-276">Se você não especificar sqlReaderQuery nem sqlReaderStoredProcedureName, as colunas definidas na seção da estrutura do JSON do conjunto de dados serão usadas para compilar uma consulta para executar no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb65-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Database.</span></span> <span data-ttu-id="ffb65-277">Por exemplo: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="ffb65-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="ffb65-278">Se a definição de conjunto de dados não tem a estrutura, todas as colunas serão selecionadas da tabela.</span><span class="sxs-lookup"><span data-stu-id="ffb65-278">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="ffb65-279">Consulte a seção [Sql Source](#sqlsource) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para obter a lista de propriedades com suporte em SqlSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="ffb65-279">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-database"></a><span data-ttu-id="ffb65-280">Exemplo: Copiar dados do Blob do Azure para o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ffb65-280">Example: Copy data from Azure Blob to Azure SQL Database</span></span>
<span data-ttu-id="ffb65-281">O exemplo define as entidades do Data Factory a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffb65-281">The sample defines the following Data Factory entities:</span></span>  

1. <span data-ttu-id="ffb65-282">Um serviço vinculado do tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ffb65-283">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ffb65-284">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ffb65-285">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="ffb65-286">Um [pipeline](data-factory-create-pipelines.md) com a atividade de Cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ffb65-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ffb65-287">O exemplo copia os dados da série temporal (por hora, dia etc.) de um blob do Azure para uma tabela no banco de dados SQL do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffb65-287">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL database every hour.</span></span> <span data-ttu-id="ffb65-288">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="ffb65-288">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="ffb65-289">**Serviço vinculado do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-289">**Azure SQL linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="ffb65-290">Consulte a seção [Serviço vinculado do SQL Azure](#linked-service) para obter a lista de propriedades com o suporte deste serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-290">See the [Azure SQL Linked Service](#linked-service) section for the list of properties supported by this linked service.</span></span>

<span data-ttu-id="ffb65-291">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ffb65-292">Consulte o artigo [Blob do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter a lista de propriedades com o suporte deste serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ffb65-292">See the [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for the list of properties supported by this linked service.</span></span>


<span data-ttu-id="ffb65-293">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="ffb65-294">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="ffb65-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ffb65-295">O caminho de pasta e nome de arquivo para o blob são avaliados dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="ffb65-295">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ffb65-296">O caminho da pasta usa a parte do ano, mês e dia da hora de início e o nome de arquivo usa a parte da hora de início.</span><span class="sxs-lookup"><span data-stu-id="ffb65-296">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="ffb65-297">A configuração “external”: ”true” informa ao serviço Data Factory que essa é uma tabela externa do data factory e não é produzida por uma atividade no data factory.</span><span class="sxs-lookup"><span data-stu-id="ffb65-297">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
<span data-ttu-id="ffb65-298">Consulte a seção [Propriedades do tipo de conjunto de dados do Blog do Azure](data-factory-azure-blob-connector.md#dataset-properties) para obter a lista de propriedades com o suporte deste tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-298">See the [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ffb65-299">**Conjunto de dados de saída do Banco de Dados SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="ffb65-300">O exemplo copia dados para uma tabela chamada "MyTable" no SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ffb65-300">The sample copies data to a table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="ffb65-301">Crie a tabela no SQL Azure com o mesmo número de colunas que você espera que o arquivo CSV de Blob contenha.</span><span class="sxs-lookup"><span data-stu-id="ffb65-301">Create the table in Azure SQL with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="ffb65-302">Novas linhas são adicionadas à tabela a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffb65-302">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
<span data-ttu-id="ffb65-303">Consulte a seção [Propriedades do tipo de conjunto de dados do SQL Azure](#dataset) para obter a lista de propriedades com o suporte deste tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ffb65-303">See the [Azure SQL dataset type properties](#dataset) section for the list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ffb65-304">**Uma atividade de cópia em um pipeline com origem Blob e coletor SQL:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="ffb65-305">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffb65-305">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ffb65-306">Na definição de JSON do pipeline, o tipo de **fonte** está definido como **BlobSource** e o tipo de **coletor** está definido como **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ffb65-306">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
<span data-ttu-id="ffb65-307">Consulte a seção [Sql Sink](#sqlsink) e [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) para obter a lista de propriedades com o suporte de SqlSink e de BlobSource.</span><span class="sxs-lookup"><span data-stu-id="ffb65-307">See the [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="ffb65-308">Colunas de identidade no banco de dados de destino</span><span class="sxs-lookup"><span data-stu-id="ffb65-308">Identity columns in the target database</span></span>
<span data-ttu-id="ffb65-309">Esta seção fornece um exemplo para copiar dados de uma tabela de origem sem uma coluna de identidade para uma tabela de destino com uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="ffb65-309">This section provides an example for copying data from a source table without an identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="ffb65-310">**Tabela de origem:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="ffb65-311">**Tabela de destino:**</span><span class="sxs-lookup"><span data-stu-id="ffb65-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="ffb65-312">Observe que a tabela de destino tem uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="ffb65-312">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="ffb65-313">**Definição de JSON do conjunto de dados de origem**</span><span class="sxs-lookup"><span data-stu-id="ffb65-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="ffb65-314">**Definição de JSON do conjunto de dados de destino**</span><span class="sxs-lookup"><span data-stu-id="ffb65-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="ffb65-315">Observe que sua tabela de origem e de destino têm um esquema diferente (a de destino tem uma coluna adicional com identidade).</span><span class="sxs-lookup"><span data-stu-id="ffb65-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="ffb65-316">Nesse cenário, você precisa especificar a propriedade **structure** na definição de conjunto de dados de destino, que não inclui a coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="ffb65-316">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="ffb65-317">Invocar o procedimento armazenado do coletor SQL</span><span class="sxs-lookup"><span data-stu-id="ffb65-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="ffb65-318">Para obter um exemplo de como invocar um procedimento armazenado do coletor SQL em uma atividade de cópia de um pipeline, confira o artigo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocar procedimento armazenado para coletor SQL na atividade de cópia).</span><span class="sxs-lookup"><span data-stu-id="ffb65-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="ffb65-319">Mapeamento de tipo do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ffb65-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="ffb65-320">Como mencionado no artigo sobre as [atividades da movimentação de dados](data-factory-data-movement-activities.md) , a atividade de Cópia executa conversões automáticas dos tipos de fonte nos tipos de coletor com a seguinte abordagem de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="ffb65-320">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="ffb65-321">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="ffb65-321">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="ffb65-322">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="ffb65-322">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="ffb65-323">Ao mover dados bidirecionalmente no Banco de Dados SQL do Azure, os mapeamentos a seguir são usados do tipo SQL para o tipo .NET, e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="ffb65-323">When moving data to and from Azure SQL Database, the following mappings are used from SQL type to .NET type and vice versa.</span></span> <span data-ttu-id="ffb65-324">O mapeamento é o mesmo que o mapeamento de tipo de dados do SQL Server para o ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="ffb65-324">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="ffb65-325">Tipo de mecanismo do Banco de Dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="ffb65-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="ffb65-326">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ffb65-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="ffb65-327">bigint</span><span class="sxs-lookup"><span data-stu-id="ffb65-327">bigint</span></span> |<span data-ttu-id="ffb65-328">Int64</span><span class="sxs-lookup"><span data-stu-id="ffb65-328">Int64</span></span> |
| <span data-ttu-id="ffb65-329">binário</span><span class="sxs-lookup"><span data-stu-id="ffb65-329">binary</span></span> |<span data-ttu-id="ffb65-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-330">Byte[]</span></span> |
| <span data-ttu-id="ffb65-331">bit</span><span class="sxs-lookup"><span data-stu-id="ffb65-331">bit</span></span> |<span data-ttu-id="ffb65-332">Booliano</span><span class="sxs-lookup"><span data-stu-id="ffb65-332">Boolean</span></span> |
| <span data-ttu-id="ffb65-333">char</span><span class="sxs-lookup"><span data-stu-id="ffb65-333">char</span></span> |<span data-ttu-id="ffb65-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-334">String, Char[]</span></span> |
| <span data-ttu-id="ffb65-335">data</span><span class="sxs-lookup"><span data-stu-id="ffb65-335">date</span></span> |<span data-ttu-id="ffb65-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffb65-336">DateTime</span></span> |
| <span data-ttu-id="ffb65-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffb65-337">Datetime</span></span> |<span data-ttu-id="ffb65-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffb65-338">DateTime</span></span> |
| <span data-ttu-id="ffb65-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="ffb65-339">datetime2</span></span> |<span data-ttu-id="ffb65-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffb65-340">DateTime</span></span> |
| <span data-ttu-id="ffb65-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="ffb65-341">Datetimeoffset</span></span> |<span data-ttu-id="ffb65-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="ffb65-342">DateTimeOffset</span></span> |
| <span data-ttu-id="ffb65-343">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffb65-343">Decimal</span></span> |<span data-ttu-id="ffb65-344">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffb65-344">Decimal</span></span> |
| <span data-ttu-id="ffb65-345">Atributo FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="ffb65-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="ffb65-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-346">Byte[]</span></span> |
| <span data-ttu-id="ffb65-347">Float</span><span class="sxs-lookup"><span data-stu-id="ffb65-347">Float</span></span> |<span data-ttu-id="ffb65-348">Duplo</span><span class="sxs-lookup"><span data-stu-id="ffb65-348">Double</span></span> |
| <span data-ttu-id="ffb65-349">imagem</span><span class="sxs-lookup"><span data-stu-id="ffb65-349">image</span></span> |<span data-ttu-id="ffb65-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-350">Byte[]</span></span> |
| <span data-ttu-id="ffb65-351">int</span><span class="sxs-lookup"><span data-stu-id="ffb65-351">int</span></span> |<span data-ttu-id="ffb65-352">Int32</span><span class="sxs-lookup"><span data-stu-id="ffb65-352">Int32</span></span> |
| <span data-ttu-id="ffb65-353">money</span><span class="sxs-lookup"><span data-stu-id="ffb65-353">money</span></span> |<span data-ttu-id="ffb65-354">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffb65-354">Decimal</span></span> |
| <span data-ttu-id="ffb65-355">nchar</span><span class="sxs-lookup"><span data-stu-id="ffb65-355">nchar</span></span> |<span data-ttu-id="ffb65-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-356">String, Char[]</span></span> |
| <span data-ttu-id="ffb65-357">ntext</span><span class="sxs-lookup"><span data-stu-id="ffb65-357">ntext</span></span> |<span data-ttu-id="ffb65-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-358">String, Char[]</span></span> |
| <span data-ttu-id="ffb65-359">numérico</span><span class="sxs-lookup"><span data-stu-id="ffb65-359">numeric</span></span> |<span data-ttu-id="ffb65-360">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffb65-360">Decimal</span></span> |
| <span data-ttu-id="ffb65-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="ffb65-361">nvarchar</span></span> |<span data-ttu-id="ffb65-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-362">String, Char[]</span></span> |
| <span data-ttu-id="ffb65-363">real</span><span class="sxs-lookup"><span data-stu-id="ffb65-363">real</span></span> |<span data-ttu-id="ffb65-364">Single</span><span class="sxs-lookup"><span data-stu-id="ffb65-364">Single</span></span> |
| <span data-ttu-id="ffb65-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="ffb65-365">rowversion</span></span> |<span data-ttu-id="ffb65-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-366">Byte[]</span></span> |
| <span data-ttu-id="ffb65-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="ffb65-367">smalldatetime</span></span> |<span data-ttu-id="ffb65-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffb65-368">DateTime</span></span> |
| <span data-ttu-id="ffb65-369">smallint</span><span class="sxs-lookup"><span data-stu-id="ffb65-369">smallint</span></span> |<span data-ttu-id="ffb65-370">Int16</span><span class="sxs-lookup"><span data-stu-id="ffb65-370">Int16</span></span> |
| <span data-ttu-id="ffb65-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="ffb65-371">smallmoney</span></span> |<span data-ttu-id="ffb65-372">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffb65-372">Decimal</span></span> |
| <span data-ttu-id="ffb65-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="ffb65-373">sql_variant</span></span> |<span data-ttu-id="ffb65-374">Objeto *</span><span class="sxs-lookup"><span data-stu-id="ffb65-374">Object *</span></span> |
| <span data-ttu-id="ffb65-375">texto</span><span class="sxs-lookup"><span data-stu-id="ffb65-375">text</span></span> |<span data-ttu-id="ffb65-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-376">String, Char[]</span></span> |
| <span data-ttu-id="ffb65-377">tempo real</span><span class="sxs-lookup"><span data-stu-id="ffb65-377">time</span></span> |<span data-ttu-id="ffb65-378">timespan</span><span class="sxs-lookup"><span data-stu-id="ffb65-378">TimeSpan</span></span> |
| <span data-ttu-id="ffb65-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="ffb65-379">timestamp</span></span> |<span data-ttu-id="ffb65-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-380">Byte[]</span></span> |
| <span data-ttu-id="ffb65-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="ffb65-381">tinyint</span></span> |<span data-ttu-id="ffb65-382">Byte</span><span class="sxs-lookup"><span data-stu-id="ffb65-382">Byte</span></span> |
| <span data-ttu-id="ffb65-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="ffb65-383">uniqueidentifier</span></span> |<span data-ttu-id="ffb65-384">Guid</span><span class="sxs-lookup"><span data-stu-id="ffb65-384">Guid</span></span> |
| <span data-ttu-id="ffb65-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="ffb65-385">varbinary</span></span> |<span data-ttu-id="ffb65-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-386">Byte[]</span></span> |
| <span data-ttu-id="ffb65-387">varchar</span><span class="sxs-lookup"><span data-stu-id="ffb65-387">varchar</span></span> |<span data-ttu-id="ffb65-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffb65-388">String, Char[]</span></span> |
| <span data-ttu-id="ffb65-389">xml</span><span class="sxs-lookup"><span data-stu-id="ffb65-389">xml</span></span> |<span data-ttu-id="ffb65-390">xml</span><span class="sxs-lookup"><span data-stu-id="ffb65-390">Xml</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="ffb65-391">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="ffb65-391">Map source to sink columns</span></span>
<span data-ttu-id="ffb65-392">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="ffb65-392">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="ffb65-393">Cópia repetida</span><span class="sxs-lookup"><span data-stu-id="ffb65-393">Repeatable copy</span></span>
<span data-ttu-id="ffb65-394">Ao copiar dados para o Banco de Dados do SQL Server, a atividade de cópia acrescenta dados à tabela de coletor por padrão.</span><span class="sxs-lookup"><span data-stu-id="ffb65-394">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="ffb65-395">Para substituir isso pela execução de UPSERT, confira o artigo [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) (Gravação repetida no SqlSink).</span><span class="sxs-lookup"><span data-stu-id="ffb65-395">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="ffb65-396">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="ffb65-396">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="ffb65-397">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="ffb65-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ffb65-398">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="ffb65-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ffb65-399">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="ffb65-399">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ffb65-400">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="ffb65-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ffb65-401">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="ffb65-401">Performance and Tuning</span></span>
<span data-ttu-id="ffb65-402">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="ffb65-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
