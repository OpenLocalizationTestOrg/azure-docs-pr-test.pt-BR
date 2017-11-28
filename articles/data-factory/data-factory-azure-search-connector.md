---
title: "índice de tooSearch aaaPush dados usando a fábrica de dados | Microsoft Docs"
description: "Saiba mais sobre como dados de toopush tooAzure índice de pesquisa usando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="374bf-103">Enviar por push o índice de pesquisa do Azure tooan dados por meio do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="374bf-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="374bf-104">Este artigo descreve como os dados de toopush do toouse hello atividade de cópia de dados de origem com suporte armazenam tooAzure índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="374bf-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="374bf-105">Armazenamentos de dados de origem com suporte são listados na coluna de origem de saudação do hello [suporte para origens e coletores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="374bf-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="374bf-106">Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia e combinações de repositório de dados com suporte.</span><span class="sxs-lookup"><span data-stu-id="374bf-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="374bf-107">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="374bf-107">Enabling connectivity</span></span>
<span data-ttu-id="374bf-108">tooallow serviço da fábrica de dados se conectar o repositório de dados do local de tooan, instalar o Gateway de gerenciamento de dados em seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="374bf-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="374bf-109">Você pode instalar o gateway em Olá mesma máquina que hospeda os dados de origem Olá armazenar ou em um tooavoid máquina separada competição por recursos com dados saudação repositório.</span><span class="sxs-lookup"><span data-stu-id="374bf-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="374bf-110">Gateway de gerenciamento de dados se conecta a serviços de toocloud de fontes de dados no local de forma segura e gerenciada.</span><span class="sxs-lookup"><span data-stu-id="374bf-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="374bf-111">Consulte o artigo [Mover dados entre local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="374bf-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="374bf-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="374bf-112">Getting started</span></span>
<span data-ttu-id="374bf-113">Você pode criar um pipeline com uma atividade de cópia que envia dados de um índice de pesquisa do código-fonte dados repositório tooAzure usando APIs/ferramentas diferentes.</span><span class="sxs-lookup"><span data-stu-id="374bf-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="374bf-114">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="374bf-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="374bf-115">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="374bf-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="374bf-116">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="374bf-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="374bf-117">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="374bf-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="374bf-118">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="374bf-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="374bf-119">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="374bf-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="374bf-120">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="374bf-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="374bf-121">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="374bf-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="374bf-122">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="374bf-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="374bf-123">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="374bf-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="374bf-124">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy índice de pesquisa de tooAzure de dados, consulte [exemplo JSON: copiar dados de índice de pesquisa do local do SQL Server tooAzure](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="374bf-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="374bf-125">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure índice de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="374bf-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="374bf-126">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="374bf-126">Linked service properties</span></span>

<span data-ttu-id="374bf-127">Olá a tabela a seguir fornece descrições dos elementos JSON de serviço de pesquisa do Azure vinculada toohello específico.</span><span class="sxs-lookup"><span data-stu-id="374bf-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="374bf-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="374bf-128">Property</span></span> | <span data-ttu-id="374bf-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="374bf-129">Description</span></span> | <span data-ttu-id="374bf-130">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="374bf-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="374bf-131">type</span><span class="sxs-lookup"><span data-stu-id="374bf-131">type</span></span> | <span data-ttu-id="374bf-132">propriedade de tipo Hello deve ser definida como: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="374bf-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="374bf-133">Sim</span><span class="sxs-lookup"><span data-stu-id="374bf-133">Yes</span></span> |
| <span data-ttu-id="374bf-134">url</span><span class="sxs-lookup"><span data-stu-id="374bf-134">url</span></span> | <span data-ttu-id="374bf-135">URL de saudação serviço de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="374bf-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="374bf-136">Sim</span><span class="sxs-lookup"><span data-stu-id="374bf-136">Yes</span></span> |
| <span data-ttu-id="374bf-137">chave</span><span class="sxs-lookup"><span data-stu-id="374bf-137">key</span></span> | <span data-ttu-id="374bf-138">Chave de administração de saudação serviço de pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="374bf-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="374bf-139">Sim</span><span class="sxs-lookup"><span data-stu-id="374bf-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="374bf-140">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="374bf-140">Dataset properties</span></span>

