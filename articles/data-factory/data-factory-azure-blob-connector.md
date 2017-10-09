---
title: aaaCopy dados para/do armazenamento de BLOBs do Azure | Microsoft Docs
description: 'Saiba como toocopy blob dados no Azure Data Factory. Usar nosso exemplo: como toocopy tooand de dados do armazenamento de BLOBs do Azure e banco de dados do SQL Azure.'
keywords: "dados de blob, cópia de blobs do azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="dd79d-105">Copiar dados tooor do armazenamento de BLOBs do Azure usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="dd79d-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="dd79d-106">Este artigo explica como toouse hello atividade de cópia no Azure Data Factory toocopy dados tooand do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="dd79d-107">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="dd79d-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dd79d-108">Overview</span></span>
<span data-ttu-id="dd79d-109">Você pode copiar dados de qualquer fonte com suporte de dados armazenam tooAzure armazenamento de Blob ou em dados de coletor do armazenamento de BLOBs do Azure tooany suporte para armazenam.</span><span class="sxs-lookup"><span data-stu-id="dd79d-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="dd79d-110">Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como fontes ou coletores pela atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="dd79d-111">Por exemplo, você pode mover dados **de** um banco de dados SQL Server ou um de banco de dados SQL do Azure **para** um armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="dd79d-112">Além disso, é possível copiar dados **de** um armazenamento de Blobs do Azure **para** um SQL Data Warehouse do Azure ou uma coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dd79d-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="dd79d-113">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="dd79d-113">Supported scenarios</span></span>
<span data-ttu-id="dd79d-114">Você pode copiar dados **do armazenamento de BLOBs do Azure** toohello repositórios de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="dd79d-115">Você pode copiar dados de saudação armazenamentos de dados a seguir **tooAzure armazenamento de Blob**:</span><span class="sxs-lookup"><span data-stu-id="dd79d-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="dd79d-116">Copiar atividade suporta copiando dados de / tooboth contas de armazenamento do Azure para fins gerais e Hot/interessantes armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="dd79d-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="dd79d-117">Hello atividade dá suporte a **ler de bloco, acrescentar ou blobs de página**, mas oferece suporte a **gravando blobs de bloco tooonly**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="dd79d-118">Não há suporte para armazenamento Premium do Azure como um coletor porque ele é feito por blobs de página.</span><span class="sxs-lookup"><span data-stu-id="dd79d-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="dd79d-119">Atividade de cópia não exclui os dados de origem Olá depois Olá dados com êxito são copiado toohello destino.</span><span class="sxs-lookup"><span data-stu-id="dd79d-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="dd79d-120">Se você precisar de dados de origem toodelete após uma cópia bem-sucedida, criar um [atividade personalizada](data-factory-use-custom-activities.md) toodelete Olá dados e usar a atividade de saudação no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="dd79d-121">Para obter um exemplo, consulte Olá [excluir exemplo de blob ou pasta no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="dd79d-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="dd79d-122">Introdução</span><span class="sxs-lookup"><span data-stu-id="dd79d-122">Get started</span></span>
<span data-ttu-id="dd79d-123">Você pode criar um pipeline com uma atividade de cópia que mova dados de um armazenamento de Blobs do Azure usando ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="dd79d-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="dd79d-124">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="dd79d-125">Este artigo possui uma [passo a passo](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) para criar dados de toocopy um pipeline de um local de armazenamento de BLOBs do Azure tooanother local de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="dd79d-126">Para obter um tutorial sobre como criar dados de toocopy um pipeline de um banco de dados SQL do tooAzure de armazenamento de BLOBs do Azure, consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="dd79d-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="dd79d-127">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="dd79d-128">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="dd79d-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="dd79d-129">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="dd79d-130">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-130">Create a **data factory**.</span></span> <span data-ttu-id="dd79d-131">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="dd79d-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="dd79d-132">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="dd79d-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="dd79d-133">Por exemplo, se você estiver copiando dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure, você criar duas toolink de serviços vinculados sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="dd79d-134">Para propriedades de serviço vinculado que específico tooAzure armazenamento de Blob, consulte [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="dd79d-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="dd79d-135">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="dd79d-136">O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="dd79d-137">E, você cria outra tabela do conjunto de dados toospecify Olá SQL no banco de dados de SQL do Azure de saudação que contém dados Olá copiados saudação do armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="dd79d-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="dd79d-138">Para propriedades de conjunto de dados que são específico tooAzure armazenamento de Blob, consulte [propriedades de conjunto de dados](#dataset-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="dd79d-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="dd79d-139">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="dd79d-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="dd79d-140">Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e do SqlSink como um coletor de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="dd79d-141">Da mesma forma, se você estiver copiando de banco de dados do Azure SQL tooAzure armazenamento de Blob, use SqlSource e BlobSink na atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="dd79d-142">Para propriedades de atividade de cópia que específico tooAzure armazenamento de Blob, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="dd79d-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="dd79d-143">Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="dd79d-144">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="dd79d-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="dd79d-145">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="dd79d-146">Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um armazenamento de BLOBs do Azure, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="dd79d-147">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="dd79d-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="dd79d-148">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="dd79d-148">Linked service properties</span></span>
<span data-ttu-id="dd79d-149">Há dois tipos de serviços vinculados, você pode usar toolink uma fábrica de dados do Azure de tooan de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="dd79d-150">São eles: o serviço vinculado **AzureStorage** e o serviço vinculado **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="dd79d-151">Olá serviço vinculado do armazenamento do Azure fornece a fábrica de dados Olá com acesso global toohello armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="dd79d-152">Enquanto o hello Azure armazenamento SAS (assinatura de acesso compartilhado) vinculado serviço fornece a fábrica de dados Olá com acesso restrito/tempo-limite toohello armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="dd79d-153">Não há outras diferenças entre esses dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="dd79d-154">Escolha o serviço de saudação vinculado que atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="dd79d-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="dd79d-155">Olá seções a seguir fornecem mais detalhes sobre esses dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="dd79d-156">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="dd79d-156">Dataset properties</span></span>
<span data-ttu-id="dd79d-157">toospecify toorepresent um conjunto de dados dados de entrada ou saídos em um armazenamento de BLOBs do Azure, defina propriedade de tipo de saudação do conjunto de dados Olá para: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="dd79d-158">Saudação de conjunto **linkedServiceName** serviço vinculado de propriedade de nome de toohello Olá dataset de saudação armazenamento do Azure ou SAS de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="dd79d-159">Propriedades de tipo de saudação do conjunto de dados Olá especificam Olá **contêiner de blob** e hello **pasta** no armazenamento de blob hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="dd79d-160">Para obter uma lista completa de seções JSON e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="dd79d-161">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="dd79d-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="dd79d-162">Fábrica de dados oferece suporte a saudação seguindo os valores de tipo compatível com CLS .NET com base para fornecer informações de tipo em "structure" para fontes de dados de esquema na leitura como BLOBs do Azure: Int16, Int32, Int64, Single, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="dd79d-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="dd79d-163">Fábrica de dados executa automaticamente conversões de tipo ao mover o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="dd79d-164">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre local hello, etc., formato de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="dd79d-165">Olá typeProperties seção de conjunto de dados do tipo **AzureBlob** conjunto de dados tiver Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="dd79d-166">Propriedade</span><span class="sxs-lookup"><span data-stu-id="dd79d-166">Property</span></span> | <span data-ttu-id="dd79d-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="dd79d-167">Description</span></span> | <span data-ttu-id="dd79d-168">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="dd79d-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd79d-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="dd79d-169">folderPath</span></span> |<span data-ttu-id="dd79d-170">Contêiner de toohello do caminho e a pasta no armazenamento de blob hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="dd79d-171">Exemplo: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="dd79d-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="dd79d-172">Sim</span><span class="sxs-lookup"><span data-stu-id="dd79d-172">Yes</span></span> |
| <span data-ttu-id="dd79d-173">fileName</span><span class="sxs-lookup"><span data-stu-id="dd79d-173">fileName</span></span> |<span data-ttu-id="dd79d-174">Nome do blob hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-174">Name of hello blob.</span></span> <span data-ttu-id="dd79d-175">fileName é opcional e diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="dd79d-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="dd79d-176">Se você especificar um nome de arquivo, hello atividade (incluindo cópia) funciona em Olá Blob específico.</span><span class="sxs-lookup"><span data-stu-id="dd79d-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="dd79d-177">Quando o nome de arquivo não for especificado, cópia inclui todos os Blobs no folderPath Olá para o conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="dd79d-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="dd79d-178">Quando **fileName** não for especificado para um conjunto de dados de saída e **preserveHierarchy** não for especificado no coletor de atividade, nome de saudação do arquivo hello gerado estaria em Olá seguindo este formato: dados.<Guid>. txt (por exemplo:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="dd79d-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="dd79d-179">Não</span><span class="sxs-lookup"><span data-stu-id="dd79d-179">No</span></span> |
| <span data-ttu-id="dd79d-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="dd79d-180">partitionedBy</span></span> |<span data-ttu-id="dd79d-181">partitionedBy é uma propriedade opcional.</span><span class="sxs-lookup"><span data-stu-id="dd79d-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="dd79d-182">Você pode usar-ele toospecify um dinâmico folderPath e filename para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="dd79d-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="dd79d-183">Por exemplo, folderPath pode ser parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="dd79d-184">Consulte Olá [usando a seção de propriedade partitionedBy](#using-partitionedBy-property) para obter detalhes e exemplos.</span><span class="sxs-lookup"><span data-stu-id="dd79d-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="dd79d-185">Não</span><span class="sxs-lookup"><span data-stu-id="dd79d-185">No</span></span> |
| <span data-ttu-id="dd79d-186">formato</span><span class="sxs-lookup"><span data-stu-id="dd79d-186">format</span></span> | <span data-ttu-id="dd79d-187">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="dd79d-188">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="dd79d-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="dd79d-189">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="dd79d-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="dd79d-190">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="dd79d-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="dd79d-191">Não</span><span class="sxs-lookup"><span data-stu-id="dd79d-191">No</span></span> |
| <span data-ttu-id="dd79d-192">compactação</span><span class="sxs-lookup"><span data-stu-id="dd79d-192">compression</span></span> | <span data-ttu-id="dd79d-193">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="dd79d-194">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="dd79d-195">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="dd79d-196">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="dd79d-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="dd79d-197">Não</span><span class="sxs-lookup"><span data-stu-id="dd79d-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="dd79d-198">Usando a propriedade partitionedBy</span><span class="sxs-lookup"><span data-stu-id="dd79d-198">Using partitionedBy property</span></span>
<span data-ttu-id="dd79d-199">Como mencionado na seção anterior hello, você pode especificar um dinâmico folderPath e filename para dados de série temporal com hello **partitionedBy** propriedade [funções da fábrica de dados e variáveis de sistema Olá](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="dd79d-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="dd79d-200">Para saber mais sobre conjuntos de dados de série temporal, agendamento e fatias, veja os artigos [Criando conjuntos de dados](data-factory-create-datasets.md) e [Agendamento e execução](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="dd79d-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="dd79d-201">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="dd79d-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="dd79d-202">Neste exemplo, {Slice} é substituído pelo valor de saudação da variável de sistema SliceStart fábrica de dados no formato de saudação (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="dd79d-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="dd79d-203">Olá SliceStart refere-se toostart tempo da fração de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="dd79d-204">Olá folderPath é diferente para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="dd79d-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="dd79d-205">Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="dd79d-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="dd79d-206">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="dd79d-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="dd79d-207">Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em variáveis separadas que são usadas pelas propriedades folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="dd79d-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="dd79d-208">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="dd79d-208">Copy activity properties</span></span>
<span data-ttu-id="dd79d-209">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="dd79d-210">As propriedades, como nome, descrição, conjuntos de dados de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="dd79d-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="dd79d-211">Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="dd79d-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="dd79d-212">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="dd79d-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="dd79d-213">Se você estiver movendo dados de um armazenamento de BLOBs do Azure, você defina o tipo de fonte de saudação na atividade de cópia de saudação muito**BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="dd79d-214">Da mesma forma, se você estiver movendo dados tooan armazenamento de BLOBs do Azure, você definir o tipo de coletor Olá na atividade de cópia de saudação muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="dd79d-215">Esta seção fornece uma lista das propriedades compatíveis com BlobSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="dd79d-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="dd79d-216">**BlobSource** dá suporte a saudação seguintes propriedades em Olá **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="dd79d-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="dd79d-217">Propriedade</span><span class="sxs-lookup"><span data-stu-id="dd79d-217">Property</span></span> | <span data-ttu-id="dd79d-218">Descrição</span><span class="sxs-lookup"><span data-stu-id="dd79d-218">Description</span></span> | <span data-ttu-id="dd79d-219">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="dd79d-219">Allowed values</span></span> | <span data-ttu-id="dd79d-220">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="dd79d-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dd79d-221">recursiva</span><span class="sxs-lookup"><span data-stu-id="dd79d-221">recursive</span></span> |<span data-ttu-id="dd79d-222">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="dd79d-223">True (valor padrão), False</span><span class="sxs-lookup"><span data-stu-id="dd79d-223">True (default value), False</span></span> |<span data-ttu-id="dd79d-224">Não</span><span class="sxs-lookup"><span data-stu-id="dd79d-224">No</span></span> |

<span data-ttu-id="dd79d-225">**BlobSink** dá suporte a saudação seguintes propriedades **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="dd79d-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="dd79d-226">Propriedade</span><span class="sxs-lookup"><span data-stu-id="dd79d-226">Property</span></span> | <span data-ttu-id="dd79d-227">Descrição</span><span class="sxs-lookup"><span data-stu-id="dd79d-227">Description</span></span> | <span data-ttu-id="dd79d-228">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="dd79d-228">Allowed values</span></span> | <span data-ttu-id="dd79d-229">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="dd79d-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="dd79d-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="dd79d-230">copyBehavior</span></span> |<span data-ttu-id="dd79d-231">Define o comportamento de cópia de saudação quando origem Olá é BlobSource ou sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="dd79d-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="dd79d-232"><b>PreserveHierarchy</b>: preserva Olá hierarquia de arquivos na pasta de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="dd79d-233">caminho relativo do Hello arquivo toosource da pasta de origem é idêntico toohello o caminho relativo da pasta de tootarget do arquivo de destino.</span><span class="sxs-lookup"><span data-stu-id="dd79d-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="dd79d-234"><b>FlattenHierarchy</b>: todos os arquivos da pasta de origem Olá estão em Olá primeiro níveis da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="dd79d-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="dd79d-235">os arquivos de destino de saudação têm nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dd79d-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="dd79d-236"><b>MergeFiles</b>: mescla todos os arquivos Olá pasta tooone do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="dd79d-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="dd79d-237">Se Olá nome de arquivo/Blob for especificado, o nome de arquivo mesclado de Olá seria nome especificado do hello. Caso contrário, seriam nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dd79d-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="dd79d-238">Não</span><span class="sxs-lookup"><span data-stu-id="dd79d-238">No</span></span> |

<span data-ttu-id="dd79d-239">**BlobSource** também oferece suporte a essas duas propriedades para compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="dd79d-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="dd79d-240">**treatEmptyAsNull**: Especifica se tootreat uma cadeia nula ou vazia como valor nulo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="dd79d-241">**skipHeaderLineCount** - Especifica quantas linhas precisam ser ignoradas.</span><span class="sxs-lookup"><span data-stu-id="dd79d-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="dd79d-242">É aplicável somente quando o conjunto de dados de entrada usa TextFormat.</span><span class="sxs-lookup"><span data-stu-id="dd79d-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="dd79d-243">Da mesma forma, **BlobSink** dá suporte a saudação de propriedade para compatibilidade com versões anteriores a seguir.</span><span class="sxs-lookup"><span data-stu-id="dd79d-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="dd79d-244">**blobWriterAddHeader**: Especifica se tooadd um cabeçalho de definições de coluna ao gravar tooan gerar conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="dd79d-245">Saudação de suporte agora de conjuntos de dados seguintes propriedades que implementam Olá a mesma funcionalidade: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="dd79d-246">Olá tabela a seguir fornece orientação sobre como usar as novas propriedades de conjunto de dados Olá no lugar dessas propriedades de fonte/coletor do blob.</span><span class="sxs-lookup"><span data-stu-id="dd79d-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="dd79d-247">Propriedade de Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="dd79d-247">Copy Activity property</span></span> | <span data-ttu-id="dd79d-248">Propriedade de Conjunto de Dados</span><span class="sxs-lookup"><span data-stu-id="dd79d-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="dd79d-249">skipHeaderLineCount em BlobSource</span><span class="sxs-lookup"><span data-stu-id="dd79d-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="dd79d-250">skipLineCount e firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="dd79d-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="dd79d-251">Linhas são ignoradas primeiro e, em seguida, a primeira linha de saudação é lido como um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="dd79d-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="dd79d-252">treatEmptyAsNull em BlobSource</span><span class="sxs-lookup"><span data-stu-id="dd79d-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="dd79d-253">treatEmptyAsNull no conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="dd79d-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="dd79d-254">blobWriterAddHeader em BlobSink</span><span class="sxs-lookup"><span data-stu-id="dd79d-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="dd79d-255">firstRowAsHeader no conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="dd79d-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="dd79d-256">Confira a seção [Especificar TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) para obter informações detalhadas sobre essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="dd79d-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="dd79d-257">exemplos de recursive e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="dd79d-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="dd79d-258">Esta seção descreve o comportamento resultante de saudação da operação de cópia de saudação para diferentes combinações de valores recursiva e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="dd79d-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="dd79d-259">recursiva</span><span class="sxs-lookup"><span data-stu-id="dd79d-259">recursive</span></span> | <span data-ttu-id="dd79d-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="dd79d-260">copyBehavior</span></span> | <span data-ttu-id="dd79d-261">Comportamento resultante</span><span class="sxs-lookup"><span data-stu-id="dd79d-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd79d-262">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="dd79d-262">true</span></span> |<span data-ttu-id="dd79d-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="dd79d-263">preserveHierarchy</span></span> |<span data-ttu-id="dd79d-264">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="dd79d-265">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-265">Folder1</span></span><br/><span data-ttu-id="dd79d-266">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dd79d-267">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dd79d-268">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dd79d-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="dd79d-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dd79d-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="dd79d-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dd79d-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="dd79d-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dd79d-272">pasta de destino de Olá Pasta1 é criada com hello mesma estrutura como fonte de saudação</span><span class="sxs-lookup"><span data-stu-id="dd79d-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="dd79d-273">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-273">Folder1</span></span><br/><span data-ttu-id="dd79d-274">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dd79d-275">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dd79d-276">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dd79d-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="dd79d-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dd79d-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="dd79d-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dd79d-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5.</span><span class="sxs-lookup"><span data-stu-id="dd79d-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="dd79d-280">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="dd79d-280">true</span></span> |<span data-ttu-id="dd79d-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="dd79d-281">flattenHierarchy</span></span> |<span data-ttu-id="dd79d-282">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="dd79d-283">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-283">Folder1</span></span><br/><span data-ttu-id="dd79d-284">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dd79d-285">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dd79d-286">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dd79d-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="dd79d-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dd79d-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="dd79d-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dd79d-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="dd79d-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dd79d-290">destino de saudação Pasta1 é criado com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="dd79d-291">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-291">Folder1</span></span><br/><span data-ttu-id="dd79d-292">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="dd79d-293">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="dd79d-294">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo3</span><span class="sxs-lookup"><span data-stu-id="dd79d-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="dd79d-295">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo4</span><span class="sxs-lookup"><span data-stu-id="dd79d-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="dd79d-296">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo5</span><span class="sxs-lookup"><span data-stu-id="dd79d-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="dd79d-297">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="dd79d-297">true</span></span> |<span data-ttu-id="dd79d-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="dd79d-298">mergeFiles</span></span> |<span data-ttu-id="dd79d-299">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="dd79d-300">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-300">Folder1</span></span><br/><span data-ttu-id="dd79d-301">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dd79d-302">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dd79d-303">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dd79d-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="dd79d-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dd79d-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="dd79d-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dd79d-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="dd79d-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dd79d-307">destino de saudação Pasta1 é criado com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="dd79d-308">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-308">Folder1</span></span><br/><span data-ttu-id="dd79d-309">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 + Arquivo3 + Arquivo4 + Arquivo5 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente</span><span class="sxs-lookup"><span data-stu-id="dd79d-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="dd79d-310">false</span><span class="sxs-lookup"><span data-stu-id="dd79d-310">false</span></span> |<span data-ttu-id="dd79d-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="dd79d-311">preserveHierarchy</span></span> |<span data-ttu-id="dd79d-312">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="dd79d-313">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-313">Folder1</span></span><br/><span data-ttu-id="dd79d-314">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dd79d-315">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dd79d-316">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dd79d-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="dd79d-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dd79d-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="dd79d-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dd79d-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="dd79d-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dd79d-320">pasta de destino de saudação Pasta1 é criada com hello estrutura a seguir</span><span class="sxs-lookup"><span data-stu-id="dd79d-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="dd79d-321">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-321">Folder1</span></span><br/><span data-ttu-id="dd79d-322">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dd79d-323">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="dd79d-324">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="dd79d-325">false</span><span class="sxs-lookup"><span data-stu-id="dd79d-325">false</span></span> |<span data-ttu-id="dd79d-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="dd79d-326">flattenHierarchy</span></span> |<span data-ttu-id="dd79d-327">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="dd79d-328">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-328">Folder1</span></span><br/><span data-ttu-id="dd79d-329">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dd79d-330">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dd79d-331">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dd79d-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="dd79d-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dd79d-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="dd79d-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dd79d-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="dd79d-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dd79d-335">pasta de destino de saudação Pasta1 é criada com hello estrutura a seguir</span><span class="sxs-lookup"><span data-stu-id="dd79d-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="dd79d-336">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-336">Folder1</span></span><br/><span data-ttu-id="dd79d-337">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="dd79d-338">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="dd79d-339">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="dd79d-340">false</span><span class="sxs-lookup"><span data-stu-id="dd79d-340">false</span></span> |<span data-ttu-id="dd79d-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="dd79d-341">mergeFiles</span></span> |<span data-ttu-id="dd79d-342">Para uma pasta de origem Pasta1 com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="dd79d-343">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-343">Folder1</span></span><br/><span data-ttu-id="dd79d-344">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="dd79d-345">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="dd79d-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="dd79d-346">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="dd79d-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="dd79d-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="dd79d-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="dd79d-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="dd79d-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="dd79d-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="dd79d-350">pasta de destino de saudação Pasta1 é criada com hello estrutura a seguir</span><span class="sxs-lookup"><span data-stu-id="dd79d-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="dd79d-351">Pasta1</span><span class="sxs-lookup"><span data-stu-id="dd79d-351">Folder1</span></span><br/><span data-ttu-id="dd79d-352">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dd79d-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="dd79d-353">Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="dd79d-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="dd79d-354">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="dd79d-355">Passo a passo: Dados de toocopy usar o Assistente para cópia para/do armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="dd79d-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="dd79d-356">Vamos examinar como o armazenamento de blob tooquickly copiar dados de um Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="dd79d-357">Neste passo a passo, os armazenamentos de dados de origem e de destino do tipo: Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="dd79d-358">Olá pipeline neste passo a passo copia dados de uma pasta tooanother pasta Olá mesmo contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="dd79d-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="dd79d-359">Este passo a passo é intencionalmente simple tooshow configurações ou propriedades ao usar o armazenamento de Blob como uma fonte ou coletor.</span><span class="sxs-lookup"><span data-stu-id="dd79d-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="dd79d-360">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dd79d-360">Prerequisites</span></span>
1. <span data-ttu-id="dd79d-361">Crie uma **Conta de Armazenamento do Azure** de uso geral caso não tenha uma.</span><span class="sxs-lookup"><span data-stu-id="dd79d-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="dd79d-362">Usar o armazenamento de blob de Olá como ambas **fonte** e **destino** repositório de dados neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="dd79d-363">Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo para toocreate etapas um.</span><span class="sxs-lookup"><span data-stu-id="dd79d-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="dd79d-364">Criar um contêiner de blob denominado **adfblobconnector** na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="dd79d-365">Crie uma pasta chamada **entrada** em Olá **adfblobconnector** contêiner.</span><span class="sxs-lookup"><span data-stu-id="dd79d-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="dd79d-366">Crie um arquivo chamado **emp.txt** com hello a seguir de conteúdo e carregá-lo toohello **entrada** pasta usando ferramentas como [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="dd79d-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="dd79d-367">Criar hello fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="dd79d-367">Create hello data factory</span></span>
1. <span data-ttu-id="dd79d-368">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd79d-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dd79d-369">Clique em **+ novo** no canto superior esquerdo de saudação, clique em **Intelligence + análise**e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="dd79d-370">Em Olá **nova fábrica de dados** folha:</span><span class="sxs-lookup"><span data-stu-id="dd79d-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="dd79d-371">Digite **ADFBlobConnectorDF** para Olá **nome**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="dd79d-372">nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="dd79d-373">Se você receber o erro Olá: `*Data factory name “ADFBlobConnectorDF” is not available`, altere o nome de Olá Olá da fábrica de dados (por exemplo, yournameADFBlobConnectorDF) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="dd79d-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="dd79d-374">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="dd79d-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="dd79d-375">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="dd79d-376">Para o grupo de recursos, selecione **usar existente** tooselect um existente recurso grupo (ou) selecione **criar novo** tooenter um nome para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd79d-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="dd79d-377">Selecione um **local** Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="dd79d-378">Selecione **toodashboard Pin** caixa de seleção na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="dd79d-379">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-379">Click **Create**.</span></span>
3. <span data-ttu-id="dd79d-380">Após a conclusão da criação de saudação, você ver Olá **Data Factory** folha conforme Olá a imagem a seguir: ![homepage de fábrica de dados](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="dd79d-381">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="dd79d-381">Copy Wizard</span></span>
1. <span data-ttu-id="dd79d-382">Na home page do hello fábrica de dados, clique em Olá **copiar dados [visualização]** bloco toolaunch **o Assistente para cópia de dados** em uma guia separada.</span><span class="sxs-lookup"><span data-stu-id="dd79d-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="dd79d-383">Se você vir esse navegador da web hello está preso em "Autorizar...", desabilitar/desmarque **bloquear cookies de terceiros e dados do site** configuração (ou) manter habilitado e criar uma exceção para **login.microsoftonline.com**e tente iniciar o Assistente de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="dd79d-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="dd79d-384">Em Olá **propriedades** página:</span><span class="sxs-lookup"><span data-stu-id="dd79d-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="dd79d-385">Insira **CopyPipeline** para **Nome da tarefa**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="dd79d-386">nome de tarefa Olá é saudação do pipeline de saudação em sua fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="dd79d-387">Insira um **descrição** para tarefas de saudação (opcional).</span><span class="sxs-lookup"><span data-stu-id="dd79d-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="dd79d-388">Para **cadência de tarefa ou o Agendador de tarefas**, lembre-Olá **executado regularmente em agenda** opção.</span><span class="sxs-lookup"><span data-stu-id="dd79d-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="dd79d-389">Se você desejar toorun essa tarefa somente uma vez, em vez de executar repetidamente em um agendamento, selecione **executar uma vez agora**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="dd79d-390">Se você selecionar a opção **Executar uma vez agora**, um [pipeline avulso](data-factory-create-pipelines.md#onetime-pipeline) será criado.</span><span class="sxs-lookup"><span data-stu-id="dd79d-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="dd79d-391">Manter configurações de saudação para **padrão recorrente**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="dd79d-392">Essa tarefa é executada diariamente entre hello começar e terminar vezes você especificar na próxima etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="dd79d-393">Saudação de alteração **data/hora inicial** muito**21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="dd79d-394">Saudação de alteração **data hora de término** muito**25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="dd79d-395">Talvez você queira data de saudação tootype em vez de navegar por meio de calendário hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="dd79d-396">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-396">Click **Next**.</span></span>
      <span data-ttu-id="dd79d-397">![Ferramenta de Cópia – Página Propriedades](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="dd79d-398">Em Olá **repositório de dados de origem** , clique em **armazenamento de BLOBs do Azure** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="dd79d-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="dd79d-399">Você pode usar esse repositório de dados de origem do página toospecify Olá para tarefas de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="dd79d-400">Você pode usar um serviço de repositório de dados vinculado existente ou especificar um novo repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="dd79d-401">serviço vinculado de toouse existente, selecione **de existente serviços vinculados** e selecione Olá serviço vinculado à direita.</span><span class="sxs-lookup"><span data-stu-id="dd79d-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="dd79d-402">![Ferramenta de Cópia – Página do armazenamento de dados de origem](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="dd79d-403">Em Olá **especificar conta de armazenamento de BLOBs do Azure Olá** página:</span><span class="sxs-lookup"><span data-stu-id="dd79d-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="dd79d-404">Manter o nome gerado automaticamente para Olá **nome de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="dd79d-405">nome da conexão de saudação é o nome de saudação do serviço vinculado de saudação do tipo: o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="dd79d-406">Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de conta**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="dd79d-407">Selecione sua assinatura do Azure ou mantenha **Selecionar tudo** para **Assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="dd79d-408">Selecione um **conta de armazenamento do Azure** de saudação lista de armazenamento do Azure contas disponível na assinatura de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="dd79d-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="dd79d-409">Você também pode escolher tooenter configurações de conta de armazenamento manualmente selecionando **inserir manualmente** opção Olá **método de seleção de conta**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="dd79d-410">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-410">Click **Next**.</span></span> 
      <span data-ttu-id="dd79d-411">![Copie a ferramenta - especificar conta de armazenamento de BLOBs do Azure Olá](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="dd79d-412">Em **pasta ou escolha o arquivo de entrada hello** página:</span><span class="sxs-lookup"><span data-stu-id="dd79d-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="dd79d-413">Clique duas vezes em **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="dd79d-414">Selecione **input** e clique em **Escolher**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="dd79d-415">Neste passo a passo, você deve selecionar pasta de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="dd79d-416">Também é possível selecionar arquivo de emp.txt Olá na pasta Olá em vez disso.</span><span class="sxs-lookup"><span data-stu-id="dd79d-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="dd79d-417">![Copie a ferramenta - escolha a pasta ou arquivo de entrada hello](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="dd79d-418">Em Olá **pasta ou escolha o arquivo de entrada hello** página:</span><span class="sxs-lookup"><span data-stu-id="dd79d-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="dd79d-419">Confirme que Olá **arquivo ou pasta** está definido muito**adfblobconnector/entrada**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="dd79d-420">Se os arquivos de saudação em subpastas, por exemplo, 01/04/2017 2017/04/02 e assim por diante, insira adfblobconnector/entrada / {year} / {month} / {day} para o arquivo ou pasta.</span><span class="sxs-lookup"><span data-stu-id="dd79d-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="dd79d-421">Quando você pressionar TAB fora da caixa de texto de saudação, você verá três formatos de tooselect listas suspensas para year (AAAA), month (MM) e dia (dd).</span><span class="sxs-lookup"><span data-stu-id="dd79d-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="dd79d-422">Não defina a opção **Copiar arquivo recursivamente**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="dd79d-423">Selecione completa de toorecursively essa opção através de pastas para arquivos toobe toohello copiado destino.</span><span class="sxs-lookup"><span data-stu-id="dd79d-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="dd79d-424">Olá não **cópia binária** opção.</span><span class="sxs-lookup"><span data-stu-id="dd79d-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="dd79d-425">Selecione essa opção tooperform uma cópia do binária do destino de toohello do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="dd79d-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="dd79d-426">Não selecione para este passo a passo para que você possa ver mais opções na página seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="dd79d-427">Confirme que Olá **tipo de compactação** está definido muito**nenhum**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="dd79d-428">Selecione um valor para essa opção se os arquivos de origem são compactados em um dos formatos de saudação com suporte.</span><span class="sxs-lookup"><span data-stu-id="dd79d-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="dd79d-429">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-429">Click **Next**.</span></span>
    <span data-ttu-id="dd79d-430">![Copie a ferramenta - escolha a pasta ou arquivo de entrada hello](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="dd79d-431">Em Olá **as configurações de formato de arquivo** página, consulte delimitadores hello e esquema de saudação que é detectada automaticamente pelo Assistente de saudação Analisando arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="dd79d-432">Confirmar Olá as opções a seguir: um.</span><span class="sxs-lookup"><span data-stu-id="dd79d-432">Confirm hello following options: a.</span></span> <span data-ttu-id="dd79d-433">Olá **formato de arquivo** está definido muito**formato de texto**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="dd79d-434">Você pode ver todos os formatos de saudação com suporte na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="dd79d-435">Por exemplo: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="dd79d-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="dd79d-436">b.</span><span class="sxs-lookup"><span data-stu-id="dd79d-436">b.</span></span> <span data-ttu-id="dd79d-437">Olá **delimitador de coluna** está definido muito`Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="dd79d-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="dd79d-438">Você pode ver Olá outros delimitadores de coluna que tem suportados pela fábrica de dados na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="dd79d-439">Você também pode especificar um delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="dd79d-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="dd79d-440">c.</span><span class="sxs-lookup"><span data-stu-id="dd79d-440">c.</span></span> <span data-ttu-id="dd79d-441">Olá **delimitador de linha** está definido muito`Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="dd79d-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="dd79d-442">Você pode ver Olá outros delimitadores de linha com suporte pela fábrica de dados na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="dd79d-443">Você também pode especificar um delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="dd79d-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="dd79d-444">d.</span><span class="sxs-lookup"><span data-stu-id="dd79d-444">d.</span></span> <span data-ttu-id="dd79d-445">Olá **Ignorar contagem de linhas** está definido muito**0**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="dd79d-446">Se você quiser alguns toobe de linhas ignorado na parte superior de saudação do arquivo hello, insira o número de saudação aqui.</span><span class="sxs-lookup"><span data-stu-id="dd79d-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="dd79d-447">e.</span><span class="sxs-lookup"><span data-stu-id="dd79d-447">e.</span></span>  <span data-ttu-id="dd79d-448">Olá **primeira linha de dados contém nomes de coluna** não está definido.</span><span class="sxs-lookup"><span data-stu-id="dd79d-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="dd79d-449">Se os arquivos de origem de saudação contêm nomes de coluna na primeira linha de saudação, selecione essa opção.</span><span class="sxs-lookup"><span data-stu-id="dd79d-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="dd79d-450">f.</span><span class="sxs-lookup"><span data-stu-id="dd79d-450">f.</span></span> <span data-ttu-id="dd79d-451">Olá **tratar o valor de coluna vazia como null** opção é definida.</span><span class="sxs-lookup"><span data-stu-id="dd79d-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="dd79d-452">Expanda **configurações avançadas** toosee avançado opção disponível.</span><span class="sxs-lookup"><span data-stu-id="dd79d-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="dd79d-453">Final Olá Olá página, consulte Olá **visualização** de dados de arquivo de emp.txt hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="dd79d-454">Clique em **esquema** guia esquema de Olá Olá inferior toosee esse assistente para cópia de saudação inferido observando Olá dados no arquivo de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="dd79d-455">Clique em **próximo** Após examinar delimitadores hello e visualizar dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="dd79d-456">![Ferramenta de Cópia – Configurações de formato de arquivo](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="dd79d-457">Em Olá **página de repositório de dados de destino**, selecione **armazenamento de BLOBs do Azure**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="dd79d-458">Você está usando Olá armazenamento de BLOBs do Azure como os dois Olá origem e destino armazenamentos de dados neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="dd79d-459">![Ferramenta de Cópia – selecionar o armazenamento de dados de destino](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="dd79d-460">Em **especificar conta de armazenamento de BLOBs do Azure Olá** página:</span><span class="sxs-lookup"><span data-stu-id="dd79d-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="dd79d-461">Digite **AzureStorageLinkedService** para Olá **nome de Conexão** campo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="dd79d-462">Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de conta**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="dd79d-463">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="dd79d-464">Selecione sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="dd79d-465">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-465">Click **Next**.</span></span>     
10. <span data-ttu-id="dd79d-466">Em Olá **Olá Escolher arquivo ou pasta de saída** página:</span><span class="sxs-lookup"><span data-stu-id="dd79d-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="dd79d-467">especifique **Caminho da pasta** como **adfblobconnector/output/{year}/{month}/{day}**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="dd79d-468">Insira **GUIA**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="dd79d-469">Para Olá **ano**, selecione **aaaa**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="dd79d-470">Para Olá **mês**, confirme se ele está definido muito**MM**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="dd79d-471">Para Olá **dia**, confirme se ele está definido muito**dd**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="dd79d-472">Confirme que Olá **tipo de compactação** está definido muito**nenhum**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="dd79d-473">Confirme que Olá **Copiar comportamento** está definido muito**mesclar arquivos**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="dd79d-474">Se Olá saída arquivo com hello mesmo nome já existir, hello novo conteúdo é adicionado toohello mesmo arquivo final hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="dd79d-475">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-475">Click **Next**.</span></span>
    <span data-ttu-id="dd79d-476">![Ferramenta de Cópia – Escolher o arquivo ou a pasta de saída](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="dd79d-477">Em Olá **as configurações de formato de arquivo** , examine as configurações de saudação e, em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="dd79d-478">Uma das opções adicionais Olá aqui é tooadd um arquivo de saída de toohello de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="dd79d-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="dd79d-479">Se você selecionar essa opção, uma linha de cabeçalho é adicionada com nomes de colunas de saudação do esquema de saudação da fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="dd79d-480">Você pode renomear nomes de coluna padrão Olá ao exibir o esquema de saudação para fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="dd79d-481">Por exemplo, você pode alterar Olá tooFirst primeiro da coluna Nome e tooLast da segunda coluna nome.</span><span class="sxs-lookup"><span data-stu-id="dd79d-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="dd79d-482">Em seguida, o arquivo de saída Olá é gerado com um cabeçalho com esses nomes como nomes de coluna.</span><span class="sxs-lookup"><span data-stu-id="dd79d-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="dd79d-483">![Ferramenta de Cópia – Configurações de formato de arquivo para o destino](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="dd79d-484">Em Olá **as configurações de desempenho** , confirme que **unidades em nuvem** e **paralelo cópias** são definidos de forma muito**automática**e clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="dd79d-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="dd79d-485">Para obter detalhes sobre essas configurações, consulte [Guia de desempenho e ajuste da atividade de cópia](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="dd79d-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="dd79d-486">![Ferramenta de Cópia – Configurações de desempenho](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="dd79d-487">Em Olá **resumo** página, examine todas as configurações (Propriedades da tarefa, as configurações de origem e de destino e as configurações de cópias) e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="dd79d-488">![Ferramenta de Cópia – Página Resumo](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="dd79d-489">Revise informações Olá **resumo** página e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="dd79d-490">Assistente de saudação cria um pipeline, dois conjuntos de dados (de entrada e saída) e dois serviços vinculados na fábrica de dados de saudação (a partir de onde você iniciou Olá Assistente para copiar).</span><span class="sxs-lookup"><span data-stu-id="dd79d-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="dd79d-491">![Ferramenta de Cópia – Página Implantação](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="dd79d-492">Pipeline de saudação do Monitor (tarefas de cópia)</span><span class="sxs-lookup"><span data-stu-id="dd79d-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="dd79d-493">Clique em link Olá `Click here toomonitor copy pipeline` em Olá **implantação** página.</span><span class="sxs-lookup"><span data-stu-id="dd79d-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="dd79d-494">Você deve ver Olá **monitorar e gerenciar aplicativos** em uma guia separada.  ![Aplicativo Monitorar e Gerenciar](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="dd79d-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="dd79d-495">Saudação de alteração **iniciar** de tempo na parte superior da saudação muito`04/19/2017` e **final** muito tempo`04/27/2017`e, em seguida, clique em **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="dd79d-496">Você deve ver cinco janelas de atividade no hello **atividade WINDOWS** lista.</span><span class="sxs-lookup"><span data-stu-id="dd79d-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="dd79d-497">Olá **WindowStart** vezes devem abranger todos os dias de horas de término de toopipeline de início do pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd79d-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="dd79d-498">Clique em **atualizar** botão para Olá **atividade WINDOWS** lista algumas vezes até que você veja o status de saudação de todos os períodos de atividade de saudação é definida tooReady.</span><span class="sxs-lookup"><span data-stu-id="dd79d-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="dd79d-499">Agora, verifique se que os arquivos de saída de hello são gerados na pasta de saída de saudação do contêiner adfblobconnector.</span><span class="sxs-lookup"><span data-stu-id="dd79d-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="dd79d-500">Você deve ver Olá estrutura de pastas na pasta de saída de hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="dd79d-501">Para obter informações detalhadas sobre como monitorar e gerenciar data factories, consulte o artigo [Monitorar e gerenciar o pipeline do Data Factory](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="dd79d-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="dd79d-502">Entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="dd79d-502">Data Factory entities</span></span>
<span data-ttu-id="dd79d-503">Agora, alterne toohello back guia com hello Data Factory home page.</span><span class="sxs-lookup"><span data-stu-id="dd79d-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="dd79d-504">Observe que agora há dois serviços vinculados, dois conjuntos de dados e um pipeline no data factory.</span><span class="sxs-lookup"><span data-stu-id="dd79d-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Home page do Data Factory com entidades](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="dd79d-506">Clique em **criar e implantar** toolaunch Editor da fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Editor Data Factory](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="dd79d-508">Você deve ver Olá entidades da fábrica de dados em sua fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="dd79d-509">Dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-509">Two linked services.</span></span> <span data-ttu-id="dd79d-510">Um para origem hello e Olá outro destino hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="dd79d-511">Ambos os serviços vinculado de saudação consulte toohello mesma conta de armazenamento do Azure neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="dd79d-512">Dois conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-512">Two datasets.</span></span> <span data-ttu-id="dd79d-513">Um conjunto de dados de entrada e um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="dd79d-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="dd79d-514">Neste passo a passo, ambos usam Olá mesmo contêiner de blob, mas consulte toodifferent pastas (entrada e saída).</span><span class="sxs-lookup"><span data-stu-id="dd79d-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="dd79d-515">Um pipeline.</span><span class="sxs-lookup"><span data-stu-id="dd79d-515">A pipeline.</span></span> <span data-ttu-id="dd79d-516">pipeline de saudação contém uma atividade de cópia que usa um blob de origem e um blob coletor toocopy os dados de um local de blob do Azure tooanother local de blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="dd79d-517">Olá seções a seguir fornecem mais informações sobre essas entidades.</span><span class="sxs-lookup"><span data-stu-id="dd79d-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="dd79d-518">Serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="dd79d-518">Linked services</span></span>
<span data-ttu-id="dd79d-519">Você deverá ver dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-519">You should see two linked services.</span></span> <span data-ttu-id="dd79d-520">Um para origem hello e Olá outro destino hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="dd79d-521">Neste passo a passo, ambas as definições de aparência Olá mesmo, exceto para nomes de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="dd79d-522">Olá **tipo** Olá serviço vinculado está definido muito**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="dd79d-523">Propriedade mais importante da definição de serviço vinculada de saudação é hello **connectionString**, que é usada pela fábrica de dados tooconnect tooyour conta de armazenamento do Azure em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="dd79d-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="dd79d-524">Ignore a propriedade de hubName Olá na definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="dd79d-525">Serviço vinculado do armazenamento de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="dd79d-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="dd79d-526">Serviço vinculado do armazenamento de blobs de destino</span><span class="sxs-lookup"><span data-stu-id="dd79d-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="dd79d-527">Para obter mais informações sobre o serviço vinculado do Armazenamento do Azure, consulte a seção [Propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="dd79d-528">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="dd79d-528">Datasets</span></span>
<span data-ttu-id="dd79d-529">Há dois conjuntos de dados: um conjunto de dados de entrada e um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="dd79d-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="dd79d-530">tipo de saudação do conjunto de dados hello está definido muito**AzureBlob** para ambos.</span><span class="sxs-lookup"><span data-stu-id="dd79d-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="dd79d-531">conjunto de dados de entrada Hello pontos toohello **entrada** pasta da saudação **adfblobconnector** contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="dd79d-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="dd79d-532">Olá **externo** propriedade for definida muito**true** para este conjunto de dados como Olá dados não são produzidos pelo pipeline de saudação com atividade de cópia de saudação que usa esse conjunto de dados como entrada.</span><span class="sxs-lookup"><span data-stu-id="dd79d-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="dd79d-533">Olá toohello de pontos de conjunto de dados de saída **saída** pasta da saudação mesmo contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="dd79d-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="dd79d-534">Olá conjunto de dados de saída também usa Olá ano, mês e dia da saudação **SliceStart** toodynamically de variável de sistema avaliar caminho Olá Olá arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="dd79d-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="dd79d-535">Para obter uma lista de funções e variáveis de sistema com suporte no Data Factory, consulte [Funções e variáveis de sistema do Data Factory](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="dd79d-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="dd79d-536">Olá **externo** propriedade for definida muito**false** (valor padrão) porque este conjunto de dados é produzido pelo pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="dd79d-537">Para obter mais informações sobre as propriedades com suporte no conjunto de dados de Blobs do Azure, consulte a seção [Propriedades do conjunto de dados](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="dd79d-538">Conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="dd79d-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
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
}
```

##### <a name="output-dataset"></a><span data-ttu-id="dd79d-539">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="dd79d-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="dd79d-540">Pipeline</span><span class="sxs-lookup"><span data-stu-id="dd79d-540">Pipeline</span></span>
<span data-ttu-id="dd79d-541">pipeline de saudação tem apenas uma atividade.</span><span class="sxs-lookup"><span data-stu-id="dd79d-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="dd79d-542">Olá **tipo** hello atividade está definida muito**cópia**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="dd79d-543">Propriedades do tipo hello atividade hello, há duas seções, uma para origem e hello outro para o coletor.</span><span class="sxs-lookup"><span data-stu-id="dd79d-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="dd79d-544">tipo de origem de saudação é definido muito**BlobSource** como atividade hello está copiando dados de um armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="dd79d-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="dd79d-545">Olá tipo de coletor é definido muito**BlobSink** como atividade Olá copiando o armazenamento de blob de tooa de dados.</span><span class="sxs-lookup"><span data-stu-id="dd79d-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="dd79d-546">atividade de cópia de saudação usa InputDataset z4y como entrada hello e OutputDataset-z4y como saída de hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="dd79d-547">Para obter mais informações sobre as propriedades com suporte na BlobSource e no BlobSink, consulte a seção [Propriedades da atividade de cópia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
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
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="dd79d-548">Exemplos JSON para copiar dados tooand do armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="dd79d-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="dd79d-549">Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="dd79d-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="dd79d-550">Eles mostram como toocopy tooand de dados do armazenamento de BLOBs do Azure e banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="dd79d-551">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="dd79d-552">Exemplo JSON: Copiar dados de armazenamento de Blob tooSQL banco de dados</span><span class="sxs-lookup"><span data-stu-id="dd79d-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="dd79d-553">Olá mostra de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-553">hello following sample shows:</span></span>

1. <span data-ttu-id="dd79d-554">Um serviço vinculado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="dd79d-555">Um serviço vinculado do tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="dd79d-556">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="dd79d-557">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="dd79d-558">Um [pipeline](data-factory-create-pipelines.md) com Atividade de cópia que usa [BlobSource](#copy-activity-properties) e [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="dd79d-559">exemplo Hello copia dados de série de tempo de uma tabela do SQL Azure tooan BLOBs do Azure por hora.</span><span class="sxs-lookup"><span data-stu-id="dd79d-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="dd79d-560">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="dd79d-561">**Serviço vinculado do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-561">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="dd79d-562">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-562">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="dd79d-563">O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="dd79d-564">Para Olá primeiro, você especificar a cadeia de caracteres de conexão de saudação que inclui a chave da conta hello e hello mais recente, você especificar Olá Uri de assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="dd79d-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="dd79d-565">Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="dd79d-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="dd79d-566">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="dd79d-567">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="dd79d-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="dd79d-568">Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="dd79d-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="dd79d-569">caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="dd79d-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="dd79d-570">"externo": "verdadeira" configuração informa fábrica de dados tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
<span data-ttu-id="dd79d-571">**Conjunto de dados de saída do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="dd79d-572">exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dd79d-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="dd79d-573">Criar tabela de saudação do banco de dados SQL do Azure com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="dd79d-574">Novas linhas são adicionadas a tabela de toohello a cada hora.</span><span class="sxs-lookup"><span data-stu-id="dd79d-574">New rows are added toohello table every hour.</span></span>

```json
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
<span data-ttu-id="dd79d-575">**Uma atividade de cópia em um pipeline com origem de Blob e coletor SQL:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="dd79d-576">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="dd79d-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="dd79d-577">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
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
            "type": "BlobSource"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="dd79d-578">Exemplo JSON: Copiar dados do SQL Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="dd79d-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="dd79d-579">Olá mostra de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd79d-579">hello following sample shows:</span></span>

1. <span data-ttu-id="dd79d-580">Um serviço vinculado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="dd79d-581">Um serviço vinculado do tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="dd79d-582">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="dd79d-583">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="dd79d-584">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) e [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="dd79d-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="dd79d-585">exemplo Hello copia dados de série temporal de um tooan de tabela do SQL Azure BLOBs do Azure por hora.</span><span class="sxs-lookup"><span data-stu-id="dd79d-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="dd79d-586">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="dd79d-587">**Serviço vinculado do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-587">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="dd79d-588">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-588">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="dd79d-589">O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="dd79d-590">Para Olá primeiro, você especificar a cadeia de caracteres de conexão de saudação que inclui a chave da conta hello e hello mais recente, você especificar Olá Uri de assinatura de acesso compartilhado (SAS).</span><span class="sxs-lookup"><span data-stu-id="dd79d-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="dd79d-591">Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="dd79d-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="dd79d-592">**Conjunto de dados de entrada do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="dd79d-593">exemplo Hello supõe que você criou uma tabela "MyTable" no SQL Azure e contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="dd79d-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="dd79d-594">Definindo "externo": "verdadeiro" informa o serviço de fábrica de dados tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="dd79d-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
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

<span data-ttu-id="dd79d-595">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="dd79d-596">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="dd79d-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="dd79d-597">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="dd79d-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="dd79d-598">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="dd79d-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
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
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

<span data-ttu-id="dd79d-599">**Uma atividade de cópia em um pipeline com origem SQL e coletor de Blob:**</span><span class="sxs-lookup"><span data-stu-id="dd79d-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="dd79d-600">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="dd79d-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="dd79d-601">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="dd79d-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="dd79d-602">consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="dd79d-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
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

> [!NOTE]
> <span data-ttu-id="dd79d-603">colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="dd79d-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="dd79d-604">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="dd79d-604">Performance and Tuning</span></span>
<span data-ttu-id="dd79d-605">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="dd79d-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
