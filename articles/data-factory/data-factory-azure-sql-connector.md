---
title: aaaCopy dados para/de banco de dados do SQL Azure | Microsoft Docs
description: Saiba como toocopy dados para/de banco de dados do SQL Azure usando o Azure Data Factory.
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
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="ffde7-103">Copiar dados tooand do banco de dados do SQL Azure usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ffde7-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="ffde7-104">Este artigo explica como toouse hello atividade de cópia no Azure Data Factory toomove dados tooand do banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ffde7-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="ffde7-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="ffde7-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="ffde7-106">Supported scenarios</span></span>
<span data-ttu-id="ffde7-107">Você pode copiar dados **do banco de dados do SQL Azure** toohello repositórios de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffde7-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="ffde7-108">Você pode copiar dados de saudação armazenamentos de dados a seguir **tooAzure banco de dados SQL**:</span><span class="sxs-lookup"><span data-stu-id="ffde7-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="ffde7-109">Tipos de autenticação com suporte</span><span class="sxs-lookup"><span data-stu-id="ffde7-109">Supported authentication type</span></span>
<span data-ttu-id="ffde7-110">O conector do Banco de Dados SQL do Azure dá suporte à autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="ffde7-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ffde7-111">Introdução</span><span class="sxs-lookup"><span data-stu-id="ffde7-111">Getting started</span></span>
<span data-ttu-id="ffde7-112">Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente de um Banco de Dados SQL do Azure usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="ffde7-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="ffde7-113">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="ffde7-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ffde7-114">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="ffde7-115">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="ffde7-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ffde7-116">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ffde7-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ffde7-117">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffde7-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="ffde7-118">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="ffde7-118">Create a **data factory**.</span></span> <span data-ttu-id="ffde7-119">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="ffde7-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="ffde7-120">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="ffde7-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="ffde7-121">Por exemplo, se você estiver copiando dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure, você criar duas toolink de serviços vinculados sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ffde7-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="ffde7-122">Para propriedades de serviço vinculado que específico tooAzure banco de dados SQL, consulte [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="ffde7-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="ffde7-123">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="ffde7-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="ffde7-124">O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="ffde7-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="ffde7-125">E, você cria outra tabela do conjunto de dados toospecify Olá SQL no banco de dados de SQL do Azure de saudação que contém dados Olá copiados saudação do armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="ffde7-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="ffde7-126">Para propriedades de conjunto de dados que são específico tooAzure repositório Data Lake, consulte [propriedades de conjunto de dados](#dataset-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="ffde7-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="ffde7-127">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="ffde7-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="ffde7-128">Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e do SqlSink como um coletor de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="ffde7-129">Da mesma forma, se você estiver copiando de banco de dados do Azure SQL tooAzure armazenamento de Blob, use SqlSource e BlobSink na atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="ffde7-130">Para propriedades de atividade de cópia que específico tooAzure banco de dados SQL, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="ffde7-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="ffde7-131">Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ffde7-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="ffde7-132">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="ffde7-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ffde7-133">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ffde7-134">Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um banco de dados do SQL Azure, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-sql-database) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="ffde7-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="ffde7-135">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure banco de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="ffde7-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="ffde7-136">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ffde7-136">Linked service properties</span></span>
<span data-ttu-id="ffde7-137">Um SQL Azure vinculado links serviço uma fábrica de dados de tooyour de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ffde7-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="ffde7-138">Olá, a tabela a seguir fornece o serviço vinculado de descrição de JSON de elementos específico tooAzure SQL.</span><span class="sxs-lookup"><span data-stu-id="ffde7-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="ffde7-139">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ffde7-139">Property</span></span> | <span data-ttu-id="ffde7-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="ffde7-140">Description</span></span> | <span data-ttu-id="ffde7-141">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ffde7-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffde7-142">type</span><span class="sxs-lookup"><span data-stu-id="ffde7-142">type</span></span> |<span data-ttu-id="ffde7-143">propriedade de tipo Hello deve ser definida como: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="ffde7-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="ffde7-144">Sim</span><span class="sxs-lookup"><span data-stu-id="ffde7-144">Yes</span></span> |
| <span data-ttu-id="ffde7-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="ffde7-145">connectionString</span></span> |<span data-ttu-id="ffde7-146">Especifique informações necessárias a instância de banco de dados do Azure SQL toohello tooconnect para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="ffde7-147">Há suporte somente para autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="ffde7-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="ffde7-148">Sim</span><span class="sxs-lookup"><span data-stu-id="ffde7-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ffde7-149">Configurar [Firewall de banco de dados do SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) Olá o servidor de banco de dados muito[permitir que serviços do Azure tooaccess Olá servidor](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="ffde7-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="ffde7-150">Além disso, se você estiver copiando dados tooAzure banco de dados SQL, incluindo Azure fora de fontes de dados local com o gateway da fábrica de dados, configure o intervalo de endereços IP apropriado para a máquina de saudação que está enviando dados tooAzure banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="ffde7-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="ffde7-151">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ffde7-151">Dataset properties</span></span>
<span data-ttu-id="ffde7-152">toospecify toorepresent um conjunto de dados dados de entrada ou saídos em um banco de dados do SQL Azure, defina propriedade de tipo de saudação do conjunto de dados Olá para: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="ffde7-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="ffde7-153">Saudação de conjunto **linkedServiceName** serviço vinculado de propriedade de nome de toohello Olá dataset de saudação SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ffde7-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="ffde7-154">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ffde7-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ffde7-155">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="ffde7-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ffde7-156">seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ffde7-157">Olá **typeProperties** seção de conjunto de dados de saudação do tipo **AzureSqlTable** tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffde7-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="ffde7-158">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ffde7-158">Property</span></span> | <span data-ttu-id="ffde7-159">Descrição</span><span class="sxs-lookup"><span data-stu-id="ffde7-159">Description</span></span> | <span data-ttu-id="ffde7-160">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ffde7-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ffde7-161">tableName</span><span class="sxs-lookup"><span data-stu-id="ffde7-161">tableName</span></span> |<span data-ttu-id="ffde7-162">Nome da tabela de saudação ou exibição na instância de banco de dados do Azure SQL Olá que serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="ffde7-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="ffde7-163">Sim</span><span class="sxs-lookup"><span data-stu-id="ffde7-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ffde7-164">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="ffde7-164">Copy activity properties</span></span>
<span data-ttu-id="ffde7-165">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="ffde7-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ffde7-166">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="ffde7-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ffde7-167">Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="ffde7-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="ffde7-168">Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="ffde7-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="ffde7-169">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="ffde7-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ffde7-170">Se você estiver movendo dados de um banco de dados do SQL Azure, você defina o tipo de fonte de saudação na atividade de cópia de saudação muito**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="ffde7-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="ffde7-171">Da mesma forma, se você estiver movendo o banco de dados do SQL Azure data tooan, você definir o tipo de coletor Olá na atividade de cópia de saudação muito**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ffde7-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="ffde7-172">Esta seção fornece uma lista das propriedades com suporte de SqlSource e SqlSink.</span><span class="sxs-lookup"><span data-stu-id="ffde7-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="ffde7-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="ffde7-173">SqlSource</span></span>
<span data-ttu-id="ffde7-174">Atividade de cópia, quando a fonte de saudação é do tipo **SqlSource**, Olá propriedades a seguir está disponível em **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="ffde7-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="ffde7-175">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ffde7-175">Property</span></span> | <span data-ttu-id="ffde7-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="ffde7-176">Description</span></span> | <span data-ttu-id="ffde7-177">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ffde7-177">Allowed values</span></span> | <span data-ttu-id="ffde7-178">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ffde7-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ffde7-179">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ffde7-179">sqlReaderQuery</span></span> |<span data-ttu-id="ffde7-180">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="ffde7-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ffde7-181">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="ffde7-181">SQL query string.</span></span> <span data-ttu-id="ffde7-182">Exemplo: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="ffde7-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="ffde7-183">Não</span><span class="sxs-lookup"><span data-stu-id="ffde7-183">No</span></span> |
| <span data-ttu-id="ffde7-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ffde7-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ffde7-185">Nome da saudação procedimento armazenado que lê dados da tabela de origem hello.</span><span class="sxs-lookup"><span data-stu-id="ffde7-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="ffde7-186">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffde7-186">Name of hello stored procedure.</span></span> <span data-ttu-id="ffde7-187">Olá a última instrução de SQL deve ser uma instrução SELECT no procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="ffde7-188">Não</span><span class="sxs-lookup"><span data-stu-id="ffde7-188">No</span></span> |
| <span data-ttu-id="ffde7-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ffde7-189">storedProcedureParameters</span></span> |<span data-ttu-id="ffde7-190">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffde7-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ffde7-191">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ffde7-191">Name/value pairs.</span></span> <span data-ttu-id="ffde7-192">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ffde7-193">Não</span><span class="sxs-lookup"><span data-stu-id="ffde7-193">No</span></span> |

<span data-ttu-id="ffde7-194">Se hello **sqlReaderQuery** é especificada para Olá SqlSource, hello atividade de cópia executa esta consulta em relação aos dados de saudação do hello Azure SQL Database fonte tooget.</span><span class="sxs-lookup"><span data-stu-id="ffde7-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="ffde7-195">Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="ffde7-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="ffde7-196">Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de saudação definidas na seção de estrutura de saudação do conjunto de dados Olá JSON são usado toobuild uma consulta (`select column1, column2 from mytable`) toorun contra hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="ffde7-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="ffde7-197">Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="ffde7-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="ffde7-198">Quando você usa **sqlReaderStoredProcedureName**, você ainda precisa toospecify um valor para Olá **tableName** propriedade no conjunto de dados Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="ffde7-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="ffde7-199">Contudo, não há nenhuma validação executada nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="ffde7-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="ffde7-200">Exemplo de SqlSource</span><span class="sxs-lookup"><span data-stu-id="ffde7-200">SqlSource example</span></span>

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

<span data-ttu-id="ffde7-201">**definição do procedimento armazenada de saudação:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-201">**hello stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="ffde7-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="ffde7-202">SqlSink</span></span>
<span data-ttu-id="ffde7-203">**SqlSink** dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffde7-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="ffde7-204">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ffde7-204">Property</span></span> | <span data-ttu-id="ffde7-205">Descrição</span><span class="sxs-lookup"><span data-stu-id="ffde7-205">Description</span></span> | <span data-ttu-id="ffde7-206">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ffde7-206">Allowed values</span></span> | <span data-ttu-id="ffde7-207">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ffde7-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ffde7-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ffde7-208">writeBatchTimeout</span></span> |<span data-ttu-id="ffde7-209">Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="ffde7-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="ffde7-210">timespan</span><span class="sxs-lookup"><span data-stu-id="ffde7-210">timespan</span></span><br/><br/> <span data-ttu-id="ffde7-211">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="ffde7-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ffde7-212">Não</span><span class="sxs-lookup"><span data-stu-id="ffde7-212">No</span></span> |
| <span data-ttu-id="ffde7-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ffde7-213">writeBatchSize</span></span> |<span data-ttu-id="ffde7-214">Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="ffde7-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="ffde7-215">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="ffde7-215">Integer (number of rows)</span></span> |<span data-ttu-id="ffde7-216">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="ffde7-216">No (default: 10000)</span></span> |
| <span data-ttu-id="ffde7-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ffde7-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ffde7-218">Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa.</span><span class="sxs-lookup"><span data-stu-id="ffde7-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="ffde7-219">Para saber mais, consulte [cópia repetida](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ffde7-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ffde7-220">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="ffde7-220">A query statement.</span></span> |<span data-ttu-id="ffde7-221">Não</span><span class="sxs-lookup"><span data-stu-id="ffde7-221">No</span></span> |
| <span data-ttu-id="ffde7-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="ffde7-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="ffde7-223">Especifique um nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente.</span><span class="sxs-lookup"><span data-stu-id="ffde7-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="ffde7-224">Para saber mais, consulte [cópia repetida](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="ffde7-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="ffde7-225">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="ffde7-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="ffde7-226">Não</span><span class="sxs-lookup"><span data-stu-id="ffde7-226">No</span></span> |
| <span data-ttu-id="ffde7-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ffde7-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="ffde7-228">Nome do hello procedimento armazenado dados upserts (atualizações/inserções) na tabela de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="ffde7-229">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffde7-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="ffde7-230">Não</span><span class="sxs-lookup"><span data-stu-id="ffde7-230">No</span></span> |
| <span data-ttu-id="ffde7-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ffde7-231">storedProcedureParameters</span></span> |<span data-ttu-id="ffde7-232">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="ffde7-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="ffde7-233">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="ffde7-233">Name/value pairs.</span></span> <span data-ttu-id="ffde7-234">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="ffde7-235">Não</span><span class="sxs-lookup"><span data-stu-id="ffde7-235">No</span></span> |
| <span data-ttu-id="ffde7-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="ffde7-236">sqlWriterTableType</span></span> |<span data-ttu-id="ffde7-237">Especifique um toobe de nome de tipo de tabela usado no procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="ffde7-238">Atividade de cópia disponibiliza dados Olá movidos em uma tabela temporária com esse tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="ffde7-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="ffde7-239">Código do procedimento armazenado, em seguida, pode mesclar dados de saudação sejam copiados com os dados existentes.</span><span class="sxs-lookup"><span data-stu-id="ffde7-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="ffde7-240">Um nome de tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="ffde7-240">A table type name.</span></span> |<span data-ttu-id="ffde7-241">Não</span><span class="sxs-lookup"><span data-stu-id="ffde7-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="ffde7-242">Exemplo de SqlSink</span><span class="sxs-lookup"><span data-stu-id="ffde7-242">SqlSink example</span></span>

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

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="ffde7-243">Exemplos JSON para copiar dados tooand do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="ffde7-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="ffde7-244">Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ffde7-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ffde7-245">Eles mostram como toocopy tooand de dados do banco de dados do SQL Azure e armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffde7-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="ffde7-246">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="ffde7-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="ffde7-247">Exemplo: Copiar dados de banco de dados do Azure SQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="ffde7-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="ffde7-248">Olá mesmo define Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffde7-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="ffde7-249">Um serviço vinculado do tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ffde7-250">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ffde7-251">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ffde7-252">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ffde7-253">Um [pipeline](data-factory-create-pipelines.md) com uma Atividade de Cópia que usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ffde7-254">exemplo Hello copia dados de série temporal (por hora, diariamente, etc) de uma tabela no blob de tooa de banco de dados do SQL Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffde7-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="ffde7-255">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="ffde7-256">**Serviço vinculado para o Banco de Dados SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-256">**Azure SQL Database linked service:**</span></span>

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
<span data-ttu-id="ffde7-257">Consulte Olá [serviço vinculado do SQL Azure](#linked-service) seção para obter lista de saudação de propriedades com suporte por esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ffde7-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="ffde7-258">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ffde7-259">Consulte Olá [BLOBs do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artigo de lista de saudação de propriedades com suporte por esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ffde7-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="ffde7-260">**Conjunto de dados de entrada do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="ffde7-261">exemplo Hello supõe que você criou uma tabela "MyTable" no SQL Azure e contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="ffde7-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="ffde7-262">Definindo "externo": "verdadeiro" informa serviço do Azure Data Factory Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="ffde7-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="ffde7-263">Consulte Olá [propriedades de tipo de conjunto de dados do SQL Azure](#dataset) seção para obter lista de saudação de propriedades com suporte por este tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ffde7-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ffde7-264">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ffde7-265">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="ffde7-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ffde7-266">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="ffde7-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ffde7-267">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="ffde7-268">Consulte Olá [propriedades de tipo de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) seção para obter lista de saudação de propriedades com suporte por este tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ffde7-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="ffde7-269">**Uma atividade de cópia em um pipeline com origem SQL e coletor de Blob:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="ffde7-270">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffde7-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ffde7-271">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ffde7-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="ffde7-272">consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="ffde7-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
<span data-ttu-id="ffde7-273">No exemplo hello, **sqlReaderQuery** é especificado para Olá SqlSource.</span><span class="sxs-lookup"><span data-stu-id="ffde7-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="ffde7-274">Hello atividade de cópia executa esta consulta Olá dados do banco de dados do Azure SQL origem tooget hello.</span><span class="sxs-lookup"><span data-stu-id="ffde7-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="ffde7-275">Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="ffde7-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="ffde7-276">Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de saudação definidas na seção de estrutura de saudação do conjunto de dados Olá JSON são usado toobuild toorun uma consulta em relação a saudação banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ffde7-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="ffde7-277">Por exemplo: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="ffde7-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="ffde7-278">Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="ffde7-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="ffde7-279">Consulte Olá [fonte Sql](#sqlsource) seção e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de saudação de propriedades com suporte SqlSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="ffde7-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="ffde7-280">Exemplo: Copiar dados de Blob do Azure tooAzure banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="ffde7-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="ffde7-281">exemplo Hello define Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffde7-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="ffde7-282">Um serviço vinculado do tipo [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="ffde7-283">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ffde7-284">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ffde7-285">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="ffde7-286">Um [pipeline](data-factory-create-pipelines.md) com a atividade de Cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ffde7-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ffde7-287">exemplo Hello copia dados de série temporal (por hora, diariamente, etc) da tabela de tooa de BLOBs do Azure no banco de dados do SQL Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffde7-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="ffde7-288">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ffde7-289">**Serviço vinculado do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-289">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="ffde7-290">Consulte Olá [serviço vinculado do SQL Azure](#linked-service) seção para obter lista de saudação de propriedades com suporte por esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ffde7-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="ffde7-291">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ffde7-292">Consulte Olá [BLOBs do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artigo de lista de saudação de propriedades com suporte por esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ffde7-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="ffde7-293">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="ffde7-294">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="ffde7-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ffde7-295">Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="ffde7-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ffde7-296">caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="ffde7-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="ffde7-297">"externo": "verdadeira" configuração informa o serviço de fábrica de dados de saudação que essa tabela é toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="ffde7-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="ffde7-298">Consulte Olá [propriedades de tipo de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) seção para obter lista de saudação de propriedades com suporte por este tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ffde7-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ffde7-299">**Conjunto de dados de saída do Banco de Dados SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="ffde7-300">exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" no SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ffde7-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="ffde7-301">Criar tabela de saudação no SQL Azure com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello.</span><span class="sxs-lookup"><span data-stu-id="ffde7-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="ffde7-302">Novas linhas são adicionadas a tabela de toohello a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffde7-302">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="ffde7-303">Consulte Olá [propriedades de tipo de conjunto de dados do SQL Azure](#dataset) seção para obter lista de saudação de propriedades com suporte por este tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ffde7-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="ffde7-304">**Uma atividade de cópia em um pipeline com origem de Blob e coletor SQL:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="ffde7-305">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ffde7-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ffde7-306">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="ffde7-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

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
<span data-ttu-id="ffde7-307">Consulte Olá [coletor Sql](#sqlsink) seção e [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de saudação de propriedades com suporte do SqlSink e BlobSource.</span><span class="sxs-lookup"><span data-stu-id="ffde7-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="ffde7-308">Colunas de identidade no banco de dados de destino Olá</span><span class="sxs-lookup"><span data-stu-id="ffde7-308">Identity columns in hello target database</span></span>
<span data-ttu-id="ffde7-309">Esta seção fornece um exemplo para copiar dados de uma tabela de origem sem uma tabela de destino identidade coluna tooa com uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="ffde7-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="ffde7-310">**Tabela de origem:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="ffde7-311">**Tabela de destino:**</span><span class="sxs-lookup"><span data-stu-id="ffde7-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="ffde7-312">Observe que essa tabela de destino Olá tem uma coluna de identidade.</span><span class="sxs-lookup"><span data-stu-id="ffde7-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="ffde7-313">**Definição de JSON do conjunto de dados de origem**</span><span class="sxs-lookup"><span data-stu-id="ffde7-313">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="ffde7-314">**Definição de JSON do conjunto de dados de destino**</span><span class="sxs-lookup"><span data-stu-id="ffde7-314">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="ffde7-315">Observe que sua tabela de origem e de destino têm um esquema diferente (a de destino tem uma coluna adicional com identidade).</span><span class="sxs-lookup"><span data-stu-id="ffde7-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="ffde7-316">Nesse cenário, você precisa toospecify **estrutura** propriedade na definição de conjunto de dados de destino hello, que não inclui a coluna de identidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="ffde7-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="ffde7-317">Invocar o procedimento armazenado do coletor SQL</span><span class="sxs-lookup"><span data-stu-id="ffde7-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="ffde7-318">Para obter um exemplo de como invocar um procedimento armazenado do coletor SQL em uma atividade de cópia de um pipeline, confira o artigo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocar procedimento armazenado para coletor SQL na atividade de cópia).</span><span class="sxs-lookup"><span data-stu-id="ffde7-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="ffde7-319">Mapeamento de tipo do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="ffde7-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="ffde7-320">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ffde7-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="ffde7-321">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="ffde7-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="ffde7-322">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="ffde7-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="ffde7-323">Ao mover dados tooand do banco de dados do SQL Azure, hello mapeamentos a seguir são usados do tipo SQL de too.NET e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="ffde7-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="ffde7-324">mapeamento de saudação é igual a saudação mapeamento de tipo de dados do SQL Server do ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="ffde7-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="ffde7-325">Tipo de mecanismo do Banco de Dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="ffde7-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="ffde7-326">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="ffde7-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="ffde7-327">bigint</span><span class="sxs-lookup"><span data-stu-id="ffde7-327">bigint</span></span> |<span data-ttu-id="ffde7-328">Int64</span><span class="sxs-lookup"><span data-stu-id="ffde7-328">Int64</span></span> |
| <span data-ttu-id="ffde7-329">binário</span><span class="sxs-lookup"><span data-stu-id="ffde7-329">binary</span></span> |<span data-ttu-id="ffde7-330">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-330">Byte[]</span></span> |
| <span data-ttu-id="ffde7-331">bit</span><span class="sxs-lookup"><span data-stu-id="ffde7-331">bit</span></span> |<span data-ttu-id="ffde7-332">Booliano</span><span class="sxs-lookup"><span data-stu-id="ffde7-332">Boolean</span></span> |
| <span data-ttu-id="ffde7-333">char</span><span class="sxs-lookup"><span data-stu-id="ffde7-333">char</span></span> |<span data-ttu-id="ffde7-334">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-334">String, Char[]</span></span> |
| <span data-ttu-id="ffde7-335">data</span><span class="sxs-lookup"><span data-stu-id="ffde7-335">date</span></span> |<span data-ttu-id="ffde7-336">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffde7-336">DateTime</span></span> |
| <span data-ttu-id="ffde7-337">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffde7-337">Datetime</span></span> |<span data-ttu-id="ffde7-338">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffde7-338">DateTime</span></span> |
| <span data-ttu-id="ffde7-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="ffde7-339">datetime2</span></span> |<span data-ttu-id="ffde7-340">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffde7-340">DateTime</span></span> |
| <span data-ttu-id="ffde7-341">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="ffde7-341">Datetimeoffset</span></span> |<span data-ttu-id="ffde7-342">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="ffde7-342">DateTimeOffset</span></span> |
| <span data-ttu-id="ffde7-343">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffde7-343">Decimal</span></span> |<span data-ttu-id="ffde7-344">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffde7-344">Decimal</span></span> |
| <span data-ttu-id="ffde7-345">Atributo FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="ffde7-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="ffde7-346">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-346">Byte[]</span></span> |
| <span data-ttu-id="ffde7-347">Float</span><span class="sxs-lookup"><span data-stu-id="ffde7-347">Float</span></span> |<span data-ttu-id="ffde7-348">Duplo</span><span class="sxs-lookup"><span data-stu-id="ffde7-348">Double</span></span> |
| <span data-ttu-id="ffde7-349">imagem</span><span class="sxs-lookup"><span data-stu-id="ffde7-349">image</span></span> |<span data-ttu-id="ffde7-350">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-350">Byte[]</span></span> |
| <span data-ttu-id="ffde7-351">int</span><span class="sxs-lookup"><span data-stu-id="ffde7-351">int</span></span> |<span data-ttu-id="ffde7-352">Int32</span><span class="sxs-lookup"><span data-stu-id="ffde7-352">Int32</span></span> |
| <span data-ttu-id="ffde7-353">money</span><span class="sxs-lookup"><span data-stu-id="ffde7-353">money</span></span> |<span data-ttu-id="ffde7-354">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffde7-354">Decimal</span></span> |
| <span data-ttu-id="ffde7-355">nchar</span><span class="sxs-lookup"><span data-stu-id="ffde7-355">nchar</span></span> |<span data-ttu-id="ffde7-356">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-356">String, Char[]</span></span> |
| <span data-ttu-id="ffde7-357">ntext</span><span class="sxs-lookup"><span data-stu-id="ffde7-357">ntext</span></span> |<span data-ttu-id="ffde7-358">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-358">String, Char[]</span></span> |
| <span data-ttu-id="ffde7-359">numérico</span><span class="sxs-lookup"><span data-stu-id="ffde7-359">numeric</span></span> |<span data-ttu-id="ffde7-360">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffde7-360">Decimal</span></span> |
| <span data-ttu-id="ffde7-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="ffde7-361">nvarchar</span></span> |<span data-ttu-id="ffde7-362">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-362">String, Char[]</span></span> |
| <span data-ttu-id="ffde7-363">real</span><span class="sxs-lookup"><span data-stu-id="ffde7-363">real</span></span> |<span data-ttu-id="ffde7-364">Single</span><span class="sxs-lookup"><span data-stu-id="ffde7-364">Single</span></span> |
| <span data-ttu-id="ffde7-365">rowversion</span><span class="sxs-lookup"><span data-stu-id="ffde7-365">rowversion</span></span> |<span data-ttu-id="ffde7-366">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-366">Byte[]</span></span> |
| <span data-ttu-id="ffde7-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="ffde7-367">smalldatetime</span></span> |<span data-ttu-id="ffde7-368">DateTime</span><span class="sxs-lookup"><span data-stu-id="ffde7-368">DateTime</span></span> |
| <span data-ttu-id="ffde7-369">smallint</span><span class="sxs-lookup"><span data-stu-id="ffde7-369">smallint</span></span> |<span data-ttu-id="ffde7-370">Int16</span><span class="sxs-lookup"><span data-stu-id="ffde7-370">Int16</span></span> |
| <span data-ttu-id="ffde7-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="ffde7-371">smallmoney</span></span> |<span data-ttu-id="ffde7-372">Decimal</span><span class="sxs-lookup"><span data-stu-id="ffde7-372">Decimal</span></span> |
| <span data-ttu-id="ffde7-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="ffde7-373">sql_variant</span></span> |<span data-ttu-id="ffde7-374">Objeto *</span><span class="sxs-lookup"><span data-stu-id="ffde7-374">Object *</span></span> |
| <span data-ttu-id="ffde7-375">texto</span><span class="sxs-lookup"><span data-stu-id="ffde7-375">text</span></span> |<span data-ttu-id="ffde7-376">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-376">String, Char[]</span></span> |
| <span data-ttu-id="ffde7-377">tempo real</span><span class="sxs-lookup"><span data-stu-id="ffde7-377">time</span></span> |<span data-ttu-id="ffde7-378">timespan</span><span class="sxs-lookup"><span data-stu-id="ffde7-378">TimeSpan</span></span> |
| <span data-ttu-id="ffde7-379">timestamp</span><span class="sxs-lookup"><span data-stu-id="ffde7-379">timestamp</span></span> |<span data-ttu-id="ffde7-380">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-380">Byte[]</span></span> |
| <span data-ttu-id="ffde7-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="ffde7-381">tinyint</span></span> |<span data-ttu-id="ffde7-382">Byte</span><span class="sxs-lookup"><span data-stu-id="ffde7-382">Byte</span></span> |
| <span data-ttu-id="ffde7-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="ffde7-383">uniqueidentifier</span></span> |<span data-ttu-id="ffde7-384">Guid</span><span class="sxs-lookup"><span data-stu-id="ffde7-384">Guid</span></span> |
| <span data-ttu-id="ffde7-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="ffde7-385">varbinary</span></span> |<span data-ttu-id="ffde7-386">Byte[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-386">Byte[]</span></span> |
| <span data-ttu-id="ffde7-387">varchar</span><span class="sxs-lookup"><span data-stu-id="ffde7-387">varchar</span></span> |<span data-ttu-id="ffde7-388">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="ffde7-388">String, Char[]</span></span> |
| <span data-ttu-id="ffde7-389">xml</span><span class="sxs-lookup"><span data-stu-id="ffde7-389">xml</span></span> |<span data-ttu-id="ffde7-390">xml</span><span class="sxs-lookup"><span data-stu-id="ffde7-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="ffde7-391">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="ffde7-391">Map source toosink columns</span></span>
<span data-ttu-id="ffde7-392">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ffde7-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="ffde7-393">Cópia repetida</span><span class="sxs-lookup"><span data-stu-id="ffde7-393">Repeatable copy</span></span>
<span data-ttu-id="ffde7-394">Ao copiar dados tooSQL banco de dados do servidor, atividade de cópia de saudação acrescenta a tabela de dados do coletor toohello por padrão.</span><span class="sxs-lookup"><span data-stu-id="ffde7-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="ffde7-395">em vez disso, consulte tooperform um UPSERT [tooSqlSink gravação Repeatable](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artigo.</span><span class="sxs-lookup"><span data-stu-id="ffde7-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="ffde7-396">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="ffde7-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="ffde7-397">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="ffde7-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ffde7-398">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="ffde7-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ffde7-399">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="ffde7-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ffde7-400">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="ffde7-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ffde7-401">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="ffde7-401">Performance and Tuning</span></span>
<span data-ttu-id="ffde7-402">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="ffde7-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