<span data-ttu-id="374bf-141">Para obter uma lista completa de seções e propriedades que estão disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="374bf-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="374bf-142">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="374bf-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="374bf-143">Olá **typeProperties** seção é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="374bf-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="374bf-144">Olá typeProperties seção um conjunto de dados do tipo hello **AzureSearchIndex** tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="374bf-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="374bf-145">Propriedade</span><span class="sxs-lookup"><span data-stu-id="374bf-145">Property</span></span> | <span data-ttu-id="374bf-146">Descrição</span><span class="sxs-lookup"><span data-stu-id="374bf-146">Description</span></span> | <span data-ttu-id="374bf-147">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="374bf-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="374bf-148">type</span><span class="sxs-lookup"><span data-stu-id="374bf-148">type</span></span> | <span data-ttu-id="374bf-149">propriedade do tipo Hello deve ser definida muito**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="374bf-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="374bf-150">Sim</span><span class="sxs-lookup"><span data-stu-id="374bf-150">Yes</span></span> |
| <span data-ttu-id="374bf-151">indexName</span><span class="sxs-lookup"><span data-stu-id="374bf-151">indexName</span></span> | <span data-ttu-id="374bf-152">Nome do índice de pesquisa do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="374bf-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="374bf-153">Fábrica de dados não cria o índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="374bf-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="374bf-154">Olá índice deve existir na pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="374bf-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="374bf-155">Sim</span><span class="sxs-lookup"><span data-stu-id="374bf-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="374bf-156">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="374bf-156">Copy activity properties</span></span>
<span data-ttu-id="374bf-157">Para obter uma lista completa de seções e propriedades que estão disponíveis para a definição de atividades, consulte Olá [criar pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="374bf-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="374bf-158">As propriedades, como nome, descrição, tabelas de entrada e saída, e diversas políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="374bf-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="374bf-159">Por outro lado, as propriedades disponíveis na seção de typeProperties Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="374bf-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="374bf-160">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="374bf-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="374bf-161">Para a atividade de cópia, quando o coletor de saudação é do tipo de saudação **AzureSearchIndexSink**, Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="374bf-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="374bf-162">Propriedade</span><span class="sxs-lookup"><span data-stu-id="374bf-162">Property</span></span> | <span data-ttu-id="374bf-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="374bf-163">Description</span></span> | <span data-ttu-id="374bf-164">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="374bf-164">Allowed values</span></span> | <span data-ttu-id="374bf-165">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="374bf-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="374bf-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="374bf-166">WriteBehavior</span></span> | <span data-ttu-id="374bf-167">Especifica se toomerge ou substituição quando um documento já existe no índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="374bf-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="374bf-168">Consulte Olá [WriteBehavior propriedade](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="374bf-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="374bf-169">Merge (padrão)</span><span class="sxs-lookup"><span data-stu-id="374bf-169">Merge (default)</span></span><br/><span data-ttu-id="374bf-170">Carregar</span><span class="sxs-lookup"><span data-stu-id="374bf-170">Upload</span></span>| <span data-ttu-id="374bf-171">Não</span><span class="sxs-lookup"><span data-stu-id="374bf-171">No</span></span> |
| <span data-ttu-id="374bf-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="374bf-172">WriteBatchSize</span></span> | <span data-ttu-id="374bf-173">Carrega dados no índice de pesquisa do Azure hello quando o tamanho do buffer de saudação atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="374bf-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="374bf-174">Consulte Olá [WriteBatchSize propriedade](#writebatchsize-property) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="374bf-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="374bf-175">1 too1, 000.</span><span class="sxs-lookup"><span data-stu-id="374bf-175">1 too1,000.</span></span> <span data-ttu-id="374bf-176">O valor padrão é 1000.</span><span class="sxs-lookup"><span data-stu-id="374bf-176">Default value is 1000.</span></span> | <span data-ttu-id="374bf-177">Não</span><span class="sxs-lookup"><span data-stu-id="374bf-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="374bf-178">Propriedade WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="374bf-178">WriteBehavior property</span></span>
<span data-ttu-id="374bf-179">Upsert do AzureSearchSink ao gravar dados.</span><span class="sxs-lookup"><span data-stu-id="374bf-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="374bf-180">Em outras palavras, ao escrever um documento, se a chave de documento hello já existe no índice de pesquisa do Azure hello, pesquisa do Azure atualiza o documento de saudação existente em vez de gerar uma exceção de conflito.</span><span class="sxs-lookup"><span data-stu-id="374bf-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="374bf-181">Olá AzureSearchSink fornece Olá após dois comportamentos upsert (usando AzureSearch SDK):</span><span class="sxs-lookup"><span data-stu-id="374bf-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="374bf-182">**Mesclar**: combinar todas as colunas de saudação em novo documento de saudação com hello existente a um.</span><span class="sxs-lookup"><span data-stu-id="374bf-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="374bf-183">Para colunas com valor nulo em novo documento de hello, Olá valor Olá existente de um é preservado.</span><span class="sxs-lookup"><span data-stu-id="374bf-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="374bf-184">**Carregar**: substitui o documento novo Olá Olá existente.</span><span class="sxs-lookup"><span data-stu-id="374bf-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="374bf-185">Para colunas não especificadas no documento novo hello, o valor de saudação é definido toonull se há um valor não nulo no documento existente hello, ou não.</span><span class="sxs-lookup"><span data-stu-id="374bf-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="374bf-186">comportamento padrão de saudação é **mesclar**.</span><span class="sxs-lookup"><span data-stu-id="374bf-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="374bf-187">Propriedade WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="374bf-187">WriteBatchSize Property</span></span>
<span data-ttu-id="374bf-188">O serviço de Azure Search oferece suporte a escrever documentos como um lote.</span><span class="sxs-lookup"><span data-stu-id="374bf-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="374bf-189">Um lote pode conter 1 too1, ações, 000.</span><span class="sxs-lookup"><span data-stu-id="374bf-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="374bf-190">Uma ação lida com uma operação de carregamento/mesclagem documento tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="374bf-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="374bf-191">Suporte ao tipo de dados</span><span class="sxs-lookup"><span data-stu-id="374bf-191">Data type support</span></span>
<span data-ttu-id="374bf-192">Olá tabela a seguir especifica se um tipo de dados de pesquisa do Azure tem suporte ou não.</span><span class="sxs-lookup"><span data-stu-id="374bf-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="374bf-193">Tipo de dados do Azure Search</span><span class="sxs-lookup"><span data-stu-id="374bf-193">Azure Search data type</span></span> | <span data-ttu-id="374bf-194">Suporte no coletor do Azure Search</span><span class="sxs-lookup"><span data-stu-id="374bf-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="374bf-195">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="374bf-195">String</span></span> | <span data-ttu-id="374bf-196">S</span><span class="sxs-lookup"><span data-stu-id="374bf-196">Y</span></span> |
| <span data-ttu-id="374bf-197">Int32</span><span class="sxs-lookup"><span data-stu-id="374bf-197">Int32</span></span> | <span data-ttu-id="374bf-198">S</span><span class="sxs-lookup"><span data-stu-id="374bf-198">Y</span></span> |
| <span data-ttu-id="374bf-199">Int64</span><span class="sxs-lookup"><span data-stu-id="374bf-199">Int64</span></span> | <span data-ttu-id="374bf-200">S</span><span class="sxs-lookup"><span data-stu-id="374bf-200">Y</span></span> |
| <span data-ttu-id="374bf-201">Duplo</span><span class="sxs-lookup"><span data-stu-id="374bf-201">Double</span></span> | <span data-ttu-id="374bf-202">S</span><span class="sxs-lookup"><span data-stu-id="374bf-202">Y</span></span> |
| <span data-ttu-id="374bf-203">Booliano</span><span class="sxs-lookup"><span data-stu-id="374bf-203">Boolean</span></span> | <span data-ttu-id="374bf-204">S</span><span class="sxs-lookup"><span data-stu-id="374bf-204">Y</span></span> |
| <span data-ttu-id="374bf-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="374bf-205">DataTimeOffset</span></span> | <span data-ttu-id="374bf-206">S</span><span class="sxs-lookup"><span data-stu-id="374bf-206">Y</span></span> |
| <span data-ttu-id="374bf-207">Matriz de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="374bf-207">String Array</span></span> | <span data-ttu-id="374bf-208">N</span><span class="sxs-lookup"><span data-stu-id="374bf-208">N</span></span> |
| <span data-ttu-id="374bf-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="374bf-209">GeographyPoint</span></span> | <span data-ttu-id="374bf-210">N</span><span class="sxs-lookup"><span data-stu-id="374bf-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="374bf-211">Exemplo JSON: copiar dados de índice de pesquisa de tooAzure do local do SQL Server</span><span class="sxs-lookup"><span data-stu-id="374bf-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="374bf-212">Olá mostra de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="374bf-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="374bf-213">Um serviço vinculado do tipo [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="374bf-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="374bf-214">Um serviço vinculado do tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="374bf-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="374bf-215">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="374bf-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="374bf-216">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="374bf-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="374bf-217">Um [pipeline](data-factory-create-pipelines.md) com a atividade de cópia que usa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) e [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="374bf-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="374bf-218">exemplo Hello copia dados de série temporal de um índice de pesquisa do Azure tooan banco de dados do local do SQL Server por hora.</span><span class="sxs-lookup"><span data-stu-id="374bf-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="374bf-219">propriedades JSON Olá usadas neste exemplo são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="374bf-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="374bf-220">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="374bf-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="374bf-221">Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="374bf-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="374bf-222">**Serviço vinculado ao Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="374bf-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="374bf-223">**Serviço vinculado do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="374bf-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="374bf-224">**Conjunto de dados de entrada do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="374bf-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="374bf-225">exemplo Hello supõe que você criou uma tabela "MyTable" no SQL Server e contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="374bf-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="374bf-226">Você pode consultar em várias tabelas em Olá mesmo usando um único conjunto de dados, mas uma única tabela de banco de dados deve ser usado para typeProperty de tableName de saudação do dataset.</span><span class="sxs-lookup"><span data-stu-id="374bf-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="374bf-227">Definindo "externo": "verdadeiro" informa o serviço de fábrica de dados Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="374bf-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

<span data-ttu-id="374bf-228">**Conjunto de dados de saída do Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="374bf-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="374bf-229">Olá exemplo copia dados tooan Azure índice de pesquisa denominada **produtos**.</span><span class="sxs-lookup"><span data-stu-id="374bf-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="374bf-230">Fábrica de dados não cria o índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="374bf-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="374bf-231">Olá tootest de exemplo, crie um índice com este nome.</span><span class="sxs-lookup"><span data-stu-id="374bf-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="374bf-232">Criar o índice de pesquisa do Azure Olá com hello mesmo número de colunas como Olá conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="374bf-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="374bf-233">São adicionadas novas entradas toohello índice de pesquisa do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="374bf-233">New entries are added toohello Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="374bf-234">**Atividade de cópia em um pipeline com origem SQL e coletor de Índice do Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="374bf-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="374bf-235">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="374bf-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="374bf-236">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource** e **coletor** tipo está definido muito**AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="374bf-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="374bf-237">consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="374bf-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="374bf-238">Se você estiver copiando dados de um armazenamento de dados de nuvem para o Azure Search, a propriedade `executionLocation` será necessária.</span><span class="sxs-lookup"><span data-stu-id="374bf-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="374bf-239">Olá, trecho JSON a seguir mostra alterações Olá necessária na atividade de cópia `typeProperties` como exemplo.</span><span class="sxs-lookup"><span data-stu-id="374bf-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="374bf-240">Verifique a seção [Copiar dados entre armazenamentos de dados de nuvem](data-factory-data-movement-activities.md#global) para obter mais detalhes e valores com suporte.</span><span class="sxs-lookup"><span data-stu-id="374bf-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="374bf-241">Copiar de uma origem de nuvem</span><span class="sxs-lookup"><span data-stu-id="374bf-241">Copy from a cloud source</span></span>
<span data-ttu-id="374bf-242">Se você estiver copiando dados de um armazenamento de dados de nuvem para o Azure Search, a propriedade `executionLocation` será necessária.</span><span class="sxs-lookup"><span data-stu-id="374bf-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="374bf-243">Olá, trecho JSON a seguir mostra alterações Olá necessária na atividade de cópia `typeProperties` como exemplo.</span><span class="sxs-lookup"><span data-stu-id="374bf-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="374bf-244">Verifique a seção [Copiar dados entre armazenamentos de dados de nuvem](data-factory-data-movement-activities.md#global) para obter mais detalhes e valores com suporte.</span><span class="sxs-lookup"><span data-stu-id="374bf-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="374bf-245">Você também pode mapear colunas de origem toocolumns de conjunto de dados do conjunto de coletor de dados na definição de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="374bf-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="374bf-246">Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="374bf-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="374bf-247">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="374bf-247">Performance and tuning</span></span>  
<span data-ttu-id="374bf-248">Consulte Olá [atividade de cópia guia de desempenho e ajuste](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="374bf-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="374bf-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="374bf-249">Next steps</span></span>
<span data-ttu-id="374bf-250">Consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="374bf-250">See hello following articles:</span></span>

* <span data-ttu-id="374bf-251">[Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criação de um pipeline com uma Atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="374bf-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
