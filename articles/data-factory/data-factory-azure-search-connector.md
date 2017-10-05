---
title: "Enviar dados ao índice de pesquisa usando o Data Factory | Microsoft Docs"
description: "Saiba mais sobre como enviar dados por push ao Índice do Azure Search usando o Azure Data Factory."
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
ms.openlocfilehash: 5c617c7a2f2eb4da2164ce5f802354a64dfd1fa1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="852da-103">Enviar dados para um índice do Azure Search usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="852da-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="852da-104">Este artigo descreve como usar a Atividade de Cópia para enviar por push dados de um repositório de dados de origem com suporte para o índice do Azure Search.</span><span class="sxs-lookup"><span data-stu-id="852da-104">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="852da-105">Armazenamentos de dados de origem com suporte listados na coluna de origem a [fontes e coletores com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="852da-105">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="852da-106">Este artigo se baseia no artigo de [atividades de movimentação de dados](data-factory-data-movement-activities.md) , que apresenta uma visão geral de movimentação de dados com a Atividade de Cópia e combinações de armazenamentos de dados com suporte.</span><span class="sxs-lookup"><span data-stu-id="852da-106">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="852da-107">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="852da-107">Enabling connectivity</span></span>
<span data-ttu-id="852da-108">Para permitir que o serviço se conecte a um armazenamento de dados local do Data Factory, instale o Gateway de Gerenciamento de Dados em seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="852da-108">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="852da-109">Você pode instalar o gateway na mesma máquina que hospeda o banco de dados ou em uma máquina separada para evitar a concorrência por recursos com o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="852da-109">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="852da-110">O Gateway de Gerenciamento de Dados conecta fontes de dados locais a serviços de nuvem de maneira segura e gerenciada.</span><span class="sxs-lookup"><span data-stu-id="852da-110">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="852da-111">Consulte o artigo [Mover dados entre local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="852da-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="852da-112">Introdução</span><span class="sxs-lookup"><span data-stu-id="852da-112">Getting started</span></span>
<span data-ttu-id="852da-113">Você pode criar um pipeline com uma atividade de cópia que envie dados por push de um repositório de dados de origem para o índice do Azure Search usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="852da-113">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="852da-114">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="852da-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="852da-115">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="852da-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="852da-116">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="852da-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="852da-117">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="852da-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="852da-118">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="852da-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="852da-119">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="852da-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="852da-120">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="852da-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="852da-121">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="852da-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="852da-122">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="852da-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="852da-123">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="852da-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="852da-124">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um índice do Azure Search, confira a seção [Exemplo de JSON: Copiar dados do SQL Server local para o índice do Azure Search](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="852da-124">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="852da-125">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao índice do Azure Search:</span><span class="sxs-lookup"><span data-stu-id="852da-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="852da-126">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="852da-126">Linked service properties</span></span>

<span data-ttu-id="852da-127">A tabela a seguir fornece descrições dos elementos JSON específicos para o serviço vinculado Azure Search.</span><span class="sxs-lookup"><span data-stu-id="852da-127">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="852da-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="852da-128">Property</span></span> | <span data-ttu-id="852da-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="852da-129">Description</span></span> | <span data-ttu-id="852da-130">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="852da-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="852da-131">type</span><span class="sxs-lookup"><span data-stu-id="852da-131">type</span></span> | <span data-ttu-id="852da-132">A propriedade type deve ser definida como: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="852da-132">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="852da-133">Sim</span><span class="sxs-lookup"><span data-stu-id="852da-133">Yes</span></span> |
| <span data-ttu-id="852da-134">URL</span><span class="sxs-lookup"><span data-stu-id="852da-134">url</span></span> | <span data-ttu-id="852da-135">URL para o serviço Azure Search.</span><span class="sxs-lookup"><span data-stu-id="852da-135">URL for the Azure Search service.</span></span> | <span data-ttu-id="852da-136">Sim</span><span class="sxs-lookup"><span data-stu-id="852da-136">Yes</span></span> |
| <span data-ttu-id="852da-137">chave</span><span class="sxs-lookup"><span data-stu-id="852da-137">key</span></span> | <span data-ttu-id="852da-138">Chave de administração para o serviço Azure Search.</span><span class="sxs-lookup"><span data-stu-id="852da-138">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="852da-139">Sim</span><span class="sxs-lookup"><span data-stu-id="852da-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="852da-140">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="852da-140">Dataset properties</span></span>

<span data-ttu-id="852da-141">Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, veja o artigo [Criando conjuntos de dados](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="852da-141">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="852da-142">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="852da-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="852da-143">A seção **typeProperties** é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="852da-143">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="852da-144">A seção typeProperties para um conjunto de dados do tipo **AzureSearchIndex** tem as propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="852da-144">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="852da-145">Propriedade</span><span class="sxs-lookup"><span data-stu-id="852da-145">Property</span></span> | <span data-ttu-id="852da-146">Descrição</span><span class="sxs-lookup"><span data-stu-id="852da-146">Description</span></span> | <span data-ttu-id="852da-147">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="852da-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="852da-148">type</span><span class="sxs-lookup"><span data-stu-id="852da-148">type</span></span> | <span data-ttu-id="852da-149">A propriedade type deve ser definida como: **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="852da-149">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="852da-150">Sim</span><span class="sxs-lookup"><span data-stu-id="852da-150">Yes</span></span> |
| <span data-ttu-id="852da-151">indexName</span><span class="sxs-lookup"><span data-stu-id="852da-151">indexName</span></span> | <span data-ttu-id="852da-152">Nome do índice do Azure Search.</span><span class="sxs-lookup"><span data-stu-id="852da-152">Name of the Azure Search index.</span></span> <span data-ttu-id="852da-153">O Data Factory não cria o índice.</span><span class="sxs-lookup"><span data-stu-id="852da-153">Data Factory does not create the index.</span></span> <span data-ttu-id="852da-154">O índice deve existir no Azure Search.</span><span class="sxs-lookup"><span data-stu-id="852da-154">The index must exist in Azure Search.</span></span> | <span data-ttu-id="852da-155">Sim</span><span class="sxs-lookup"><span data-stu-id="852da-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="852da-156">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="852da-156">Copy activity properties</span></span>
<span data-ttu-id="852da-157">Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, veja o artigo [Criando pipelines](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="852da-157">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="852da-158">As propriedades, como nome, descrição, tabelas de entrada e saída, e diversas políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="852da-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="852da-159">Por outro lado, as propriedades disponíveis na seção typeProperties variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="852da-159">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="852da-160">Para a Atividade de Cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="852da-160">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="852da-161">Na Atividade de Cópia, quando o coletor é do tipo **AzureSearchIndexSink**, as seguintes propriedades estão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="852da-161">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="852da-162">Propriedade</span><span class="sxs-lookup"><span data-stu-id="852da-162">Property</span></span> | <span data-ttu-id="852da-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="852da-163">Description</span></span> | <span data-ttu-id="852da-164">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="852da-164">Allowed values</span></span> | <span data-ttu-id="852da-165">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="852da-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="852da-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="852da-166">WriteBehavior</span></span> | <span data-ttu-id="852da-167">Especifica se deve mesclar ou substituir quando já existe um documento no índice.</span><span class="sxs-lookup"><span data-stu-id="852da-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="852da-168">Veja a [propriedade WriteBehavior](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="852da-168">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="852da-169">Merge (padrão)</span><span class="sxs-lookup"><span data-stu-id="852da-169">Merge (default)</span></span><br/><span data-ttu-id="852da-170">Carregar</span><span class="sxs-lookup"><span data-stu-id="852da-170">Upload</span></span>| <span data-ttu-id="852da-171">Não</span><span class="sxs-lookup"><span data-stu-id="852da-171">No</span></span> |
| <span data-ttu-id="852da-172">WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="852da-172">WriteBatchSize</span></span> | <span data-ttu-id="852da-173">Carrega dados para o índice do Azure Search quando o tamanho do buffer atinge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="852da-173">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="852da-174">Veja a [propriedade WriteBatchSize](#writebatchsize-property) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="852da-174">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="852da-175">1 a 1.000.</span><span class="sxs-lookup"><span data-stu-id="852da-175">1 to 1,000.</span></span> <span data-ttu-id="852da-176">O valor padrão é 1000.</span><span class="sxs-lookup"><span data-stu-id="852da-176">Default value is 1000.</span></span> | <span data-ttu-id="852da-177">Não</span><span class="sxs-lookup"><span data-stu-id="852da-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="852da-178">Propriedade WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="852da-178">WriteBehavior property</span></span>
<span data-ttu-id="852da-179">Upsert do AzureSearchSink ao gravar dados.</span><span class="sxs-lookup"><span data-stu-id="852da-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="852da-180">Em outras palavras, ao escrever um documento, se a chave do documento já existe no índice do Azure Search, o Azure Search atualiza o documento existente, em vez de lançar uma exceção de conflito.</span><span class="sxs-lookup"><span data-stu-id="852da-180">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="852da-181">O AzureSearchSink fornece estes dois comportamentos de upsert (usando o SDK da AzureSearch):</span><span class="sxs-lookup"><span data-stu-id="852da-181">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="852da-182">**Mesclar**: combine todas as colunas no novo documento com a existente.</span><span class="sxs-lookup"><span data-stu-id="852da-182">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="852da-183">Para colunas com valor nulo no novo documento, o valor existente é preservado.</span><span class="sxs-lookup"><span data-stu-id="852da-183">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="852da-184">**Carregar**: o novo documento substituirá o existente.</span><span class="sxs-lookup"><span data-stu-id="852da-184">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="852da-185">Para colunas não especificadas no novo documento, o valor será definido como nulo se houver um valor não nulo no documento existente ou não.</span><span class="sxs-lookup"><span data-stu-id="852da-185">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="852da-186">O comportamento padrão é **Mesclar**.</span><span class="sxs-lookup"><span data-stu-id="852da-186">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="852da-187">Propriedade WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="852da-187">WriteBatchSize Property</span></span>
<span data-ttu-id="852da-188">O serviço de Azure Search oferece suporte a escrever documentos como um lote.</span><span class="sxs-lookup"><span data-stu-id="852da-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="852da-189">Um lote pode conter de 1 a 1.000 ações.</span><span class="sxs-lookup"><span data-stu-id="852da-189">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="852da-190">Uma ação manipula um documento para executar a operação de carregamento/mesclagem.</span><span class="sxs-lookup"><span data-stu-id="852da-190">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="852da-191">Suporte ao tipo de dados</span><span class="sxs-lookup"><span data-stu-id="852da-191">Data type support</span></span>
<span data-ttu-id="852da-192">A tabela a seguir especifica se um tipo de dados do Azure Search tem suporte ou não.</span><span class="sxs-lookup"><span data-stu-id="852da-192">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="852da-193">Tipo de dados do Azure Search</span><span class="sxs-lookup"><span data-stu-id="852da-193">Azure Search data type</span></span> | <span data-ttu-id="852da-194">Suporte no coletor do Azure Search</span><span class="sxs-lookup"><span data-stu-id="852da-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="852da-195">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="852da-195">String</span></span> | <span data-ttu-id="852da-196">S</span><span class="sxs-lookup"><span data-stu-id="852da-196">Y</span></span> |
| <span data-ttu-id="852da-197">Int32</span><span class="sxs-lookup"><span data-stu-id="852da-197">Int32</span></span> | <span data-ttu-id="852da-198">S</span><span class="sxs-lookup"><span data-stu-id="852da-198">Y</span></span> |
| <span data-ttu-id="852da-199">Int64</span><span class="sxs-lookup"><span data-stu-id="852da-199">Int64</span></span> | <span data-ttu-id="852da-200">S</span><span class="sxs-lookup"><span data-stu-id="852da-200">Y</span></span> |
| <span data-ttu-id="852da-201">Duplo</span><span class="sxs-lookup"><span data-stu-id="852da-201">Double</span></span> | <span data-ttu-id="852da-202">S</span><span class="sxs-lookup"><span data-stu-id="852da-202">Y</span></span> |
| <span data-ttu-id="852da-203">Booliano</span><span class="sxs-lookup"><span data-stu-id="852da-203">Boolean</span></span> | <span data-ttu-id="852da-204">S</span><span class="sxs-lookup"><span data-stu-id="852da-204">Y</span></span> |
| <span data-ttu-id="852da-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="852da-205">DataTimeOffset</span></span> | <span data-ttu-id="852da-206">S</span><span class="sxs-lookup"><span data-stu-id="852da-206">Y</span></span> |
| <span data-ttu-id="852da-207">Matriz de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="852da-207">String Array</span></span> | <span data-ttu-id="852da-208">N</span><span class="sxs-lookup"><span data-stu-id="852da-208">N</span></span> |
| <span data-ttu-id="852da-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="852da-209">GeographyPoint</span></span> | <span data-ttu-id="852da-210">N</span><span class="sxs-lookup"><span data-stu-id="852da-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="852da-211">Exemplo de JSON: Copiar dados do SQL Server local para o índice do Azure Search</span><span class="sxs-lookup"><span data-stu-id="852da-211">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="852da-212">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="852da-212">The following sample shows:</span></span>

1.  <span data-ttu-id="852da-213">Um serviço vinculado do tipo [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="852da-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="852da-214">Um serviço vinculado do tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="852da-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="852da-215">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="852da-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="852da-216">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="852da-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="852da-217">Um [pipeline](data-factory-create-pipelines.md) com a atividade de cópia que usa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) e [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="852da-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="852da-218">O exemplo copia dados de série temporal de um banco de dados do SQL Server local para um índice do Azure Search por hora.</span><span class="sxs-lookup"><span data-stu-id="852da-218">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="852da-219">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="852da-219">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="852da-220">Como uma primeira etapa, configure o gateway de gerenciamento de dados em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="852da-220">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="852da-221">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="852da-221">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="852da-222">**Serviço vinculado ao Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="852da-222">**Azure Search linked service:**</span></span>

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

<span data-ttu-id="852da-223">**Serviço vinculado do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="852da-223">**SQL Server linked service**</span></span>

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

<span data-ttu-id="852da-224">**Conjunto de dados de entrada do SQL Server**</span><span class="sxs-lookup"><span data-stu-id="852da-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="852da-225">O exemplo supõe que você criou uma tabela "MyTable" no SQL Server e que ela contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="852da-225">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="852da-226">Você pode consultar várias tabelas no mesmo banco de dados usando um único conjunto de dados, mas uma única tabela deve ser usada para a typeProperty de tableName do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="852da-226">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="852da-227">Configurar "external": "true" informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="852da-227">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="852da-228">**Conjunto de dados de saída do Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="852da-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="852da-229">O exemplo copia dados para um índice do Azure Search chamado **produtos**.</span><span class="sxs-lookup"><span data-stu-id="852da-229">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="852da-230">O Data Factory não cria o índice.</span><span class="sxs-lookup"><span data-stu-id="852da-230">Data Factory does not create the index.</span></span> <span data-ttu-id="852da-231">Para testar o exemplo, crie um índice com esse nome.</span><span class="sxs-lookup"><span data-stu-id="852da-231">To test the sample, create an index with this name.</span></span> <span data-ttu-id="852da-232">Crie o índice do Azure Search com o mesmo número de colunas do que o conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="852da-232">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="852da-233">Novas entradas são adicionadas ao índice do Azure Search a cada hora.</span><span class="sxs-lookup"><span data-stu-id="852da-233">New entries are added to the Azure Search index every hour.</span></span>

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

<span data-ttu-id="852da-234">**Atividade de cópia em um pipeline com origem SQL e coletor de Índice do Azure Search:**</span><span class="sxs-lookup"><span data-stu-id="852da-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="852da-235">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="852da-235">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="852da-236">Na definição de JSON do pipeline, o tipo de **fonte** está definido como **SqlSource** e o tipo de **coletor** está definido como **AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="852da-236">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="852da-237">A consulta SQL especificada para a propriedade **SqlReaderQuery** seleciona os dados na última hora a serem copiados.</span><span class="sxs-lookup"><span data-stu-id="852da-237">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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

<span data-ttu-id="852da-238">Se você estiver copiando dados de um armazenamento de dados de nuvem para o Azure Search, a propriedade `executionLocation` será necessária.</span><span class="sxs-lookup"><span data-stu-id="852da-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="852da-239">O trecho JSON a seguir mostra a alteração necessária na Atividade de Cópia `typeProperties` como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="852da-239">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="852da-240">Verifique a seção [Copiar dados entre armazenamentos de dados de nuvem](data-factory-data-movement-activities.md#global) para obter mais detalhes e valores com suporte.</span><span class="sxs-lookup"><span data-stu-id="852da-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="852da-241">Copiar de uma origem de nuvem</span><span class="sxs-lookup"><span data-stu-id="852da-241">Copy from a cloud source</span></span>
<span data-ttu-id="852da-242">Se você estiver copiando dados de um armazenamento de dados de nuvem para o Azure Search, a propriedade `executionLocation` será necessária.</span><span class="sxs-lookup"><span data-stu-id="852da-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="852da-243">O trecho JSON a seguir mostra a alteração necessária na Atividade de Cópia `typeProperties` como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="852da-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="852da-244">Verifique a seção [Copiar dados entre armazenamentos de dados de nuvem](data-factory-data-movement-activities.md#global) para obter mais detalhes e valores com suporte.</span><span class="sxs-lookup"><span data-stu-id="852da-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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

<span data-ttu-id="852da-245">Você também pode mapear colunas do conjunto de dados de origem para colunas do conjunto de dados de coletor na definição da atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="852da-245">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="852da-246">Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="852da-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="852da-247">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="852da-247">Performance and tuning</span></span>  
<span data-ttu-id="852da-248">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho e a movimentação dos dados (Atividade de Cópia), além de várias maneiras de otimizar.</span><span class="sxs-lookup"><span data-stu-id="852da-248">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="852da-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="852da-249">Next steps</span></span>
<span data-ttu-id="852da-250">Confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="852da-250">See the following articles:</span></span>

* <span data-ttu-id="852da-251">[Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criação de um pipeline com uma Atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="852da-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
