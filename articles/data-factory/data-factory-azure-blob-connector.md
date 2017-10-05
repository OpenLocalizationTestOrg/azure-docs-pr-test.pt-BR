---
title: Copiar dados de/para o Armazenamento de Blobs do Azure | Microsoft Docs
description: Saiba como copiar dados de blob no Azure Data Factory. O(s) exemplo(s) a seguir mostra(m) como copiar dados de e para o Armazenamento de Blobs do Azure e o Banco de Dados SQL do Azure.
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
ms.openlocfilehash: 2cf955b52010869a4e753c441e17bdd32fd2e63d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="aff00-105">Copie os dados de ou para o Armazenamento de Blobs do Azure usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="aff00-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="aff00-106">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para copiar dados de e para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span></span> <span data-ttu-id="aff00-107">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="aff00-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="aff00-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="aff00-108">Overview</span></span>
<span data-ttu-id="aff00-109">Você pode copiar dados de qualquer armazenamento de dados de origem com suporte para o armazenamento de Blobs do Azure ou do armazenamento de Blobs do Azure para qualquer armazenamento de dados do coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="aff00-109">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="aff00-110">A tabela a seguir fornece uma lista de armazenamentos de dados com suporte como fontes ou coletores na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="aff00-110">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span></span> <span data-ttu-id="aff00-111">Por exemplo, você pode mover dados **de** um banco de dados SQL Server ou um de banco de dados SQL do Azure **para** um armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="aff00-112">Além disso, é possível copiar dados **de** um armazenamento de Blobs do Azure **para** um SQL Data Warehouse do Azure ou uma coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aff00-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="aff00-113">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="aff00-113">Supported scenarios</span></span>
<span data-ttu-id="aff00-114">Você pode copiar dados **do Armazenamento de Blobs do Azure** para os seguintes armazenamentos de dados:</span><span class="sxs-lookup"><span data-stu-id="aff00-114">You can copy data **from Azure Blob Storage** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="aff00-115">Você pode copiar dados dos seguintes armazenamentos de dados **para um Armazenamento de Blobs do Azure**:</span><span class="sxs-lookup"><span data-stu-id="aff00-115">You can copy data from the following data stores **to Azure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="aff00-116">A Atividade de Cópia dá suporte à cópia de dados de/para contas de Armazenamento do Azure para fins gerais e para o Armazenamento de Blobs Dinâmico/Estático.</span><span class="sxs-lookup"><span data-stu-id="aff00-116">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="aff00-117">A atividade dá suporte à **leitura de blobs de bloco, de acréscimo ou de página**, mas dá suporte à **gravação apenas em blobs de blocos**.</span><span class="sxs-lookup"><span data-stu-id="aff00-117">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span></span> <span data-ttu-id="aff00-118">Não há suporte para armazenamento Premium do Azure como um coletor porque ele é feito por blobs de página.</span><span class="sxs-lookup"><span data-stu-id="aff00-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="aff00-119">A atividade de cópia não exclui os dados de origem depois que eles são copiados com êxito para o destino.</span><span class="sxs-lookup"><span data-stu-id="aff00-119">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span></span> <span data-ttu-id="aff00-120">Se você precisar excluir os dados de origem após uma cópia bem-sucedida, crie uma [atividade personalizada](data-factory-use-custom-activities.md) para excluir os dados e use a atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="aff00-120">If you need to delete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) to delete the data and use the activity in the pipeline.</span></span> <span data-ttu-id="aff00-121">Para obter um exemplo, consulte [Excluir exemplo de blob ou pasta no GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="aff00-121">For an example, see the [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="aff00-122">Introdução</span><span class="sxs-lookup"><span data-stu-id="aff00-122">Get started</span></span>
<span data-ttu-id="aff00-123">Você pode criar um pipeline com uma atividade de cópia que mova dados de um armazenamento de Blobs do Azure usando ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="aff00-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="aff00-124">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="aff00-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="aff00-125">Este artigo tem um [passo a passo](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) para criar um pipeline para copiar dados de um local Armazenamento de Blobs do Azure para outro.</span><span class="sxs-lookup"><span data-stu-id="aff00-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span></span> <span data-ttu-id="aff00-126">Para encontrar um tutorial sobre a criação de um pipeline para copiar dados de um Armazenamento de Blobs do Azure para o Banco de Dados SQL do Azure, consulte [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="aff00-126">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="aff00-127">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="aff00-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="aff00-128">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="aff00-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="aff00-129">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="aff00-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="aff00-130">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="aff00-130">Create a **data factory**.</span></span> <span data-ttu-id="aff00-131">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="aff00-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="aff00-132">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-132">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="aff00-133">Por exemplo, se você está copiando dados de um Armazenamento de Blobs do Azure para um Banco de Dados SQL do Azure, crie dois serviços vinculados para vincular sua Conta de Armazenamento do Azure e o Banco de Dados SQL do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-133">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="aff00-134">Para propriedades do serviço vinculado que são específicas do Armazenamento de Blobs do Azure, consulte a seção de [propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-134">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="aff00-135">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="aff00-135">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="aff00-136">No exemplo mencionado na última etapa, você cria um conjunto de dados para especificar o contêiner de blobs e a pasta que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="aff00-136">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="aff00-137">Em seguida, você cria outro conjunto de dados para especificar a tabela SQL no Banco de Dados SQL do Azure que contém os dados copiados do Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="aff00-137">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span></span> <span data-ttu-id="aff00-138">Para propriedades do conjunto de dados que são específicas do Armazenamento de Blobs do Azure, consulte a seção de [propriedades do conjunto de dados](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-138">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="aff00-139">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="aff00-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="aff00-140">No exemplo mencionado anteriormente, você usa BlobSource como fonte e SqlSink como coletor para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="aff00-140">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="aff00-141">De modo similar, se estiver copiando do Banco de Dados SQL do Azure para o Armazenamento de Blobs do Azure, você usará SqlSource e BlobSink na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="aff00-141">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="aff00-142">Para propriedades da atividade de cópia que são específicas do Armazenamento de Blobs do Azure, consulte a seção de [propriedades da atividade de cópia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-142">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="aff00-143">Para obter detalhes sobre como usar um armazenamento de dados como uma origem ou um coletor, clique no link na seção anterior para o seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="aff00-143">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="aff00-144">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="aff00-144">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="aff00-145">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="aff00-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="aff00-146">Para obter exemplos com definições de JSON das entidades do Data Factory usadas para copiar dados bidirecionalmente em um Armazenamento de Blobs do Azure, confira a seção [Exemplos de JSON](#json-examples-for-copying-data-to-and-from-blob-storage  ) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="aff00-146">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="aff00-147">As seções a seguir fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-147">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="aff00-148">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="aff00-148">Linked service properties</span></span>
<span data-ttu-id="aff00-149">Existem dois tipos de serviço vinculado que você pode usar para vincular um Armazenamento do Azure a um Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-149">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="aff00-150">São eles: o serviço vinculado **AzureStorage** e o serviço vinculado **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="aff00-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="aff00-151">O serviço vinculado do Armazenamento do Azure fornece o data factory com acesso global ao Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-151">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="aff00-152">Já o serviço vinculado SAS (Assinatura de Acesso Compartilhado) do Armazenamento do Azure fornece o data factory com acesso restrito/associado ao tempo ao Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-152">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="aff00-153">Não há outras diferenças entre esses dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="aff00-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="aff00-154">Escolha o serviço vinculado que atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="aff00-154">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="aff00-155">As seções a seguir fornecem mais detalhes sobre esses dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="aff00-155">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="aff00-156">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="aff00-156">Dataset properties</span></span>
<span data-ttu-id="aff00-157">Para especificar um conjunto de dados de modo a representar dados de entrada ou saída em um Armazenamento de Blobs do Azure, defina a propriedade de tipo do conjunto de dados para: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="aff00-157">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="aff00-158">Defina a propriedade **linkedServiceName** do conjunto de dados para o nome do Armazenamento do Azure ou do serviço vinculado de SAS do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-158">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="aff00-159">As propriedades de tipo do conjunto de dados especificam o **contêiner de blob** e a **pasta** no Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="aff00-159">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="aff00-160">Para obter uma lista completa das seções e propriedades JSON disponíveis para definir conjuntos de dados, consulte o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="aff00-160">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="aff00-161">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="aff00-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="aff00-162">O Data Factory dá suporte aos valores de tipo baseados em .NET em conformidade com CLS a seguir, para fornecer informações de tipo em "estrutura" para fontes de dados em que o esquema é definido na leitura, assim como o blob do Azure: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="aff00-162">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="aff00-163">O Data Factory executa conversões de tipo automaticamente ao mover dados de um armazenamento de dados de origem para um armazenamento de dados do coletor.</span><span class="sxs-lookup"><span data-stu-id="aff00-163">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="aff00-164">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre a localização, o formato etc. dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="aff00-164">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="aff00-165">A seção typeProperties para o conjunto de dados do tipo **AzureBlob** tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="aff00-165">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="aff00-166">Propriedade</span><span class="sxs-lookup"><span data-stu-id="aff00-166">Property</span></span> | <span data-ttu-id="aff00-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="aff00-167">Description</span></span> | <span data-ttu-id="aff00-168">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="aff00-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="aff00-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="aff00-169">folderPath</span></span> |<span data-ttu-id="aff00-170">Caminho para o contêiner e a pasta no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="aff00-170">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="aff00-171">Exemplo: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="aff00-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="aff00-172">Sim</span><span class="sxs-lookup"><span data-stu-id="aff00-172">Yes</span></span> |
| <span data-ttu-id="aff00-173">fileName</span><span class="sxs-lookup"><span data-stu-id="aff00-173">fileName</span></span> |<span data-ttu-id="aff00-174">O nome do blob.</span><span class="sxs-lookup"><span data-stu-id="aff00-174">Name of the blob.</span></span> <span data-ttu-id="aff00-175">fileName é opcional e diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="aff00-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="aff00-176">Caso você especifique um nome de arquivo, a atividade (incluindo Cópia) funcionará no Blob específico.</span><span class="sxs-lookup"><span data-stu-id="aff00-176">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="aff00-177">Quando fileName não for especificado, a Cópia incluirá todos os Blobs do folderPath para o conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="aff00-177">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="aff00-178">Quando **fileName** não for especificado para um conjunto de dados de saída e **preserveHierarchy** não for especificado em um coletor de atividade, o nome do arquivo gerado estaria no seguinte formato: Data.<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="aff00-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="aff00-179">Não</span><span class="sxs-lookup"><span data-stu-id="aff00-179">No</span></span> |
| <span data-ttu-id="aff00-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="aff00-180">partitionedBy</span></span> |<span data-ttu-id="aff00-181">partitionedBy é uma propriedade opcional.</span><span class="sxs-lookup"><span data-stu-id="aff00-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="aff00-182">Você pode usá-lo para especificar um folderPath dinâmico e o nome de arquivo para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="aff00-182">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="aff00-183">Por exemplo, folderPath pode ser parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="aff00-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="aff00-184">Confira a seção [Usando a propriedade partitionedBy](#using-partitionedBy-property) para obter detalhes e exemplos.</span><span class="sxs-lookup"><span data-stu-id="aff00-184">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="aff00-185">Não</span><span class="sxs-lookup"><span data-stu-id="aff00-185">No</span></span> |
| <span data-ttu-id="aff00-186">formato</span><span class="sxs-lookup"><span data-stu-id="aff00-186">format</span></span> | <span data-ttu-id="aff00-187">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="aff00-187">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="aff00-188">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="aff00-188">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="aff00-189">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="aff00-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="aff00-190">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="aff00-190">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="aff00-191">Não</span><span class="sxs-lookup"><span data-stu-id="aff00-191">No</span></span> |
| <span data-ttu-id="aff00-192">compactação</span><span class="sxs-lookup"><span data-stu-id="aff00-192">compression</span></span> | <span data-ttu-id="aff00-193">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="aff00-193">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="aff00-194">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="aff00-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="aff00-195">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="aff00-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="aff00-196">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="aff00-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="aff00-197">Não</span><span class="sxs-lookup"><span data-stu-id="aff00-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="aff00-198">Usando a propriedade partitionedBy</span><span class="sxs-lookup"><span data-stu-id="aff00-198">Using partitionedBy property</span></span>
<span data-ttu-id="aff00-199">Conforme mencionado na seção anterior, você pode especificar um nome de arquivo e um folderPath dinâmico para dados de série temporal com a propriedade **partitionedBy**, [funções do Data Factory e as variáveis do sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="aff00-199">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="aff00-200">Para saber mais sobre conjuntos de dados de série temporal, agendamento e fatias, veja os artigos [Criando conjuntos de dados](data-factory-create-datasets.md) e [Agendamento e execução](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="aff00-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="aff00-201">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="aff00-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="aff00-202">Nesse exemplo, {Slice} é substituído pelo valor da variável de sistema SliceStart do Data Factory no formato (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="aff00-202">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="aff00-203">O SliceStart refere-se à hora de início da fatia.</span><span class="sxs-lookup"><span data-stu-id="aff00-203">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="aff00-204">O folderPath é diferente para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="aff00-204">The folderPath is different for each slice.</span></span> <span data-ttu-id="aff00-205">Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="aff00-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="aff00-206">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="aff00-206">Sample 2</span></span>

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

<span data-ttu-id="aff00-207">Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em variáveis separadas que são usadas pelas propriedades folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="aff00-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="aff00-208">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="aff00-208">Copy activity properties</span></span>
<span data-ttu-id="aff00-209">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="aff00-209">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="aff00-210">As propriedades, como nome, descrição, conjuntos de dados de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="aff00-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="aff00-211">Por outro lado, as propriedades disponíveis na seção **typeProperties** da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="aff00-211">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="aff00-212">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="aff00-212">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="aff00-213">Se você estiver movendo dados de um armazenamento de Blobs do Azure, defina o tipo de origem na atividade de cópia como **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="aff00-213">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="aff00-214">Da mesma forma, se você estiver movendo dados para um armazenamento de Blobs do Azure, defina o tipo de coletor na atividade de cópia como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="aff00-214">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="aff00-215">Esta seção fornece uma lista das propriedades compatíveis com BlobSource e BlobSink.</span><span class="sxs-lookup"><span data-stu-id="aff00-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="aff00-216">O **BlobSource** dá suporte às seguintes propriedades na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="aff00-216">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="aff00-217">Propriedade</span><span class="sxs-lookup"><span data-stu-id="aff00-217">Property</span></span> | <span data-ttu-id="aff00-218">Descrição</span><span class="sxs-lookup"><span data-stu-id="aff00-218">Description</span></span> | <span data-ttu-id="aff00-219">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="aff00-219">Allowed values</span></span> | <span data-ttu-id="aff00-220">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="aff00-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="aff00-221">recursiva</span><span class="sxs-lookup"><span data-stu-id="aff00-221">recursive</span></span> |<span data-ttu-id="aff00-222">Indica se os dados são lidos recursivamente por meio de subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="aff00-222">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="aff00-223">True (valor padrão), False</span><span class="sxs-lookup"><span data-stu-id="aff00-223">True (default value), False</span></span> |<span data-ttu-id="aff00-224">Não</span><span class="sxs-lookup"><span data-stu-id="aff00-224">No</span></span> |

<span data-ttu-id="aff00-225">O **BlobSink** dá suporte às seguintes propriedades na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="aff00-225">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="aff00-226">Propriedade</span><span class="sxs-lookup"><span data-stu-id="aff00-226">Property</span></span> | <span data-ttu-id="aff00-227">Descrição</span><span class="sxs-lookup"><span data-stu-id="aff00-227">Description</span></span> | <span data-ttu-id="aff00-228">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="aff00-228">Allowed values</span></span> | <span data-ttu-id="aff00-229">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="aff00-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="aff00-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="aff00-230">copyBehavior</span></span> |<span data-ttu-id="aff00-231">Define o comportamento de cópia quando a origem é BlobSource ou FileSystem.</span><span class="sxs-lookup"><span data-stu-id="aff00-231">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="aff00-232"><b>PreserveHierarchy:</b> preserva a hierarquia de arquivos na pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="aff00-232"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="aff00-233">O caminho relativo do arquivo de origem para a pasta de origem é idêntico ao caminho relativo do arquivo de destino para a pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="aff00-233">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="aff00-234"><b>FlattenHierarchy:</b> todos os arquivos da pasta de origem estão no primeiro nível da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="aff00-234"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="aff00-235">Os arquivos de destino têm o nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aff00-235">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="aff00-236"><b>MergeFiles:</b> mescla todos os arquivos da pasta de origem em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="aff00-236"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="aff00-237">Se o nome do arquivo/blob for especificado, o nome do arquivo mesclado será o nome especificado; caso contrário, será o nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aff00-237">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="aff00-238">Não</span><span class="sxs-lookup"><span data-stu-id="aff00-238">No</span></span> |

<span data-ttu-id="aff00-239">**BlobSource** também oferece suporte a essas duas propriedades para compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="aff00-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="aff00-240">**treatEmptyAsNull**: especifica se deve-se tratar a cadeia de caracteres nula ou vazia como valor nulo.</span><span class="sxs-lookup"><span data-stu-id="aff00-240">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="aff00-241">**skipHeaderLineCount** - Especifica quantas linhas precisam ser ignoradas.</span><span class="sxs-lookup"><span data-stu-id="aff00-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="aff00-242">É aplicável somente quando o conjunto de dados de entrada usa TextFormat.</span><span class="sxs-lookup"><span data-stu-id="aff00-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="aff00-243">Da mesma forma, **BlobSink** oferece suporte à seguinte propriedade para compatibilidade com versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="aff00-243">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="aff00-244">**blobWriterAddHeader**: especifica se deve adicionar um cabeçalho de definições de coluna ao gravar em um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="aff00-244">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="aff00-245">Agora, os conjuntos de dados dão suporte às seguintes propriedades que implementam a mesma funcionalidade: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="aff00-245">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="aff00-246">A tabela a seguir fornece orientação sobre como usar as novas propriedades do conjunto de dados em vez de propriedades de fonte/coletor de blob.</span><span class="sxs-lookup"><span data-stu-id="aff00-246">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="aff00-247">Propriedade de Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="aff00-247">Copy Activity property</span></span> | <span data-ttu-id="aff00-248">Propriedade de Conjunto de Dados</span><span class="sxs-lookup"><span data-stu-id="aff00-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="aff00-249">skipHeaderLineCount em BlobSource</span><span class="sxs-lookup"><span data-stu-id="aff00-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="aff00-250">skipLineCount e firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="aff00-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="aff00-251">As linhas são ignoradas primeiro e, em seguida, a primeira linha é lida como um cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="aff00-251">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="aff00-252">treatEmptyAsNull em BlobSource</span><span class="sxs-lookup"><span data-stu-id="aff00-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="aff00-253">treatEmptyAsNull no conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="aff00-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="aff00-254">blobWriterAddHeader em BlobSink</span><span class="sxs-lookup"><span data-stu-id="aff00-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="aff00-255">firstRowAsHeader no conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="aff00-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="aff00-256">Confira a seção [Especificar TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) para obter informações detalhadas sobre essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="aff00-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="aff00-257">exemplos de recursive e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="aff00-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="aff00-258">Esta seção descreve o comportamento resultante da operação de cópia para diferentes combinações de valores recursive e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="aff00-258">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="aff00-259">recursiva</span><span class="sxs-lookup"><span data-stu-id="aff00-259">recursive</span></span> | <span data-ttu-id="aff00-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="aff00-260">copyBehavior</span></span> | <span data-ttu-id="aff00-261">Comportamento resultante</span><span class="sxs-lookup"><span data-stu-id="aff00-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="aff00-262">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="aff00-262">true</span></span> |<span data-ttu-id="aff00-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="aff00-263">preserveHierarchy</span></span> |<span data-ttu-id="aff00-264">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="aff00-264">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="aff00-265">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-265">Folder1</span></span><br/><span data-ttu-id="aff00-266">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="aff00-267">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="aff00-268">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="aff00-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="aff00-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="aff00-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="aff00-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="aff00-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="aff00-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="aff00-272">a pasta de destino Pasta1 é criada com a mesma estrutura da origem</span><span class="sxs-lookup"><span data-stu-id="aff00-272">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="aff00-273">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-273">Folder1</span></span><br/><span data-ttu-id="aff00-274">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="aff00-275">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="aff00-276">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="aff00-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="aff00-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="aff00-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="aff00-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="aff00-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5.</span><span class="sxs-lookup"><span data-stu-id="aff00-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="aff00-280">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="aff00-280">true</span></span> |<span data-ttu-id="aff00-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="aff00-281">flattenHierarchy</span></span> |<span data-ttu-id="aff00-282">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="aff00-282">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="aff00-283">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-283">Folder1</span></span><br/><span data-ttu-id="aff00-284">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="aff00-285">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="aff00-286">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="aff00-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="aff00-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="aff00-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="aff00-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="aff00-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="aff00-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="aff00-290">a Pasta1 de destino é criada com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="aff00-290">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="aff00-291">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-291">Folder1</span></span><br/><span data-ttu-id="aff00-292">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="aff00-293">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="aff00-294">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo3</span><span class="sxs-lookup"><span data-stu-id="aff00-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="aff00-295">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo4</span><span class="sxs-lookup"><span data-stu-id="aff00-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="aff00-296">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo5</span><span class="sxs-lookup"><span data-stu-id="aff00-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="aff00-297">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="aff00-297">true</span></span> |<span data-ttu-id="aff00-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="aff00-298">mergeFiles</span></span> |<span data-ttu-id="aff00-299">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="aff00-299">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="aff00-300">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-300">Folder1</span></span><br/><span data-ttu-id="aff00-301">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="aff00-302">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="aff00-303">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="aff00-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="aff00-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="aff00-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="aff00-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="aff00-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="aff00-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="aff00-307">a Pasta1 de destino é criada com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="aff00-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="aff00-308">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-308">Folder1</span></span><br/><span data-ttu-id="aff00-309">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 + Arquivo3 + Arquivo4 + Arquivo5 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente</span><span class="sxs-lookup"><span data-stu-id="aff00-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="aff00-310">false</span><span class="sxs-lookup"><span data-stu-id="aff00-310">false</span></span> |<span data-ttu-id="aff00-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="aff00-311">preserveHierarchy</span></span> |<span data-ttu-id="aff00-312">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="aff00-312">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="aff00-313">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-313">Folder1</span></span><br/><span data-ttu-id="aff00-314">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="aff00-315">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="aff00-316">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="aff00-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="aff00-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="aff00-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="aff00-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="aff00-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="aff00-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="aff00-320">a pasta de destino Pasta1 é criada com a seguinte estrutura</span><span class="sxs-lookup"><span data-stu-id="aff00-320">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="aff00-321">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-321">Folder1</span></span><br/><span data-ttu-id="aff00-322">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="aff00-323">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="aff00-324">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="aff00-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="aff00-325">false</span><span class="sxs-lookup"><span data-stu-id="aff00-325">false</span></span> |<span data-ttu-id="aff00-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="aff00-326">flattenHierarchy</span></span> |<span data-ttu-id="aff00-327">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="aff00-327">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="aff00-328">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-328">Folder1</span></span><br/><span data-ttu-id="aff00-329">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="aff00-330">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="aff00-331">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="aff00-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="aff00-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="aff00-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="aff00-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="aff00-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="aff00-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="aff00-335">a pasta de destino Pasta1 é criada com a seguinte estrutura</span><span class="sxs-lookup"><span data-stu-id="aff00-335">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="aff00-336">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-336">Folder1</span></span><br/><span data-ttu-id="aff00-337">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="aff00-338">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="aff00-339">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="aff00-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="aff00-340">false</span><span class="sxs-lookup"><span data-stu-id="aff00-340">false</span></span> |<span data-ttu-id="aff00-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="aff00-341">mergeFiles</span></span> |<span data-ttu-id="aff00-342">Para uma pasta de origem Pasta1 com a seguinte estrutura: </span><span class="sxs-lookup"><span data-stu-id="aff00-342">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="aff00-343">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-343">Folder1</span></span><br/><span data-ttu-id="aff00-344">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="aff00-345">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="aff00-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="aff00-346">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="aff00-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="aff00-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="aff00-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="aff00-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="aff00-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="aff00-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="aff00-350">a pasta de destino Pasta1 é criada com a seguinte estrutura</span><span class="sxs-lookup"><span data-stu-id="aff00-350">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="aff00-351">Pasta1</span><span class="sxs-lookup"><span data-stu-id="aff00-351">Folder1</span></span><br/><span data-ttu-id="aff00-352">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos dos Arquivo1 + Arquivo2 são mesclados em um único arquivo com um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aff00-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="aff00-353">Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="aff00-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="aff00-354">Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não são selecionados.</span><span class="sxs-lookup"><span data-stu-id="aff00-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage"></a><span data-ttu-id="aff00-355">Passo a passo: Usar o Assistente de Cópia para copiar dados do e para o Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="aff00-355">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span></span>
<span data-ttu-id="aff00-356">Vamos examinar como copiar dados rapidamente de e para um armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-356">Let's look at how to quickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="aff00-357">Neste passo a passo, os armazenamentos de dados de origem e de destino do tipo: Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="aff00-358">O pipeline neste passo a passo copia os dados de uma pasta para outra no mesmo contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="aff00-358">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span></span> <span data-ttu-id="aff00-359">Este passo a passo é intencionalmente simples para mostrar configurações ou propriedades ao usar o Armazenamento de Blobs como uma fonte ou um coletor.</span><span class="sxs-lookup"><span data-stu-id="aff00-359">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="aff00-360">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aff00-360">Prerequisites</span></span>
1. <span data-ttu-id="aff00-361">Crie uma **Conta de Armazenamento do Azure** de uso geral caso não tenha uma.</span><span class="sxs-lookup"><span data-stu-id="aff00-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="aff00-362">Neste passo a passo, o armazenamento de blobs é usado como um armazenamento de dados de **origem** e de **destino**.</span><span class="sxs-lookup"><span data-stu-id="aff00-362">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="aff00-363">Se você não tiver uma conta de armazenamento do Azure, veja o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) para conhecer as etapas para criar um.</span><span class="sxs-lookup"><span data-stu-id="aff00-363">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
2. <span data-ttu-id="aff00-364">Crie um contêiner de blobs chamado **adfblobconnector** na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="aff00-364">Create a blob container named **adfblobconnector** in the storage account.</span></span> 
4. <span data-ttu-id="aff00-365">Crie uma pasta chamada **input** no contêiner **adfblobconnector**.</span><span class="sxs-lookup"><span data-stu-id="aff00-365">Create a folder named **input** in the **adfblobconnector** container.</span></span>
5. <span data-ttu-id="aff00-366">Crie um arquivo chamado **emp.txt** com o seguinte conteúdo e carregue-o para a pasta **input** usando ferramentas como o [Gerenciador de Armazenamento do Azure](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="aff00-366">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-the-data-factory"></a><span data-ttu-id="aff00-367">Criar o data factory</span><span class="sxs-lookup"><span data-stu-id="aff00-367">Create the data factory</span></span>
1. <span data-ttu-id="aff00-368">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aff00-368">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="aff00-369">Clique em **+NOVO** no canto superior esquerdo, clique em **Inteligência + análise** e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="aff00-369">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="aff00-370">Na folha **Nova data factory** :</span><span class="sxs-lookup"><span data-stu-id="aff00-370">In the **New data factory** blade:</span></span>   
    1. <span data-ttu-id="aff00-371">Insira **ADFBlobConnectorDF** para o **nome**.</span><span class="sxs-lookup"><span data-stu-id="aff00-371">Enter **ADFBlobConnectorDF** for the **name**.</span></span> <span data-ttu-id="aff00-372">O nome da data factory do Azure deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="aff00-372">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="aff00-373">Se você receber o erro `*Data factory name “ADFBlobConnectorDF” is not available`, altere o nome do data factory (por exemplo, yournameADFBlobConnectorDF) e tente criá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="aff00-373">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="aff00-374">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="aff00-375">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="aff00-376">Para Grupo de Recursos, selecione **Usar existente** para selecionar um grupo de recursos existente (ou) selecione **Criar novo** para inserir um nome para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="aff00-376">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span></span>
    4. <span data-ttu-id="aff00-377">Selecione um **local** para o data factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-377">Select a **location** for the data factory.</span></span>
    5. <span data-ttu-id="aff00-378">Marque a caixa de seleção **Fixar no painel** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="aff00-378">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>
    6. <span data-ttu-id="aff00-379">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aff00-379">Click **Create**.</span></span>
3. <span data-ttu-id="aff00-380">Depois que a criação for concluída, você verá a folha **Data Factory**, conforme mostrado na seguinte imagem: ![Home page do data factory](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-380">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="aff00-381">Assistente de Cópia</span><span class="sxs-lookup"><span data-stu-id="aff00-381">Copy Wizard</span></span>
1. <span data-ttu-id="aff00-382">Na home page do Data Factory, clique no bloco **Copiar dados [VISUALIZAÇÃO]** para iniciar o **Assistente de Cópia de Dados** em uma guia separada.</span><span class="sxs-lookup"><span data-stu-id="aff00-382">On the Data Factory home page, click the **Copy data [PREVIEW]** tile to launch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="aff00-383">Se você vir que o navegador da Web está bloqueado em "Autorizando...", desabilite/desmarque a configuração **Bloquear cookies de terceiros e dados de site** (ou) mantenha-a habilitada, crie uma exceção para **login.microsoftonline.com** e tente iniciar o assistente novamente.</span><span class="sxs-lookup"><span data-stu-id="aff00-383">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="aff00-384">Na página **Propriedades** :</span><span class="sxs-lookup"><span data-stu-id="aff00-384">In the **Properties** page:</span></span>
    1. <span data-ttu-id="aff00-385">Insira **CopyPipeline** para **Nome da tarefa**.</span><span class="sxs-lookup"><span data-stu-id="aff00-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="aff00-386">O nome da tarefa é o nome do pipeline no data factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-386">The task name is the name of the pipeline in your data factory.</span></span>
    2. <span data-ttu-id="aff00-387">Insira uma **descrição** para a tarefa (opcional).</span><span class="sxs-lookup"><span data-stu-id="aff00-387">Enter a **description** for the task (optional).</span></span>
    3. <span data-ttu-id="aff00-388">Para **Cadência de tarefa ou Agendamento de tarefa**, mantenha a opção **Executar regularmente de acordo com o agendamento**.</span><span class="sxs-lookup"><span data-stu-id="aff00-388">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span></span> <span data-ttu-id="aff00-389">Se você desejar executar essa tarefa somente uma vez, em vez de executá-la repetidamente de acordo com um agendamento, selecione **Executar uma vez agora**.</span><span class="sxs-lookup"><span data-stu-id="aff00-389">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="aff00-390">Se você selecionar a opção **Executar uma vez agora**, um [pipeline avulso](data-factory-create-pipelines.md#onetime-pipeline) será criado.</span><span class="sxs-lookup"><span data-stu-id="aff00-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="aff00-391">Mantenha as configurações de **Padrão recorrente**.</span><span class="sxs-lookup"><span data-stu-id="aff00-391">Keep the settings for **Recurring pattern**.</span></span> <span data-ttu-id="aff00-392">Essa tarefa é executada diariamente entre as horas de início e término especificadas na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="aff00-392">This task runs daily between the start and end times you specify in the next step.</span></span>
    5. <span data-ttu-id="aff00-393">Altere a **Data/hora de início** para **21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="aff00-393">Change the **Start date time** to **04/21/2017**.</span></span> 
    6. <span data-ttu-id="aff00-394">Altere a **Data/hora de término** para **25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="aff00-394">Change the **End date time** to **04/25/2017**.</span></span> <span data-ttu-id="aff00-395">Talvez você queira digitar a data em vez de procurá-la no calendário.</span><span class="sxs-lookup"><span data-stu-id="aff00-395">You may want to type the date instead of browsing through the calendar.</span></span>     
    8. <span data-ttu-id="aff00-396">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="aff00-396">Click **Next**.</span></span>
      <span data-ttu-id="aff00-397">![Ferramenta de Cópia – Página Propriedades](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="aff00-398">Na página **Repositório de dados de origem**, clique no bloco **Armazenamento de Blobs do Azure**.</span><span class="sxs-lookup"><span data-stu-id="aff00-398">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="aff00-399">Use essa página para especificar o repositório de dados de origem para a tarefa de cópia.</span><span class="sxs-lookup"><span data-stu-id="aff00-399">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="aff00-400">Você pode usar um serviço de repositório de dados vinculado existente ou especificar um novo repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="aff00-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="aff00-401">Para usar um serviço vinculado existente, selecione **DE SERVIÇOS VINCULADOS EXISTENTES** e selecione o serviço vinculado correto.</span><span class="sxs-lookup"><span data-stu-id="aff00-401">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
    <span data-ttu-id="aff00-402">![Ferramenta de Cópia – Página do armazenamento de dados de origem](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="aff00-403">Na página **Especificar a conta de armazenamento de Blobs do Azure** :</span><span class="sxs-lookup"><span data-stu-id="aff00-403">On the **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="aff00-404">Mantenha o nome gerado automaticamente para o **Nome da conexão**.</span><span class="sxs-lookup"><span data-stu-id="aff00-404">Keep the auto-generated name for **Connection name**.</span></span> <span data-ttu-id="aff00-405">O nome da conexão é o nome do serviço vinculado do tipo: Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-405">The connection name is the name of the linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="aff00-406">Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de conta**.</span><span class="sxs-lookup"><span data-stu-id="aff00-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="aff00-407">Selecione sua assinatura do Azure ou mantenha **Selecionar tudo** para **Assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="aff00-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="aff00-408">Selecione uma **Conta de armazenamento do Azure** na lista de contas de armazenamento do Azure disponíveis na assinatura selecionada.</span><span class="sxs-lookup"><span data-stu-id="aff00-408">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="aff00-409">Você também pode optar por inserir as configurações da conta de armazenamento manualmente selecionando a opção **Inserir manualmente** para o **Método de seleção de conta**.</span><span class="sxs-lookup"><span data-stu-id="aff00-409">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span></span>
   5. <span data-ttu-id="aff00-410">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="aff00-410">Click **Next**.</span></span> 
      <span data-ttu-id="aff00-411">![Ferramenta de Cópia – Especificar a conta do armazenamento de Blobs do Azure](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-411">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="aff00-412">Na página **Escolher o arquivo de entrada ou a pasta** :</span><span class="sxs-lookup"><span data-stu-id="aff00-412">On **Choose the input file or folder** page:</span></span>
   1. <span data-ttu-id="aff00-413">Clique duas vezes em **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="aff00-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="aff00-414">Selecione **input** e clique em **Escolher**.</span><span class="sxs-lookup"><span data-stu-id="aff00-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="aff00-415">Neste passo a passo, você seleciona a pasta input.</span><span class="sxs-lookup"><span data-stu-id="aff00-415">In this walkthrough, you select the input folder.</span></span> <span data-ttu-id="aff00-416">Você também pode selecionar o arquivo emp.txt na pasta.</span><span class="sxs-lookup"><span data-stu-id="aff00-416">You could also select the emp.txt file in the folder instead.</span></span> 
      <span data-ttu-id="aff00-417">![Ferramenta de Cópia – Escolher a pasta ou o arquivo de entrada](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-417">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="aff00-418">Na página **Escolher o arquivo ou a pasta de entrada**:</span><span class="sxs-lookup"><span data-stu-id="aff00-418">On the **Choose the input file or folder** page:</span></span>
    1. <span data-ttu-id="aff00-419">Confirme se **a pasta ou o arquivo** está definido como **adfblobconnector/input**.</span><span class="sxs-lookup"><span data-stu-id="aff00-419">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span></span> <span data-ttu-id="aff00-420">Se os arquivos estiverem em subpastas, por exemplo, 01/04/2017, 02/04/2017 e assim por diante, insira adfblobconnector/input/{year}/{month}/{day} para o arquivo ou a pasta.</span><span class="sxs-lookup"><span data-stu-id="aff00-420">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="aff00-421">Ao pressionar TAB fora da caixa de texto, você verá três listas suspensas para selecionar formatos de ano (yyyy), mês (MM) e dia (dd).</span><span class="sxs-lookup"><span data-stu-id="aff00-421">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="aff00-422">Não defina a opção **Copiar arquivo recursivamente**.</span><span class="sxs-lookup"><span data-stu-id="aff00-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="aff00-423">Selecione essa opção para percorrer as pastas recursivamente para que os arquivos sejam copiados para o destino.</span><span class="sxs-lookup"><span data-stu-id="aff00-423">Select this option to recursively traverse through folders for files to be copied to the destination.</span></span> 
    3. <span data-ttu-id="aff00-424">Não defina a opção **Cópia binária**.</span><span class="sxs-lookup"><span data-stu-id="aff00-424">Do not the **binary copy** option.</span></span> <span data-ttu-id="aff00-425">Selecione essa opção para executar uma cópia binária do arquivo de origem para o destino.</span><span class="sxs-lookup"><span data-stu-id="aff00-425">Select this option to perform a binary copy of source file to the destination.</span></span> <span data-ttu-id="aff00-426">Não selecione essa opção neste passo a passo, de forma que você possa ver mais opções na próxima página.</span><span class="sxs-lookup"><span data-stu-id="aff00-426">Do not select for this walkthrough so that you can see more options in the next pages.</span></span> 
    4. <span data-ttu-id="aff00-427">Confirme se o **Tipo de compactação** está definido como **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="aff00-427">Confirm that the **Compression type** is set to **None**.</span></span> <span data-ttu-id="aff00-428">Selecione um valor para essa opção se os arquivos de origem estiverem compactados em um dos formatos com suporte.</span><span class="sxs-lookup"><span data-stu-id="aff00-428">Select a value for this option if your source files are compressed in one of the supported formats.</span></span> 
    5. <span data-ttu-id="aff00-429">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="aff00-429">Click **Next**.</span></span>
    <span data-ttu-id="aff00-430">![Ferramenta de Cópia – Escolher a pasta ou o arquivo de entrada](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-430">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="aff00-431">Na página **Configurações de formato de arquivo**, você vê os delimitadores e o esquema é detectado automaticamente pelo assistente na análise do arquivo.</span><span class="sxs-lookup"><span data-stu-id="aff00-431">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> 
    1. <span data-ttu-id="aff00-432">Considere as seguintes opções: a.</span><span class="sxs-lookup"><span data-stu-id="aff00-432">Confirm the following options: a.</span></span> <span data-ttu-id="aff00-433">O **formato de arquivo** está definido como **Formato de texto**.</span><span class="sxs-lookup"><span data-stu-id="aff00-433">The **file format** is set to **Text format**.</span></span> <span data-ttu-id="aff00-434">É possível ver todos os formatos com suporte na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="aff00-434">You can see all the supported formats in the drop-down list.</span></span> <span data-ttu-id="aff00-435">Por exemplo: JSON, Avro, ORC, Parquet.</span><span class="sxs-lookup"><span data-stu-id="aff00-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="aff00-436">b.</span><span class="sxs-lookup"><span data-stu-id="aff00-436">b.</span></span> <span data-ttu-id="aff00-437">O **delimitador de coluna** está definido como `Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="aff00-437">The **column delimiter** is set to `Comma (,)`.</span></span> <span data-ttu-id="aff00-438">É possível ver os outros delimitadores de coluna com suporte no Data Factory na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="aff00-438">You can see the other column delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="aff00-439">Você também pode especificar um delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="aff00-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="aff00-440">c.</span><span class="sxs-lookup"><span data-stu-id="aff00-440">c.</span></span> <span data-ttu-id="aff00-441">O **delimitador de coluna** está definido como `Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="aff00-441">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="aff00-442">É possível ver os outros delimitadores de linha com suporte no Data Factory na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="aff00-442">You can see the other row delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="aff00-443">Você também pode especificar um delimitador personalizado.</span><span class="sxs-lookup"><span data-stu-id="aff00-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="aff00-444">d.</span><span class="sxs-lookup"><span data-stu-id="aff00-444">d.</span></span> <span data-ttu-id="aff00-445">A opção **ignorar contagem de linhas** está definida como **0**.</span><span class="sxs-lookup"><span data-stu-id="aff00-445">The **skip line count** is set to **0**.</span></span> <span data-ttu-id="aff00-446">Se você desejar que algumas linhas sejam ignoradas na parte superior do arquivo, insira o número aqui.</span><span class="sxs-lookup"><span data-stu-id="aff00-446">If you want a few lines to be skipped at the top of the file, enter the number here.</span></span>
        <span data-ttu-id="aff00-447">e.</span><span class="sxs-lookup"><span data-stu-id="aff00-447">e.</span></span>  <span data-ttu-id="aff00-448">A opção **primeira linha de dados contém nomes de coluna** não está definida.</span><span class="sxs-lookup"><span data-stu-id="aff00-448">The **first data row contains column names** is not set.</span></span> <span data-ttu-id="aff00-449">Se os arquivos de origem contiverem nomes de coluna na primeira linha, selecione essa opção.</span><span class="sxs-lookup"><span data-stu-id="aff00-449">If the source files contain column names in the first row, select this option.</span></span>
        <span data-ttu-id="aff00-450">f.</span><span class="sxs-lookup"><span data-stu-id="aff00-450">f.</span></span> <span data-ttu-id="aff00-451">A opção **tratar o valor da coluna vazia como nulo** está definida.</span><span class="sxs-lookup"><span data-stu-id="aff00-451">The **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="aff00-452">Expanda **Configurações avançadas** para ver a opção avançada disponível.</span><span class="sxs-lookup"><span data-stu-id="aff00-452">Expand **Advanced settings** to see advanced option available.</span></span>
    3. <span data-ttu-id="aff00-453">Na parte inferior da página, consulte a **visualização** de dados do arquivo emp.txt.</span><span class="sxs-lookup"><span data-stu-id="aff00-453">At the bottom of the page, see the **preview** of data from the emp.txt file.</span></span>
    4. <span data-ttu-id="aff00-454">Clique na guia **ESQUEMA** na parte inferior para ver o esquema inferido pelo assistente de cópia observando os dados no arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="aff00-454">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span></span>
    5. <span data-ttu-id="aff00-455">Clique em **Avançar** depois de revisar os delimitadores e visualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="aff00-455">Click **Next** after you review the delimiters and preview data.</span></span>
    <span data-ttu-id="aff00-456">![Ferramenta de Cópia – Configurações de formato de arquivo](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="aff00-457">Na **página Armazenamento de dados de destino**, selecione **Armazenamento de Blobs do Azure** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="aff00-457">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="aff00-458">Você está usando o Armazenamento de Blobs do Azure como os armazenamentos de dados de origem e de destino neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="aff00-458">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="aff00-459">![Ferramenta de Cópia – selecionar o armazenamento de dados de destino](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="aff00-460">Na página **Especificar a conta de armazenamento de Blobs do Azure**:</span><span class="sxs-lookup"><span data-stu-id="aff00-460">On **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="aff00-461">Insira **AzureStorageLinkedService** no campo **Nome da conexão**.</span><span class="sxs-lookup"><span data-stu-id="aff00-461">Enter **AzureStorageLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="aff00-462">Confirme se a opção **De assinaturas do Azure** foi selecionada em **Método de seleção de conta**.</span><span class="sxs-lookup"><span data-stu-id="aff00-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="aff00-463">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="aff00-464">Selecione sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="aff00-465">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="aff00-465">Click **Next**.</span></span>     
10. <span data-ttu-id="aff00-466">Na página **Escolher o arquivo ou a pasta de saída**:</span><span class="sxs-lookup"><span data-stu-id="aff00-466">On the **Choose the output file or folder** page:</span></span> 
    6. <span data-ttu-id="aff00-467">especifique **Caminho da pasta** como **adfblobconnector/output/{year}/{month}/{day}**.</span><span class="sxs-lookup"><span data-stu-id="aff00-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="aff00-468">Insira **GUIA**.</span><span class="sxs-lookup"><span data-stu-id="aff00-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="aff00-469">No **ano**, selecione **yyyy**.</span><span class="sxs-lookup"><span data-stu-id="aff00-469">For the **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="aff00-470">No **mês**, confirme se ele está definido como **MM**.</span><span class="sxs-lookup"><span data-stu-id="aff00-470">For the **month**, confirm that it is set to **MM**.</span></span>
    9. <span data-ttu-id="aff00-471">No **dia**, confirme se ele está definido como **dd**.</span><span class="sxs-lookup"><span data-stu-id="aff00-471">For the **day**, confirm that it is set to **dd**.</span></span>
    10. <span data-ttu-id="aff00-472">Confirme se o **tipo de compactação** está definido como **Nenhum**.</span><span class="sxs-lookup"><span data-stu-id="aff00-472">Confirm that the **compression type** is set to **None**.</span></span>
    11. <span data-ttu-id="aff00-473">Confirme se o **comportamento de cópia** está definido como **Mesclar arquivos**.</span><span class="sxs-lookup"><span data-stu-id="aff00-473">Confirm that the **copy behavior** is set to **Merge files**.</span></span> <span data-ttu-id="aff00-474">Se o arquivo de saída com o mesmo nome já existir, o novo conteúdo será adicionado ao mesmo arquivo no final.</span><span class="sxs-lookup"><span data-stu-id="aff00-474">If the output file with the same name already exists, the new content is added to the same file at the end.</span></span>
    12. <span data-ttu-id="aff00-475">Clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="aff00-475">Click **Next**.</span></span>
    <span data-ttu-id="aff00-476">![Ferramenta de Cópia – Escolher o arquivo ou a pasta de saída](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="aff00-477">Na página **Configurações de formato de arquivo**, examine as configurações e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="aff00-477">On the **File format settings** page, review the settings, and click **Next**.</span></span> <span data-ttu-id="aff00-478">Uma das opções adicionais aqui é adicionar um cabeçalho ao arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="aff00-478">One of the additional options here is to add a header to the output file.</span></span> <span data-ttu-id="aff00-479">Se você selecionar essa opção, uma linha de cabeçalho será adicionada com nomes das colunas do esquema da fonte.</span><span class="sxs-lookup"><span data-stu-id="aff00-479">If you select that option, a header row is added with names of the columns from the schema of the source.</span></span> <span data-ttu-id="aff00-480">Você pode renomear os nomes de coluna padrão ao exibir o esquema da fonte.</span><span class="sxs-lookup"><span data-stu-id="aff00-480">You can rename the default column names when viewing the schema for the source.</span></span> <span data-ttu-id="aff00-481">Por exemplo, você poderá alterar a primeira coluna para Nome e a segunda coluna para Sobrenome.</span><span class="sxs-lookup"><span data-stu-id="aff00-481">For example, you could change the first column to First Name and second column to Last Name.</span></span> <span data-ttu-id="aff00-482">Em seguida, o arquivo de saída será gerado com um cabeçalho com esses nomes como nomes de coluna.</span><span class="sxs-lookup"><span data-stu-id="aff00-482">Then, the output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="aff00-483">![Ferramenta de Cópia – Configurações de formato de arquivo para o destino](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="aff00-484">Na página **Configurações de desempenho**, confirme se **unidades de nuvem** e **cópias paralelas** estão definidas como **Automático** e clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="aff00-484">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span></span> <span data-ttu-id="aff00-485">Para obter detalhes sobre essas configurações, consulte [Guia de desempenho e ajuste da atividade de cópia](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="aff00-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="aff00-486">![Ferramenta de Cópia – Configurações de desempenho](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="aff00-487">Na página **Resumo**, examine todas as configurações (propriedades da tarefa, configurações da origem e do destino e configurações de cópia) e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="aff00-487">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="aff00-488">![Ferramenta de Cópia – Página Resumo](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="aff00-489">Examine as informações na página **Resumo** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="aff00-489">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="aff00-490">Esse assistente cria dois serviços vinculados, dois conjuntos de dados (entrada e saída) e um pipeline no data factory (de onde você iniciou o Assistente de Cópia).</span><span class="sxs-lookup"><span data-stu-id="aff00-490">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span>
    <span data-ttu-id="aff00-491">![Ferramenta de Cópia – Página Implantação](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-the-pipeline-copy-task"></a><span data-ttu-id="aff00-492">Monitorar o pipeline (tarefa de cópia)</span><span class="sxs-lookup"><span data-stu-id="aff00-492">Monitor the pipeline (copy task)</span></span>

1. <span data-ttu-id="aff00-493">Clique no link `Click here to monitor copy pipeline` na página **Implantação**.</span><span class="sxs-lookup"><span data-stu-id="aff00-493">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span></span> 
2. <span data-ttu-id="aff00-494">Você deverá ver o **aplicativo Monitorar e Gerenciar** em uma guia separada.  ![Aplicativo Monitorar e Gerenciar](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="aff00-494">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="aff00-495">Altere a hora de **início** na parte superior para `04/19/2017` e a hora de **término** para `04/27/2017` e, em seguida, clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="aff00-495">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="aff00-496">Você deverá ver cinco janelas de atividades na lista **JANELAS DE ATIVIDADES**.</span><span class="sxs-lookup"><span data-stu-id="aff00-496">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="aff00-497">As horas de **WindowStart** devem abranger todos os dias desde a hora de início até a hora de término do pipeline.</span><span class="sxs-lookup"><span data-stu-id="aff00-497">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span></span> 
5. <span data-ttu-id="aff00-498">Clique no botão **Atualizar** da lista **JANELAS DE ATIVIDADES** algumas vezes até ver que o status de todas as janelas de atividades está definido como Pronto.</span><span class="sxs-lookup"><span data-stu-id="aff00-498">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span></span> 
6. <span data-ttu-id="aff00-499">Agora, verifique se os arquivos de saída são gerados na pasta de saída do contêiner adfblobconnector.</span><span class="sxs-lookup"><span data-stu-id="aff00-499">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span></span> <span data-ttu-id="aff00-500">Você deverá ver a seguinte estrutura de pastas na pasta de saída:</span><span class="sxs-lookup"><span data-stu-id="aff00-500">You should see the following folder structure in the output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="aff00-501">Para obter informações detalhadas sobre como monitorar e gerenciar data factories, consulte o artigo [Monitorar e gerenciar o pipeline do Data Factory](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="aff00-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="aff00-502">Entidades de Data Factory</span><span class="sxs-lookup"><span data-stu-id="aff00-502">Data Factory entities</span></span>
<span data-ttu-id="aff00-503">Agora, volte para a guia com a home page do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-503">Now, switch back to the tab with the Data Factory home page.</span></span> <span data-ttu-id="aff00-504">Observe que agora há dois serviços vinculados, dois conjuntos de dados e um pipeline no data factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Home page do Data Factory com entidades](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="aff00-506">Clique em **Criar e implantar** para iniciar o Editor do Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-506">Click **Author and deploy** to launch Data Factory Editor.</span></span> 

![Editor Data Factory](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="aff00-508">Você deverá ver as seguintes entidades do Data Factory no data factory:</span><span class="sxs-lookup"><span data-stu-id="aff00-508">You should see the following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="aff00-509">Dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="aff00-509">Two linked services.</span></span> <span data-ttu-id="aff00-510">Um para a origem e o outro para o destino.</span><span class="sxs-lookup"><span data-stu-id="aff00-510">One for the source and the other one for the destination.</span></span> <span data-ttu-id="aff00-511">Ambos os serviços vinculados consultam a mesma conta de Armazenamento do Azure neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="aff00-511">Both the linked services refer to the same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="aff00-512">Dois conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="aff00-512">Two datasets.</span></span> <span data-ttu-id="aff00-513">Um conjunto de dados de entrada e um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="aff00-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="aff00-514">Neste passo a passo, ambos usam o mesmo contêiner de blobs, mas consultam pastas diferentes (entrada e saída).</span><span class="sxs-lookup"><span data-stu-id="aff00-514">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span></span>
 - <span data-ttu-id="aff00-515">Um pipeline.</span><span class="sxs-lookup"><span data-stu-id="aff00-515">A pipeline.</span></span> <span data-ttu-id="aff00-516">O pipeline contém uma atividade de cópia que usa uma fonte de blob e um coletor de blob para copiar dados de uma localização de blob do Azure para outra.</span><span class="sxs-lookup"><span data-stu-id="aff00-516">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span></span> 

<span data-ttu-id="aff00-517">As próximas seções fornecem mais informações sobre essas entidades.</span><span class="sxs-lookup"><span data-stu-id="aff00-517">The following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="aff00-518">Serviços vinculados</span><span class="sxs-lookup"><span data-stu-id="aff00-518">Linked services</span></span>
<span data-ttu-id="aff00-519">Você deverá ver dois serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="aff00-519">You should see two linked services.</span></span> <span data-ttu-id="aff00-520">Um para a origem e o outro para o destino.</span><span class="sxs-lookup"><span data-stu-id="aff00-520">One for the source and the other one for the destination.</span></span> <span data-ttu-id="aff00-521">Neste passo a passo, ambas as definições têm a mesma aparência, exceto os nomes.</span><span class="sxs-lookup"><span data-stu-id="aff00-521">In this walkthrough, both definitions look the same except for the names.</span></span> <span data-ttu-id="aff00-522">O **tipo** do serviço vinculado está definido como **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="aff00-522">The **type** of the linked service is set to **AzureStorage**.</span></span> <span data-ttu-id="aff00-523">A propriedade mais importante da definição de serviço vinculado é a **connectionString**, que é usada pelo Data Factory para se conectar à sua conta de Armazenamento do Azure em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="aff00-523">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span></span> <span data-ttu-id="aff00-524">Ignore a propriedade hubName na definição.</span><span class="sxs-lookup"><span data-stu-id="aff00-524">Ignore the hubName property in the definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="aff00-525">Serviço vinculado do armazenamento de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="aff00-525">Source blob storage linked service</span></span>
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

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="aff00-526">Serviço vinculado do armazenamento de blobs de destino</span><span class="sxs-lookup"><span data-stu-id="aff00-526">Destination blob storage linked service</span></span>

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

<span data-ttu-id="aff00-527">Para obter mais informações sobre o serviço vinculado do Armazenamento do Azure, consulte a seção [Propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="aff00-528">Conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="aff00-528">Datasets</span></span>
<span data-ttu-id="aff00-529">Há dois conjuntos de dados: um conjunto de dados de entrada e um conjunto de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="aff00-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="aff00-530">O tipo do conjunto de dados está definido como **AzureBlob** para ambos.</span><span class="sxs-lookup"><span data-stu-id="aff00-530">The type of the dataset is set to **AzureBlob** for both.</span></span> 

<span data-ttu-id="aff00-531">O conjunto de dados de entrada aponta para a pasta **input** do contêiner de blobs **adfblobconnector**.</span><span class="sxs-lookup"><span data-stu-id="aff00-531">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span></span> <span data-ttu-id="aff00-532">A propriedade **external** está definida como **true** para este conjunto de dados, pois os dados não são gerados pelo pipeline com a atividade de cópia que usa esse conjunto de dados como entrada.</span><span class="sxs-lookup"><span data-stu-id="aff00-532">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="aff00-533">O conjunto de dados de saída aponta para a pasta **output** do mesmo contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="aff00-533">The output dataset points to the **output** folder of the same blob container.</span></span> <span data-ttu-id="aff00-534">O conjunto de dados de saída também usa o ano, mês e dia da variável de sistema **SliceStart** para avaliar dinamicamente o caminho do arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="aff00-534">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span></span> <span data-ttu-id="aff00-535">Para obter uma lista de funções e variáveis de sistema com suporte no Data Factory, consulte [Funções e variáveis de sistema do Data Factory](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="aff00-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="aff00-536">A propriedade **external** está definida como **false** (valor padrão), pois este conjunto de dados é gerado pelo pipeline.</span><span class="sxs-lookup"><span data-stu-id="aff00-536">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span></span> 

<span data-ttu-id="aff00-537">Para obter mais informações sobre as propriedades com suporte no conjunto de dados de Blobs do Azure, consulte a seção [Propriedades do conjunto de dados](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="aff00-538">Conjunto de dados de entrada</span><span class="sxs-lookup"><span data-stu-id="aff00-538">Input dataset</span></span>

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

##### <a name="output-dataset"></a><span data-ttu-id="aff00-539">Conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="aff00-539">Output dataset</span></span>

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

#### <a name="pipeline"></a><span data-ttu-id="aff00-540">Pipeline</span><span class="sxs-lookup"><span data-stu-id="aff00-540">Pipeline</span></span>
<span data-ttu-id="aff00-541">O pipeline tem apenas uma atividade.</span><span class="sxs-lookup"><span data-stu-id="aff00-541">The pipeline has just one activity.</span></span> <span data-ttu-id="aff00-542">O **tipo** da atividade está definido como **Cópia**.</span><span class="sxs-lookup"><span data-stu-id="aff00-542">The **type** of the activity is set to **Copy**.</span></span>  <span data-ttu-id="aff00-543">Nas propriedades de tipo da atividade, há duas seções, uma para a fonte e a outra para o coletor.</span><span class="sxs-lookup"><span data-stu-id="aff00-543">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span></span> <span data-ttu-id="aff00-544">O tipo de origem está definido como **BlobSource**, pois a atividade está copiando dados de um armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="aff00-544">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span></span> <span data-ttu-id="aff00-545">O tipo de coletor está definido como **BlobSink**, pois a atividade está copiando dados para um armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="aff00-545">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span></span> <span data-ttu-id="aff00-546">A atividade de cópia usa InputDataset-z4y como a entrada e OutputDataset-z4y como a saída.</span><span class="sxs-lookup"><span data-stu-id="aff00-546">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span></span> 

<span data-ttu-id="aff00-547">Para obter mais informações sobre as propriedades com suporte na BlobSource e no BlobSink, consulte a seção [Propriedades da atividade de cópia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

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

## <a name="json-examples-for-copying-data-to-and-from-blob-storage"></a><span data-ttu-id="aff00-548">Exemplos JSON para cópia de dados de e para o Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="aff00-548">JSON examples for copying data to and from Blob Storage</span></span>  
<span data-ttu-id="aff00-549">Os exemplos a seguir fornecem amostras de definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="aff00-549">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="aff00-550">Tais exemplos mostram como copiar dados de/para o Armazenamento de Blobs do Azure e o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-550">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="aff00-551">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-551">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="aff00-552">Exemplo de JSON: Copiar dados do Armazenamento de Blobs para o Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="aff00-552">JSON Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="aff00-553">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="aff00-553">The following sample shows:</span></span>

1. <span data-ttu-id="aff00-554">Um serviço vinculado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="aff00-555">Um serviço vinculado do tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="aff00-556">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="aff00-557">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="aff00-558">Um [pipeline](data-factory-create-pipelines.md) com Atividade de cópia que usa [BlobSource](#copy-activity-properties) e [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="aff00-559">O exemplo copia os dados de série temporal de um blob do Azure para uma tabela SQL do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="aff00-559">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="aff00-560">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="aff00-560">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="aff00-561">**Serviço vinculado do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="aff00-561">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="aff00-562">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="aff00-562">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="aff00-563">O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="aff00-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="aff00-564">Para o primeiro, você especifica a cadeia de conexão que inclui a chave de conta, e para o mais recente, você especifica o URI de SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="aff00-564">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="aff00-565">Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="aff00-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="aff00-566">**Conjunto de dados de entrada de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="aff00-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="aff00-567">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="aff00-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="aff00-568">O caminho de pasta e nome de arquivo para o blob são avaliados dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="aff00-568">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="aff00-569">O caminho da pasta usa parte da hora de início do dia, mês e ano e o nome de arquivo usa a parte da hora de início.</span><span class="sxs-lookup"><span data-stu-id="aff00-569">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="aff00-570">A configuração "external": "true" informa o Data Factory que a tabela é externa ao Data Factory e não é produzida por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-570">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="aff00-571">**Conjunto de dados de saída do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="aff00-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="aff00-572">Os dados de cópia do exemplo em uma tabela chamada "MyTable" em um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="aff00-572">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="aff00-573">Crie a tabela no banco de dados SQL Azure com o mesmo número de colunas que você espera que o arquivo CSV de Blob contenha.</span><span class="sxs-lookup"><span data-stu-id="aff00-573">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="aff00-574">Novas linhas são adicionadas à tabela a cada hora.</span><span class="sxs-lookup"><span data-stu-id="aff00-574">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="aff00-575">**Uma atividade de cópia em um pipeline com origem de Blob e coletor SQL:**</span><span class="sxs-lookup"><span data-stu-id="aff00-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="aff00-576">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="aff00-576">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="aff00-577">Na definição de JSON do pipeline, o tipo de **fonte** está definido como **BlobSource** e o tipo de **coletor** está definido como **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="aff00-577">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
### <a name="json-example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="aff00-578">Exemplo de JSON: Copiar dados do SQL do Azure para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="aff00-578">JSON Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="aff00-579">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="aff00-579">The following sample shows:</span></span>

1. <span data-ttu-id="aff00-580">Um serviço vinculado do tipo [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="aff00-581">Um serviço vinculado do tipo [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="aff00-582">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="aff00-583">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="aff00-584">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) e [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="aff00-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="aff00-585">O exemplo copia os dados de série temporal de uma tabela SQL do Azure para um blob do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="aff00-585">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="aff00-586">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="aff00-586">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="aff00-587">**Serviço vinculado do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="aff00-587">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="aff00-588">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="aff00-588">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="aff00-589">O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="aff00-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="aff00-590">Para o primeiro, você especifica a cadeia de conexão que inclui a chave de conta, e para o mais recente, você especifica o URI de SAS (Assinatura de Acesso Compartilhado).</span><span class="sxs-lookup"><span data-stu-id="aff00-590">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="aff00-591">Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="aff00-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="aff00-592">**Conjunto de dados de entrada do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="aff00-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="aff00-593">O exemplo supõe que você criou uma tabela "MyTable" no SQL Azure e que ela contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="aff00-593">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="aff00-594">Configurar "external": true informa ao serviço Data Factory que a tabela é externa ao Data Factory e não é produzida por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="aff00-594">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="aff00-595">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="aff00-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="aff00-596">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="aff00-596">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="aff00-597">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="aff00-597">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="aff00-598">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="aff00-598">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="aff00-599">**Uma atividade de cópia em um pipeline com origem SQL e coletor de Blob:**</span><span class="sxs-lookup"><span data-stu-id="aff00-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="aff00-600">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="aff00-600">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="aff00-601">Na definição de JSON do pipeline, o tipo de **fonte** está definido como **SqlSource** e o tipo de **coletor** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="aff00-601">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="aff00-602">A consulta SQL especificada para a propriedade **SqlReaderQuery** seleciona os dados na última hora a serem copiados.</span><span class="sxs-lookup"><span data-stu-id="aff00-602">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="aff00-603">Para mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de coletor, confira [Mapeando colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="aff00-603">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="aff00-604">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="aff00-604">Performance and Tuning</span></span>
<span data-ttu-id="aff00-605">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="aff00-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
