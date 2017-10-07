---
title: aaaCopy dados para/do Azure SQL Data Warehouse | Microsoft Docs
description: Saiba como toocopy dados para/do Azure SQL Data Warehouse usando o Azure Data Factory
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
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="47d69-103">Copiar dados tooand do Azure SQL Data Warehouse usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="47d69-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="47d69-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de/para o Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="47d69-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="47d69-106">tooachieve melhor desempenho, use dados tooload no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="47d69-107">Olá [Use tooload dados no Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) seção tem detalhes.</span><span class="sxs-lookup"><span data-stu-id="47d69-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="47d69-108">Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="47d69-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="47d69-109">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="47d69-109">Supported scenarios</span></span>
<span data-ttu-id="47d69-110">Você pode copiar dados **do Azure SQL Data Warehouse** toohello repositórios de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d69-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="47d69-111">Você pode copiar dados de saudação armazenamentos de dados a seguir **tooAzure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="47d69-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="47d69-112">Ao copiar dados de tooAzure do SQL Server ou banco de dados do SQL Azure SQL Data Warehouse, se a tabela de saudação não existe no repositório de destino hello, fábrica de dados pode criar automaticamente tabela Olá no SQL Data Warehouse usando o esquema de saudação da tabela de saudação na fonte de saudação armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="47d69-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="47d69-113">Consulte [Criação automática de tabela](#auto-table-creation) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="47d69-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="47d69-114">Tipos de autenticação com suporte</span><span class="sxs-lookup"><span data-stu-id="47d69-114">Supported authentication type</span></span>
<span data-ttu-id="47d69-115">O conector do SQL Data Warehouse do Azure dá suporte à autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="47d69-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="47d69-116">Introdução</span><span class="sxs-lookup"><span data-stu-id="47d69-116">Getting started</span></span>
<span data-ttu-id="47d69-117">Você pode criar um pipeline com uma atividade de cópia que mova dados de um banco de dados bidirecionalmente em um SQL Data Warehouse do Azure usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="47d69-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="47d69-118">toocreate de maneira mais fácil de saudação um pipeline que copia dados de/para o Azure SQL Data Warehouse é assistente toouse Olá de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="47d69-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="47d69-119">Consulte [Tutorial: carregar dados no SQL Data Warehouse com o Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="47d69-120">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="47d69-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="47d69-121">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="47d69-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="47d69-122">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d69-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="47d69-123">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="47d69-123">Create a **data factory**.</span></span> <span data-ttu-id="47d69-124">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="47d69-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="47d69-125">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="47d69-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="47d69-126">Por exemplo, se você estiver copiando dados de um data warehouse de BLOBs do Azure storage tooan SQL Azure, você criar duas toolink de serviços vinculados sua conta de armazenamento do Azure e a fábrica de dados do SQL Azure data warehouse tooyour.</span><span class="sxs-lookup"><span data-stu-id="47d69-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="47d69-127">Para propriedades de serviço vinculado que tooAzure específica do SQL Data Warehouse, consulte [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="47d69-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="47d69-128">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="47d69-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="47d69-129">O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="47d69-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="47d69-130">E, você cria outra tabela de saudação de toospecify de conjunto de dados no data warehouse Olá SQL do Azure que contém dados Olá copiados saudação do armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="47d69-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="47d69-131">Para propriedades de conjunto de dados que são específico tooAzure SQL Data Warehouse, consulte [propriedades de conjunto de dados](#dataset-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="47d69-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="47d69-132">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="47d69-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="47d69-133">Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e SqlDWSink como um coletor de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="47d69-134">Da mesma forma, se você está copiando do Azure SQL Data Warehouse tooAzure armazenamento de Blob, use SqlDWSource e BlobSink na atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="47d69-135">Para propriedades de atividade de cópia que tooAzure específica do SQL Data Warehouse, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="47d69-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="47d69-136">Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="47d69-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="47d69-137">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="47d69-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="47d69-138">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="47d69-139">Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um depósito de dados do SQL Azure, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="47d69-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="47d69-140">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="47d69-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="47d69-141">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="47d69-141">Linked service properties</span></span>
<span data-ttu-id="47d69-142">Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooAzure serviço vinculado do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="47d69-143">Propriedade</span><span class="sxs-lookup"><span data-stu-id="47d69-143">Property</span></span> | <span data-ttu-id="47d69-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="47d69-144">Description</span></span> | <span data-ttu-id="47d69-145">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="47d69-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47d69-146">type</span><span class="sxs-lookup"><span data-stu-id="47d69-146">type</span></span> |<span data-ttu-id="47d69-147">propriedade de tipo Hello deve ser definida como: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="47d69-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="47d69-148">Sim</span><span class="sxs-lookup"><span data-stu-id="47d69-148">Yes</span></span> |
| <span data-ttu-id="47d69-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="47d69-149">connectionString</span></span> |<span data-ttu-id="47d69-150">Especifique informações necessárias a instância do tooconnect toohello Azure SQL Data Warehouse para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="47d69-151">Há suporte somente para autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="47d69-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="47d69-152">Sim</span><span class="sxs-lookup"><span data-stu-id="47d69-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="47d69-153">Configurar [Firewall de banco de dados do SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) e Olá o servidor de banco de dados muito[permitir que serviços do Azure tooaccess Olá servidor](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="47d69-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="47d69-154">Além disso, se você estiver copiando dados tooAzure SQL Data Warehouse incluindo Azure fora de fontes de dados local com o gateway da fábrica de dados, configure o intervalo de endereços IP apropriado para a máquina de saudação que está enviando dados tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="47d69-155">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="47d69-155">Dataset properties</span></span>
<span data-ttu-id="47d69-156">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="47d69-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="47d69-157">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="47d69-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="47d69-158">seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="47d69-159">Olá **typeProperties** seção de conjunto de dados de saudação do tipo **AzureSqlDWTable** tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d69-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="47d69-160">Propriedade</span><span class="sxs-lookup"><span data-stu-id="47d69-160">Property</span></span> | <span data-ttu-id="47d69-161">Descrição</span><span class="sxs-lookup"><span data-stu-id="47d69-161">Description</span></span> | <span data-ttu-id="47d69-162">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="47d69-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47d69-163">tableName</span><span class="sxs-lookup"><span data-stu-id="47d69-163">tableName</span></span> |<span data-ttu-id="47d69-164">Nome da tabela de saudação ou exibição no banco de dados de Data warehouse do SQL Azure de saudação que Olá serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="47d69-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="47d69-165">Sim</span><span class="sxs-lookup"><span data-stu-id="47d69-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="47d69-166">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="47d69-166">Copy activity properties</span></span>
<span data-ttu-id="47d69-167">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="47d69-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="47d69-168">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="47d69-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="47d69-169">Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="47d69-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="47d69-170">Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="47d69-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="47d69-171">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="47d69-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="47d69-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="47d69-172">SqlDWSource</span></span>
<span data-ttu-id="47d69-173">Quando a fonte é do tipo **SqlDWSource**, Olá propriedades a seguir está disponível em **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="47d69-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="47d69-174">Propriedade</span><span class="sxs-lookup"><span data-stu-id="47d69-174">Property</span></span> | <span data-ttu-id="47d69-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="47d69-175">Description</span></span> | <span data-ttu-id="47d69-176">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="47d69-176">Allowed values</span></span> | <span data-ttu-id="47d69-177">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="47d69-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="47d69-178">SqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="47d69-178">sqlReaderQuery</span></span> |<span data-ttu-id="47d69-179">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="47d69-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="47d69-180">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="47d69-180">SQL query string.</span></span> <span data-ttu-id="47d69-181">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="47d69-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="47d69-182">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-182">No</span></span> |
| <span data-ttu-id="47d69-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="47d69-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="47d69-184">Nome da saudação procedimento armazenado que lê dados da tabela de origem hello.</span><span class="sxs-lookup"><span data-stu-id="47d69-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="47d69-185">Nome da saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="47d69-185">Name of hello stored procedure.</span></span> <span data-ttu-id="47d69-186">Olá a última instrução de SQL deve ser uma instrução SELECT no procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="47d69-187">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-187">No</span></span> |
| <span data-ttu-id="47d69-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="47d69-188">storedProcedureParameters</span></span> |<span data-ttu-id="47d69-189">Parâmetros de saudação de procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="47d69-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="47d69-190">Pares de nome/valor.</span><span class="sxs-lookup"><span data-stu-id="47d69-190">Name/value pairs.</span></span> <span data-ttu-id="47d69-191">Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="47d69-192">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-192">No</span></span> |

<span data-ttu-id="47d69-193">Se hello **sqlReaderQuery** é especificada para Olá SqlDWSource, hello atividade de cópia executa esta consulta em relação a saudação dados do Azure SQL Data Warehouse origem tooget Olá.</span><span class="sxs-lookup"><span data-stu-id="47d69-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="47d69-194">Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="47d69-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="47d69-195">Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de saudação definidas na seção de estrutura de saudação do conjunto de dados Olá JSON são usado toobuild toorun uma consulta em relação a hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="47d69-196">Exemplo: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="47d69-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="47d69-197">Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="47d69-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="47d69-198">Exemplo de SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="47d69-198">SqlDWSource example</span></span>

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
<span data-ttu-id="47d69-199">**definição do procedimento armazenada de saudação:**</span><span class="sxs-lookup"><span data-stu-id="47d69-199">**hello stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="47d69-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="47d69-200">SqlDWSink</span></span>
<span data-ttu-id="47d69-201">**SqlDWSink** dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d69-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="47d69-202">Propriedade</span><span class="sxs-lookup"><span data-stu-id="47d69-202">Property</span></span> | <span data-ttu-id="47d69-203">Descrição</span><span class="sxs-lookup"><span data-stu-id="47d69-203">Description</span></span> | <span data-ttu-id="47d69-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="47d69-204">Allowed values</span></span> | <span data-ttu-id="47d69-205">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="47d69-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="47d69-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="47d69-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="47d69-207">Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa.</span><span class="sxs-lookup"><span data-stu-id="47d69-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="47d69-208">Para obter detalhes, consulte a [seção de repetição](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="47d69-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="47d69-209">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="47d69-209">A query statement.</span></span> |<span data-ttu-id="47d69-210">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-210">No</span></span> |
| <span data-ttu-id="47d69-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="47d69-211">allowPolyBase</span></span> |<span data-ttu-id="47d69-212">Indica se toouse PolyBase (quando aplicável) em vez de mecanismo BULKINSERT.</span><span class="sxs-lookup"><span data-stu-id="47d69-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="47d69-213">**Usar o PolyBase é hello recomendado a maneira como os dados tooload no SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="47d69-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="47d69-214">Consulte [Use tooload dados no Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) seção de detalhes e restrições.</span><span class="sxs-lookup"><span data-stu-id="47d69-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="47d69-215">Verdadeiro</span><span class="sxs-lookup"><span data-stu-id="47d69-215">True</span></span> <br/><span data-ttu-id="47d69-216">False (padrão)</span><span class="sxs-lookup"><span data-stu-id="47d69-216">False (default)</span></span> |<span data-ttu-id="47d69-217">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-217">No</span></span> |
| <span data-ttu-id="47d69-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="47d69-218">polyBaseSettings</span></span> |<span data-ttu-id="47d69-219">Um grupo de propriedades que podem ser especificadas ao hello **allowPolybase** propriedade for definida muito**true**.</span><span class="sxs-lookup"><span data-stu-id="47d69-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="47d69-220">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-220">No</span></span> |
| <span data-ttu-id="47d69-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="47d69-221">rejectValue</span></span> |<span data-ttu-id="47d69-222">Especifica o número de saudação ou a porcentagem de linhas que pode ser rejeitada antes Olá consulta falhe.</span><span class="sxs-lookup"><span data-stu-id="47d69-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="47d69-223">Saiba mais sobre do PolyBase Olá rejeitar opções Olá **argumentos** seção [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="47d69-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="47d69-224">0 (padrão), 1, 2, …</span><span class="sxs-lookup"><span data-stu-id="47d69-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="47d69-225">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-225">No</span></span> |
| <span data-ttu-id="47d69-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="47d69-226">rejectType</span></span> |<span data-ttu-id="47d69-227">Especifica se a opção de rejectValue de saudação é especificada como um valor literal ou uma porcentagem.</span><span class="sxs-lookup"><span data-stu-id="47d69-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="47d69-228">Valor (padrão), Percentual</span><span class="sxs-lookup"><span data-stu-id="47d69-228">Value (default), Percentage</span></span> |<span data-ttu-id="47d69-229">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-229">No</span></span> |
| <span data-ttu-id="47d69-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="47d69-230">rejectSampleValue</span></span> |<span data-ttu-id="47d69-231">Determina o número de saudação de linhas tooretrieve antes Olá PolyBase recalcula a porcentagem de saudação de linhas rejeitadas.</span><span class="sxs-lookup"><span data-stu-id="47d69-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="47d69-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="47d69-232">1, 2, …</span></span> |<span data-ttu-id="47d69-233">Sim, se **rejectType** for **percentual**</span><span class="sxs-lookup"><span data-stu-id="47d69-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="47d69-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="47d69-234">useTypeDefault</span></span> |<span data-ttu-id="47d69-235">Especifica como toohandle faltando valores delimitados por arquivos de texto quando PolyBase recupera dados do arquivo de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="47d69-236">Saiba mais sobre essa propriedade da seção argumentos Olá [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="47d69-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="47d69-237">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="47d69-237">True, False (default)</span></span> |<span data-ttu-id="47d69-238">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-238">No</span></span> |
| <span data-ttu-id="47d69-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="47d69-239">writeBatchSize</span></span> |<span data-ttu-id="47d69-240">Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="47d69-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="47d69-241">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="47d69-241">Integer (number of rows)</span></span> |<span data-ttu-id="47d69-242">Não (padrão: 10000)</span><span class="sxs-lookup"><span data-stu-id="47d69-242">No (default: 10000)</span></span> |
| <span data-ttu-id="47d69-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="47d69-243">writeBatchTimeout</span></span> |<span data-ttu-id="47d69-244">Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="47d69-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="47d69-245">timespan</span><span class="sxs-lookup"><span data-stu-id="47d69-245">timespan</span></span><br/><br/> <span data-ttu-id="47d69-246">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="47d69-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="47d69-247">Não</span><span class="sxs-lookup"><span data-stu-id="47d69-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="47d69-248">Exemplo de SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="47d69-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="47d69-249">Usar dados tooload no Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="47d69-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="47d69-250">Usar o **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** é uma maneira eficiente de carregar grandes quantidades de dados no SQL Data Warehouse do Azure com alta taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="47d69-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="47d69-251">Você pode ver um ganho grande na taxa de transferência hello usando PolyBase em vez do mecanismo BULKINSERT saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="47d69-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="47d69-252">Veja [número de referência do desempenho de cópia](data-factory-copy-activity-performance.md#performance-reference) com comparação detalhada.</span><span class="sxs-lookup"><span data-stu-id="47d69-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="47d69-253">Para ver um passo a passo com um caso de uso, veja [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) (Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="47d69-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="47d69-254">Se sua fonte de dados está em **BLOBs do Azure ou do repositório Azure Data Lake**e formato de saudação é compatível com o PolyBase, você pode copiar diretamente tooAzure SQL Data Warehouse usando PolyBase.</span><span class="sxs-lookup"><span data-stu-id="47d69-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="47d69-255">Veja **[Cópia direta usando o PolyBase](#direct-copy-using-polybase)** com detalhes.</span><span class="sxs-lookup"><span data-stu-id="47d69-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="47d69-256">Se o repositório de dados de origem e o formato não tiver suporte originalmente pelo PolyBase, você pode usar o hello  **[cópia testados usando PolyBase](#staged-copy-using-polybase)**  recurso em vez disso.</span><span class="sxs-lookup"><span data-stu-id="47d69-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="47d69-257">Ele também fornece melhor taxa de transferência automaticamente converter dados de saudação em formato compatível com o PolyBase e armazenando dados saudação no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="47d69-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="47d69-258">Em seguida, ele carrega os dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="47d69-259">Saudação de conjunto `allowPolyBase` propriedade muito**true** conforme mostrado no seguinte exemplo para o Azure Data Factory toouse toocopy dados no Azure SQL Data Warehouse de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="47d69-260">Quando você define allowPolyBase tootrue, você pode especificar propriedades específicas do PolyBase usando Olá `polyBaseSettings` grupo de propriedades.</span><span class="sxs-lookup"><span data-stu-id="47d69-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="47d69-261">Consulte Olá [SqlDWSink](#SqlDWSink) seção para obter detalhes sobre as propriedades que você pode usar com polyBaseSettings.</span><span class="sxs-lookup"><span data-stu-id="47d69-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="47d69-262">Cópia direta usando o PolyBase</span><span class="sxs-lookup"><span data-stu-id="47d69-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="47d69-263">O SQL Data Warehouse PolyBase dá suporte diretamente ao Blob do Azure e ao Azure Data Lake Store (usando a entidade de serviço) como origem e com os requisitos de formato de arquivo específico.</span><span class="sxs-lookup"><span data-stu-id="47d69-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="47d69-264">Se sua fonte de dados atende aos critérios de saudação descritos nesta seção, você pode copiar diretamente da fonte tooAzure de repositório de dados que do SQL Data Warehouse usando PolyBase.</span><span class="sxs-lookup"><span data-stu-id="47d69-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="47d69-265">Caso contrário, poderá aproveitar a [Cópia de preparo usando o PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="47d69-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="47d69-266">toocopy dados do repositório Data Lake tooSQL Data Warehouse com eficiência, saiba mais de [do Azure Data Factory torna insights toouncover mais fácil e conveniente de dados, mesmo ao usar o repositório Data Lake com o SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="47d69-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="47d69-267">Se Olá requisitos não forem atendidos, o Azure Data Factory verifica as configurações de saudação e automaticamente reverterá toohello mecanismo BULKINSERT Olá para movimentação de dados.</span><span class="sxs-lookup"><span data-stu-id="47d69-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="47d69-268">O **serviço vinculado de origem** é do tipo: **AzureStorage** ou **AzureDataLakeStore com autenticação da entidade de serviço**.</span><span class="sxs-lookup"><span data-stu-id="47d69-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="47d69-269">Olá **conjunto de dados de entrada** é do tipo: **AzureBlob** ou **AzureDataLakeStore**, e Olá tipo de formato em `type` propriedades é **OrcFormat** , ou **TextFormat** com hello configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d69-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="47d69-270">`rowDelimiter` deve ser **\n**.</span><span class="sxs-lookup"><span data-stu-id="47d69-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="47d69-271">`nullValue`está definido muito**cadeia de caracteres vazia** (""), ou `treatEmptyAsNull` está definido muito**true**.</span><span class="sxs-lookup"><span data-stu-id="47d69-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="47d69-272">`encodingName`está definido muito**utf-8**, que é **padrão** valor.</span><span class="sxs-lookup"><span data-stu-id="47d69-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="47d69-273">`escapeChar`, `quoteChar`, `firstRowAsHeader` e `skipLineCount` não foram especificados.</span><span class="sxs-lookup"><span data-stu-id="47d69-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="47d69-274">`compression` pode ser **sem compactação**, **GZip** ou **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="47d69-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="47d69-275">Não há nenhum `skipHeaderLineCount` em **BlobSource** ou **AzureDataLakeStore** para hello atividade de cópia no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="47d69-276">Não há nenhum `sliceIdentifierColumnName` em **SqlDWSink** para hello atividade de cópia no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="47d69-277">(O PolyBase garante que todos os dados são atualizados ou que nada é atualizado em uma execução única.</span><span class="sxs-lookup"><span data-stu-id="47d69-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="47d69-278">tooachieve **repetibilidade**, você pode usar `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="47d69-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="47d69-279">Não há nenhum `columnMapping` que está sendo usado em Olá associado na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="47d69-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="47d69-280">Cópia de preparo usando o PolyBase</span><span class="sxs-lookup"><span data-stu-id="47d69-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="47d69-281">Quando sua fonte de dados não atendem aos critérios de saudação apresentados na seção anterior hello, você pode habilitar a cópia de dados por meio de um armazenamento de Blob de preparo do Azure provisório (não pode ser o armazenamento Premium).</span><span class="sxs-lookup"><span data-stu-id="47d69-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="47d69-282">Nesse caso, Azure Data Factory automaticamente executa transformações em Olá dados toomeet formato requisitos de dados de PolyBase e, em seguida, use dados tooload no SQL Data Warehouse e no último limpar seus dados temporários saudação do armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="47d69-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="47d69-283">Confira [Cópia de Preparo](data-factory-copy-activity-performance.md#staged-copy) para obter detalhes sobre como copiar dados por meio de um trabalho de preparo do Blob do Azure em geral.</span><span class="sxs-lookup"><span data-stu-id="47d69-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="47d69-284">Quando copiar dados de um local de dados armazenam no Azure SQL Data Warehouse usando PolyBase e preparação, se a sua versão do Gateway de gerenciamento de dados está abaixo 2.4, o JRE (Java Runtime Environment) é necessária no gateway do computador que é usado tootransform sua fonte de dados em formato adequado.</span><span class="sxs-lookup"><span data-stu-id="47d69-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="47d69-285">Sugerir que atualizar seu tooavoid mais recente do gateway toohello tal dependência.</span><span class="sxs-lookup"><span data-stu-id="47d69-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="47d69-286">toouse esse recurso, criar um [serviço vinculado do armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) que se refere a toohello conta de armazenamento do Azure que tem o armazenamento de blob provisório hello, especifique Olá `enableStaging` e `stagingSettings` propriedades para hello atividade de cópia conforme mostrado na saudação de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d69-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="47d69-287">Práticas recomendadas ao usar o PolyBase</span><span class="sxs-lookup"><span data-stu-id="47d69-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="47d69-288">Olá seções a seguir fornecem toohello de práticas recomendada adicionais que são mencionados na [práticas recomendadas para o Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="47d69-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="47d69-289">Permissão de banco de dados obrigatória</span><span class="sxs-lookup"><span data-stu-id="47d69-289">Required database permission</span></span>
<span data-ttu-id="47d69-290">toouse PolyBase, ele requer Olá usuário que está sendo usado tooload dados no SQL Data Warehouse tem Olá [permissão "CONTROL"](https://msdn.microsoft.com/library/ms191291.aspx) no banco de dados de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="47d69-291">Tooachieve unidirecional que é tooadd esse usuário como um membro da função "db_owner".</span><span class="sxs-lookup"><span data-stu-id="47d69-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="47d69-292">Saiba como toodo que seguindo [nesta seção](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="47d69-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="47d69-293">Limitação de tamanho da linha e tipo de dados</span><span class="sxs-lookup"><span data-stu-id="47d69-293">Row size and data type limitation</span></span>
<span data-ttu-id="47d69-294">Cargas de Polybase estão limitadas tooloading linhas ambos menor do que **1 MB** e não é possível carregar tooVARCHR(MAX), nvarchar (max) ou varbinary (max).</span><span class="sxs-lookup"><span data-stu-id="47d69-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="47d69-295">Consulte também[aqui](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="47d69-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="47d69-296">Se você tiver dados de origem com linhas de tamanho maior que 1 MB, convém tabelas de origem toosplit Olá verticalmente em várias partes pequenas onde maior tamanho de linha hello de cada um deles não exceda o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="47d69-297">tabelas menores Hello, em seguida, podem ser carregadas usando PolyBase e mesclados no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="47d69-298">Classe de recursos do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="47d69-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="47d69-299">tooachieve melhor transferência possíveis, considere tooassign maior recurso classe toohello usuário sendo tooload de dados usados no SQL Data Warehouse por meio do PolyBase.</span><span class="sxs-lookup"><span data-stu-id="47d69-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="47d69-300">Saiba como toodo que seguindo [alterar um exemplo de classe de recurso de usuário](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="47d69-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="47d69-301">tableName no Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="47d69-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="47d69-302">Olá tabela a seguir fornece exemplos de como Olá toospecify **tableName** propriedade no conjunto de dados JSON para várias combinações de nome de esquema e tabela.</span><span class="sxs-lookup"><span data-stu-id="47d69-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="47d69-303">Esquema do BD</span><span class="sxs-lookup"><span data-stu-id="47d69-303">DB Schema</span></span> | <span data-ttu-id="47d69-304">Nome da tabela</span><span class="sxs-lookup"><span data-stu-id="47d69-304">Table name</span></span> | <span data-ttu-id="47d69-305">Propriedade JSON tableName</span><span class="sxs-lookup"><span data-stu-id="47d69-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="47d69-306">dbo</span><span class="sxs-lookup"><span data-stu-id="47d69-306">dbo</span></span> |<span data-ttu-id="47d69-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="47d69-307">MyTable</span></span> |<span data-ttu-id="47d69-308">MyTable ou dbo.MyTable ou [dbo].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="47d69-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="47d69-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="47d69-309">dbo1</span></span> |<span data-ttu-id="47d69-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="47d69-310">MyTable</span></span> |<span data-ttu-id="47d69-311">dbo1.MyTable ou [dbo1].[MyTable]</span><span class="sxs-lookup"><span data-stu-id="47d69-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="47d69-312">dbo</span><span class="sxs-lookup"><span data-stu-id="47d69-312">dbo</span></span> |<span data-ttu-id="47d69-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="47d69-313">My.Table</span></span> |<span data-ttu-id="47d69-314">[My.Table] ou [dbo].[My.Table]</span><span class="sxs-lookup"><span data-stu-id="47d69-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="47d69-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="47d69-315">dbo1</span></span> |<span data-ttu-id="47d69-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="47d69-316">My.Table</span></span> |<span data-ttu-id="47d69-317">[dbo1]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="47d69-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="47d69-318">Se você vir Olá erro a seguir, pode ser um problema com valor de saudação especificado para a propriedade tableName de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="47d69-319">Consulte a tabela Olá Olá maneira correta toospecify valores para a propriedade do hello tableName JSON.</span><span class="sxs-lookup"><span data-stu-id="47d69-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="47d69-320">Colunas com valores padrão</span><span class="sxs-lookup"><span data-stu-id="47d69-320">Columns with default values</span></span>
<span data-ttu-id="47d69-321">Atualmente, só aceita um recurso na fábrica de dados de PolyBase Olá mesmo número de colunas na tabela de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="47d69-322">Digamos que você tenha uma tabela com quatro colunas e uma delas esteja definida com um valor padrão.</span><span class="sxs-lookup"><span data-stu-id="47d69-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="47d69-323">dados de entrada Hello ainda devem conter quatro colunas.</span><span class="sxs-lookup"><span data-stu-id="47d69-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="47d69-324">Fornecer um conjunto de dados de entrada de 3-coluna produziria uma toohello semelhante erro seguinte mensagem:</span><span class="sxs-lookup"><span data-stu-id="47d69-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="47d69-325">O valor NULL é uma forma especial do valor padrão.</span><span class="sxs-lookup"><span data-stu-id="47d69-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="47d69-326">Se a coluna de saudação é anulável, dados de entrada hello (de blob) para essa coluna podem ser vazios (não pode estar ausente da saudação conjunto de dados de entrada).</span><span class="sxs-lookup"><span data-stu-id="47d69-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="47d69-327">PolyBase insere NULL para eles no hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="47d69-328">Criação automática de tabela</span><span class="sxs-lookup"><span data-stu-id="47d69-328">Auto table creation</span></span>
<span data-ttu-id="47d69-329">Se você estiver usando o Assistente de cópia toocopy dados do SQL Server ou banco de dados do Azure SQL tooAzure SQL Data Warehouse e hello tabela que corresponde a tabela de origem toohello não existem no repositório de destino hello, fábrica de dados pode criar automaticamente tabela Olá em Olá depósito de dados usando o esquema de tabela de origem hello.</span><span class="sxs-lookup"><span data-stu-id="47d69-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="47d69-330">Fábrica de dados cria a tabela de saudação no repositório de destino Olá com hello mesmo nome no repositório de dados de origem de saudação da tabela.</span><span class="sxs-lookup"><span data-stu-id="47d69-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="47d69-331">tipos de dados Olá para colunas são escolhidos com base em Olá mapeamento de tipo a seguir.</span><span class="sxs-lookup"><span data-stu-id="47d69-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="47d69-332">Se necessário, ele executa toofix de conversões de tipo quaisquer incompatibilidades entre repositórios de origem e de destino.</span><span class="sxs-lookup"><span data-stu-id="47d69-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="47d69-333">Ele também usa a distribuição de tabelas em um Round Robin.</span><span class="sxs-lookup"><span data-stu-id="47d69-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="47d69-334">Tipo de coluna do Banco de Dados SQL da origem</span><span class="sxs-lookup"><span data-stu-id="47d69-334">Source SQL Database column type</span></span> | <span data-ttu-id="47d69-335">Tipo de coluna do SQL DW de destino (limitação de tamanho)</span><span class="sxs-lookup"><span data-stu-id="47d69-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="47d69-336">int</span><span class="sxs-lookup"><span data-stu-id="47d69-336">Int</span></span> | <span data-ttu-id="47d69-337">int</span><span class="sxs-lookup"><span data-stu-id="47d69-337">Int</span></span> |
| <span data-ttu-id="47d69-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="47d69-338">BigInt</span></span> | <span data-ttu-id="47d69-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="47d69-339">BigInt</span></span> |
| <span data-ttu-id="47d69-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="47d69-340">SmallInt</span></span> | <span data-ttu-id="47d69-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="47d69-341">SmallInt</span></span> |
| <span data-ttu-id="47d69-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="47d69-342">TinyInt</span></span> | <span data-ttu-id="47d69-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="47d69-343">TinyInt</span></span> |
| <span data-ttu-id="47d69-344">Bit</span><span class="sxs-lookup"><span data-stu-id="47d69-344">Bit</span></span> | <span data-ttu-id="47d69-345">Bit</span><span class="sxs-lookup"><span data-stu-id="47d69-345">Bit</span></span> |
| <span data-ttu-id="47d69-346">Decimal</span><span class="sxs-lookup"><span data-stu-id="47d69-346">Decimal</span></span> | <span data-ttu-id="47d69-347">Decimal</span><span class="sxs-lookup"><span data-stu-id="47d69-347">Decimal</span></span> |
| <span data-ttu-id="47d69-348">Numérico</span><span class="sxs-lookup"><span data-stu-id="47d69-348">Numeric</span></span> | <span data-ttu-id="47d69-349">Decimal</span><span class="sxs-lookup"><span data-stu-id="47d69-349">Decimal</span></span> |
| <span data-ttu-id="47d69-350">Float</span><span class="sxs-lookup"><span data-stu-id="47d69-350">Float</span></span> | <span data-ttu-id="47d69-351">Float</span><span class="sxs-lookup"><span data-stu-id="47d69-351">Float</span></span> |
| <span data-ttu-id="47d69-352">Money</span><span class="sxs-lookup"><span data-stu-id="47d69-352">Money</span></span> | <span data-ttu-id="47d69-353">Money</span><span class="sxs-lookup"><span data-stu-id="47d69-353">Money</span></span> |
| <span data-ttu-id="47d69-354">Real</span><span class="sxs-lookup"><span data-stu-id="47d69-354">Real</span></span> | <span data-ttu-id="47d69-355">Real</span><span class="sxs-lookup"><span data-stu-id="47d69-355">Real</span></span> |
| <span data-ttu-id="47d69-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="47d69-356">SmallMoney</span></span> | <span data-ttu-id="47d69-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="47d69-357">SmallMoney</span></span> |
| <span data-ttu-id="47d69-358">Binário</span><span class="sxs-lookup"><span data-stu-id="47d69-358">Binary</span></span> | <span data-ttu-id="47d69-359">Binário</span><span class="sxs-lookup"><span data-stu-id="47d69-359">Binary</span></span> |
| <span data-ttu-id="47d69-360">Varbinary</span><span class="sxs-lookup"><span data-stu-id="47d69-360">Varbinary</span></span> | <span data-ttu-id="47d69-361">Varbinary (até too8000)</span><span class="sxs-lookup"><span data-stu-id="47d69-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="47d69-362">Data</span><span class="sxs-lookup"><span data-stu-id="47d69-362">Date</span></span> | <span data-ttu-id="47d69-363">Data</span><span class="sxs-lookup"><span data-stu-id="47d69-363">Date</span></span> |
| <span data-ttu-id="47d69-364">DateTime</span><span class="sxs-lookup"><span data-stu-id="47d69-364">DateTime</span></span> | <span data-ttu-id="47d69-365">DateTime</span><span class="sxs-lookup"><span data-stu-id="47d69-365">DateTime</span></span> |
| <span data-ttu-id="47d69-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="47d69-366">DateTime2</span></span> | <span data-ttu-id="47d69-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="47d69-367">DateTime2</span></span> |
| <span data-ttu-id="47d69-368">Hora</span><span class="sxs-lookup"><span data-stu-id="47d69-368">Time</span></span> | <span data-ttu-id="47d69-369">Hora</span><span class="sxs-lookup"><span data-stu-id="47d69-369">Time</span></span> |
| <span data-ttu-id="47d69-370">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="47d69-370">DateTimeOffset</span></span> | <span data-ttu-id="47d69-371">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="47d69-371">DateTimeOffset</span></span> |
| <span data-ttu-id="47d69-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="47d69-372">SmallDateTime</span></span> | <span data-ttu-id="47d69-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="47d69-373">SmallDateTime</span></span> |
| <span data-ttu-id="47d69-374">Texto</span><span class="sxs-lookup"><span data-stu-id="47d69-374">Text</span></span> | <span data-ttu-id="47d69-375">Varchar (até too8000)</span><span class="sxs-lookup"><span data-stu-id="47d69-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="47d69-376">NText</span><span class="sxs-lookup"><span data-stu-id="47d69-376">NText</span></span> | <span data-ttu-id="47d69-377">NVarChar (até too4000)</span><span class="sxs-lookup"><span data-stu-id="47d69-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="47d69-378">Imagem</span><span class="sxs-lookup"><span data-stu-id="47d69-378">Image</span></span> | <span data-ttu-id="47d69-379">VarBinary (até too8000)</span><span class="sxs-lookup"><span data-stu-id="47d69-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="47d69-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="47d69-380">UniqueIdentifier</span></span> | <span data-ttu-id="47d69-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="47d69-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="47d69-382">Char</span><span class="sxs-lookup"><span data-stu-id="47d69-382">Char</span></span> | <span data-ttu-id="47d69-383">Char</span><span class="sxs-lookup"><span data-stu-id="47d69-383">Char</span></span> |
| <span data-ttu-id="47d69-384">NChar</span><span class="sxs-lookup"><span data-stu-id="47d69-384">NChar</span></span> | <span data-ttu-id="47d69-385">NChar</span><span class="sxs-lookup"><span data-stu-id="47d69-385">NChar</span></span> |
| <span data-ttu-id="47d69-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="47d69-386">VarChar</span></span> | <span data-ttu-id="47d69-387">VarChar (até too8000)</span><span class="sxs-lookup"><span data-stu-id="47d69-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="47d69-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="47d69-388">NVarChar</span></span> | <span data-ttu-id="47d69-389">NVarChar (até too4000)</span><span class="sxs-lookup"><span data-stu-id="47d69-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="47d69-390">xml</span><span class="sxs-lookup"><span data-stu-id="47d69-390">Xml</span></span> | <span data-ttu-id="47d69-391">Varchar (até too8000)</span><span class="sxs-lookup"><span data-stu-id="47d69-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="47d69-392">Mapeamento de tipo do SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="47d69-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="47d69-393">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d69-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="47d69-394">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="47d69-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="47d69-395">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="47d69-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="47d69-396">Ao mover dados muito & do Azure SQL Data Warehouse, hello mapeamentos a seguir são usados do tipo SQL de too.NET e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="47d69-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="47d69-397">mapeamento de saudação é igual a saudação [mapeamento de tipo de dados do SQL Server do ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="47d69-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="47d69-398">Tipo de mecanismo do Banco de Dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="47d69-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="47d69-399">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="47d69-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="47d69-400">bigint</span><span class="sxs-lookup"><span data-stu-id="47d69-400">bigint</span></span> |<span data-ttu-id="47d69-401">Int64</span><span class="sxs-lookup"><span data-stu-id="47d69-401">Int64</span></span> |
| <span data-ttu-id="47d69-402">binário</span><span class="sxs-lookup"><span data-stu-id="47d69-402">binary</span></span> |<span data-ttu-id="47d69-403">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47d69-403">Byte[]</span></span> |
| <span data-ttu-id="47d69-404">bit</span><span class="sxs-lookup"><span data-stu-id="47d69-404">bit</span></span> |<span data-ttu-id="47d69-405">Booliano</span><span class="sxs-lookup"><span data-stu-id="47d69-405">Boolean</span></span> |
| <span data-ttu-id="47d69-406">char</span><span class="sxs-lookup"><span data-stu-id="47d69-406">char</span></span> |<span data-ttu-id="47d69-407">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47d69-407">String, Char[]</span></span> |
| <span data-ttu-id="47d69-408">data</span><span class="sxs-lookup"><span data-stu-id="47d69-408">date</span></span> |<span data-ttu-id="47d69-409">DateTime</span><span class="sxs-lookup"><span data-stu-id="47d69-409">DateTime</span></span> |
| <span data-ttu-id="47d69-410">DateTime</span><span class="sxs-lookup"><span data-stu-id="47d69-410">Datetime</span></span> |<span data-ttu-id="47d69-411">DateTime</span><span class="sxs-lookup"><span data-stu-id="47d69-411">DateTime</span></span> |
| <span data-ttu-id="47d69-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="47d69-412">datetime2</span></span> |<span data-ttu-id="47d69-413">DateTime</span><span class="sxs-lookup"><span data-stu-id="47d69-413">DateTime</span></span> |
| <span data-ttu-id="47d69-414">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="47d69-414">Datetimeoffset</span></span> |<span data-ttu-id="47d69-415">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="47d69-415">DateTimeOffset</span></span> |
| <span data-ttu-id="47d69-416">Decimal</span><span class="sxs-lookup"><span data-stu-id="47d69-416">Decimal</span></span> |<span data-ttu-id="47d69-417">Decimal</span><span class="sxs-lookup"><span data-stu-id="47d69-417">Decimal</span></span> |
| <span data-ttu-id="47d69-418">Atributo FILESTREAM (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="47d69-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="47d69-419">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47d69-419">Byte[]</span></span> |
| <span data-ttu-id="47d69-420">Float</span><span class="sxs-lookup"><span data-stu-id="47d69-420">Float</span></span> |<span data-ttu-id="47d69-421">Duplo</span><span class="sxs-lookup"><span data-stu-id="47d69-421">Double</span></span> |
| <span data-ttu-id="47d69-422">imagem</span><span class="sxs-lookup"><span data-stu-id="47d69-422">image</span></span> |<span data-ttu-id="47d69-423">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47d69-423">Byte[]</span></span> |
| <span data-ttu-id="47d69-424">int</span><span class="sxs-lookup"><span data-stu-id="47d69-424">int</span></span> |<span data-ttu-id="47d69-425">Int32</span><span class="sxs-lookup"><span data-stu-id="47d69-425">Int32</span></span> |
| <span data-ttu-id="47d69-426">money</span><span class="sxs-lookup"><span data-stu-id="47d69-426">money</span></span> |<span data-ttu-id="47d69-427">Decimal</span><span class="sxs-lookup"><span data-stu-id="47d69-427">Decimal</span></span> |
| <span data-ttu-id="47d69-428">nchar</span><span class="sxs-lookup"><span data-stu-id="47d69-428">nchar</span></span> |<span data-ttu-id="47d69-429">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47d69-429">String, Char[]</span></span> |
| <span data-ttu-id="47d69-430">ntext</span><span class="sxs-lookup"><span data-stu-id="47d69-430">ntext</span></span> |<span data-ttu-id="47d69-431">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47d69-431">String, Char[]</span></span> |
| <span data-ttu-id="47d69-432">numérico</span><span class="sxs-lookup"><span data-stu-id="47d69-432">numeric</span></span> |<span data-ttu-id="47d69-433">Decimal</span><span class="sxs-lookup"><span data-stu-id="47d69-433">Decimal</span></span> |
| <span data-ttu-id="47d69-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="47d69-434">nvarchar</span></span> |<span data-ttu-id="47d69-435">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47d69-435">String, Char[]</span></span> |
| <span data-ttu-id="47d69-436">real</span><span class="sxs-lookup"><span data-stu-id="47d69-436">real</span></span> |<span data-ttu-id="47d69-437">Single</span><span class="sxs-lookup"><span data-stu-id="47d69-437">Single</span></span> |
| <span data-ttu-id="47d69-438">rowversion</span><span class="sxs-lookup"><span data-stu-id="47d69-438">rowversion</span></span> |<span data-ttu-id="47d69-439">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47d69-439">Byte[]</span></span> |
| <span data-ttu-id="47d69-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="47d69-440">smalldatetime</span></span> |<span data-ttu-id="47d69-441">DateTime</span><span class="sxs-lookup"><span data-stu-id="47d69-441">DateTime</span></span> |
| <span data-ttu-id="47d69-442">smallint</span><span class="sxs-lookup"><span data-stu-id="47d69-442">smallint</span></span> |<span data-ttu-id="47d69-443">Int16</span><span class="sxs-lookup"><span data-stu-id="47d69-443">Int16</span></span> |
| <span data-ttu-id="47d69-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="47d69-444">smallmoney</span></span> |<span data-ttu-id="47d69-445">Decimal</span><span class="sxs-lookup"><span data-stu-id="47d69-445">Decimal</span></span> |
| <span data-ttu-id="47d69-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="47d69-446">sql_variant</span></span> |<span data-ttu-id="47d69-447">Objeto *</span><span class="sxs-lookup"><span data-stu-id="47d69-447">Object *</span></span> |
| <span data-ttu-id="47d69-448">texto</span><span class="sxs-lookup"><span data-stu-id="47d69-448">text</span></span> |<span data-ttu-id="47d69-449">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47d69-449">String, Char[]</span></span> |
| <span data-ttu-id="47d69-450">tempo real</span><span class="sxs-lookup"><span data-stu-id="47d69-450">time</span></span> |<span data-ttu-id="47d69-451">timespan</span><span class="sxs-lookup"><span data-stu-id="47d69-451">TimeSpan</span></span> |
| <span data-ttu-id="47d69-452">timestamp</span><span class="sxs-lookup"><span data-stu-id="47d69-452">timestamp</span></span> |<span data-ttu-id="47d69-453">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47d69-453">Byte[]</span></span> |
| <span data-ttu-id="47d69-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="47d69-454">tinyint</span></span> |<span data-ttu-id="47d69-455">Byte</span><span class="sxs-lookup"><span data-stu-id="47d69-455">Byte</span></span> |
| <span data-ttu-id="47d69-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="47d69-456">uniqueidentifier</span></span> |<span data-ttu-id="47d69-457">Guid</span><span class="sxs-lookup"><span data-stu-id="47d69-457">Guid</span></span> |
| <span data-ttu-id="47d69-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="47d69-458">varbinary</span></span> |<span data-ttu-id="47d69-459">Byte[]</span><span class="sxs-lookup"><span data-stu-id="47d69-459">Byte[]</span></span> |
| <span data-ttu-id="47d69-460">varchar</span><span class="sxs-lookup"><span data-stu-id="47d69-460">varchar</span></span> |<span data-ttu-id="47d69-461">String, Char[]</span><span class="sxs-lookup"><span data-stu-id="47d69-461">String, Char[]</span></span> |
| <span data-ttu-id="47d69-462">xml</span><span class="sxs-lookup"><span data-stu-id="47d69-462">xml</span></span> |<span data-ttu-id="47d69-463">xml</span><span class="sxs-lookup"><span data-stu-id="47d69-463">Xml</span></span> |

<span data-ttu-id="47d69-464">Você também pode mapear colunas de origem toocolumns de conjunto de dados do conjunto de coletor de dados na definição de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="47d69-465">Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="47d69-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="47d69-466">Exemplos JSON para copiar dados tooand do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="47d69-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="47d69-467">Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="47d69-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="47d69-468">Eles mostram como toocopy tooand de dados do Azure SQL Data Warehouse e o armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="47d69-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="47d69-469">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="47d69-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="47d69-470">Exemplo: Copiar dados do Azure SQL Data Warehouse tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="47d69-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="47d69-471">exemplo Hello define Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d69-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="47d69-472">Um serviço vinculado do tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="47d69-473">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="47d69-474">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="47d69-475">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="47d69-476">O [pipeline](data-factory-create-pipelines.md) com a Atividade de cópia que usa [SqlDWSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="47d69-477">exemplo Hello copia dados de série temporal (por hora, diariamente, etc.) de uma tabela no blob do Azure SQL Data Warehouse banco de dados tooa a cada hora.</span><span class="sxs-lookup"><span data-stu-id="47d69-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="47d69-478">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="47d69-479">**Serviço vinculado do SQL Data Warehouse do Azure:**</span><span class="sxs-lookup"><span data-stu-id="47d69-479">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="47d69-480">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="47d69-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="47d69-481">**Conjunto de dados de entrada do SQL Data Warehouse do Azure:**</span><span class="sxs-lookup"><span data-stu-id="47d69-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="47d69-482">exemplo Hello supõe que você criou uma tabela "MyTable" no Azure SQL Data Warehouse e contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="47d69-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="47d69-483">Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="47d69-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="47d69-484">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="47d69-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="47d69-485">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="47d69-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="47d69-486">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="47d69-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="47d69-487">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="47d69-488">**Atividade de cópia em um pipeline com SqlDWSource e BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="47d69-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="47d69-489">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="47d69-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="47d69-490">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlDWSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="47d69-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="47d69-491">consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="47d69-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
> <span data-ttu-id="47d69-492">No exemplo hello, **sqlReaderQuery** é especificado para Olá SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="47d69-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="47d69-493">Hello atividade de cópia executa esta consulta Olá dados do Azure SQL Data Warehouse origem tooget hello.</span><span class="sxs-lookup"><span data-stu-id="47d69-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="47d69-494">Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).</span><span class="sxs-lookup"><span data-stu-id="47d69-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="47d69-495">Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de saudação definidas na seção de estrutura de saudação do conjunto de dados Olá JSON são usado toobuild uma consulta (selecione column1, column2 de mytable) toorun contra hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="47d69-496">Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="47d69-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="47d69-497">Exemplo: Copiar dados de tooAzure de BLOBs do Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="47d69-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="47d69-498">exemplo Hello define Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="47d69-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="47d69-499">Um serviço vinculado do tipo [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="47d69-500">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="47d69-501">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="47d69-502">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="47d69-503">Um [pipeline](data-factory-create-pipelines.md) com Atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="47d69-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="47d69-504">exemplo Hello copia dados de série temporal (por hora, diariamente, etc) da tabela de tooa de BLOBs do Azure no banco de dados do Azure SQL Data Warehouse, a cada hora.</span><span class="sxs-lookup"><span data-stu-id="47d69-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="47d69-505">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="47d69-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="47d69-506">**Serviço vinculado do SQL Data Warehouse do Azure:**</span><span class="sxs-lookup"><span data-stu-id="47d69-506">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="47d69-507">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="47d69-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="47d69-508">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="47d69-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="47d69-509">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="47d69-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="47d69-510">Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="47d69-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="47d69-511">caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="47d69-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="47d69-512">"externo": "verdadeira" configuração informa o serviço de fábrica de dados de saudação que essa tabela é toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="47d69-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="47d69-513">**Conjunto de dados de saída do SQL Data Warehouse do Azure:**</span><span class="sxs-lookup"><span data-stu-id="47d69-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="47d69-514">exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="47d69-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="47d69-515">Criar tabela de saudação no Azure SQL Data Warehouse com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello.</span><span class="sxs-lookup"><span data-stu-id="47d69-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="47d69-516">Novas linhas são adicionadas a tabela de toohello a cada hora.</span><span class="sxs-lookup"><span data-stu-id="47d69-516">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="47d69-517">**Atividade de cópia em um pipeline com BlobSource e SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="47d69-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="47d69-518">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="47d69-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="47d69-519">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="47d69-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

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
<span data-ttu-id="47d69-520">Para obter instruções, consulte Olá [carregar 1 TB no Azure SQL Data Warehouse em 15 minutos com o Azure Data Factory](data-factory-load-sql-data-warehouse.md) e [carregar os dados com o Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artigo hello Azure SQL Data Warehouse documentação.</span><span class="sxs-lookup"><span data-stu-id="47d69-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="47d69-521">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="47d69-521">Performance and Tuning</span></span>
<span data-ttu-id="47d69-522">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="47d69-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
