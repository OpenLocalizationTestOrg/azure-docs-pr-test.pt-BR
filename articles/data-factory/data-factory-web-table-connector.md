---
title: aaaMove dados da tabela da Web usando o Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre como toomove de uma tabela em uma Web de páginas de dados usando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="af580-103">Mover dados de uma fonte de tabela da Web usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af580-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="af580-104">Este artigo descreve como toouse hello atividade de cópia em dados do Azure Data Factory toomove de uma tabela em uma página da Web tooa suporte para o repositório de dados do coletor.</span><span class="sxs-lookup"><span data-stu-id="af580-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="af580-105">Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo que apresenta uma visão geral de movimentação de dados com Copiar atividade e hello lista de repositórios de dados têm suportada como/coletores de fontes.</span><span class="sxs-lookup"><span data-stu-id="af580-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="af580-106">Fábrica de dados atualmente oferece suporte somente a movimentação de dados de uma data de tooother Web tabela armazena, mas não movendo os dados de outros dados armazena tooa Web tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="af580-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af580-107">No momento, esse conector da Web dá suporte apenas à extração do conteúdo da tabela de uma página HTML.</span><span class="sxs-lookup"><span data-stu-id="af580-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="af580-108">tooretrieve de dados de um ponto de extremidade HTTP/s usar [conector HTTP](data-factory-http-connector.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="af580-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="af580-109">Introdução</span><span class="sxs-lookup"><span data-stu-id="af580-109">Getting started</span></span>
<span data-ttu-id="af580-110">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="af580-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="af580-111">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="af580-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="af580-112">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="af580-113">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="af580-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="af580-114">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="af580-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="af580-115">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="af580-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="af580-116">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="af580-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="af580-117">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="af580-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="af580-118">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="af580-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="af580-119">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="af580-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="af580-120">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="af580-121">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de uma tabela da web, consulte [exemplo JSON: copiar dados da tabela de Web tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="af580-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="af580-122">Olá seções a seguir fornece detalhes sobre as propriedades JSON que a tabela usada toodefine fábrica de dados entidades tooa específico da Web:</span><span class="sxs-lookup"><span data-stu-id="af580-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="af580-123">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="af580-123">Linked service properties</span></span>
<span data-ttu-id="af580-124">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooWeb vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="af580-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="af580-125">Propriedade</span><span class="sxs-lookup"><span data-stu-id="af580-125">Property</span></span> | <span data-ttu-id="af580-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="af580-126">Description</span></span> | <span data-ttu-id="af580-127">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="af580-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af580-128">type</span><span class="sxs-lookup"><span data-stu-id="af580-128">type</span></span> |<span data-ttu-id="af580-129">propriedade de tipo Hello deve ser definida como: **Web**</span><span class="sxs-lookup"><span data-stu-id="af580-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="af580-130">Sim</span><span class="sxs-lookup"><span data-stu-id="af580-130">Yes</span></span> |
| <span data-ttu-id="af580-131">Url</span><span class="sxs-lookup"><span data-stu-id="af580-131">Url</span></span> |<span data-ttu-id="af580-132">Origem da URL toohello da Web</span><span class="sxs-lookup"><span data-stu-id="af580-132">URL toohello Web source</span></span> |<span data-ttu-id="af580-133">Sim</span><span class="sxs-lookup"><span data-stu-id="af580-133">Yes</span></span> |
| <span data-ttu-id="af580-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="af580-134">authenticationType</span></span> |<span data-ttu-id="af580-135">Anônima.</span><span class="sxs-lookup"><span data-stu-id="af580-135">Anonymous.</span></span> |<span data-ttu-id="af580-136">Sim</span><span class="sxs-lookup"><span data-stu-id="af580-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="af580-137">Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="af580-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="af580-138">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="af580-138">Dataset properties</span></span>
<span data-ttu-id="af580-139">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="af580-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="af580-140">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="af580-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="af580-141">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="af580-142">Olá typeProperties seção de conjunto de dados do tipo **WebTable** tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="af580-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="af580-143">Propriedade</span><span class="sxs-lookup"><span data-stu-id="af580-143">Property</span></span> | <span data-ttu-id="af580-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="af580-144">Description</span></span> | <span data-ttu-id="af580-145">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="af580-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="af580-146">type</span><span class="sxs-lookup"><span data-stu-id="af580-146">type</span></span> |<span data-ttu-id="af580-147">Tipo de conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-147">type of hello dataset.</span></span> <span data-ttu-id="af580-148">deve ser definido muito**WebTable**</span><span class="sxs-lookup"><span data-stu-id="af580-148">must be set too**WebTable**</span></span> |<span data-ttu-id="af580-149">Sim</span><span class="sxs-lookup"><span data-stu-id="af580-149">Yes</span></span> |
| <span data-ttu-id="af580-150">path</span><span class="sxs-lookup"><span data-stu-id="af580-150">path</span></span> |<span data-ttu-id="af580-151">Um relativa URL toohello de recursos que contém a tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="af580-152">Não.</span><span class="sxs-lookup"><span data-stu-id="af580-152">No.</span></span> <span data-ttu-id="af580-153">Quando não for especificado, somente URL Olá especificado na definição de serviço vinculada de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="af580-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="af580-154">índice</span><span class="sxs-lookup"><span data-stu-id="af580-154">index</span></span> |<span data-ttu-id="af580-155">índice de saudação da tabela de saudação no recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="af580-156">Consulte [índice de obtenção de uma tabela em uma página HTML](#get-index-of-a-table-in-an-html-page) seção de índice de toogetting de etapas de uma tabela em uma página HTML.</span><span class="sxs-lookup"><span data-stu-id="af580-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="af580-157">Sim</span><span class="sxs-lookup"><span data-stu-id="af580-157">Yes</span></span> |

<span data-ttu-id="af580-158">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="af580-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="af580-159">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="af580-159">Copy activity properties</span></span>
<span data-ttu-id="af580-160">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="af580-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="af580-161">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="af580-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="af580-162">Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="af580-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="af580-163">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="af580-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="af580-164">Atualmente, quando a fonte de saudação na atividade de cópia é do tipo **WebSource**, sem propriedades adicionais são suportadas.</span><span class="sxs-lookup"><span data-stu-id="af580-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="af580-165">Exemplo JSON: copiar dados da tabela de Web tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="af580-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="af580-166">Olá mostra de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="af580-166">hello following sample shows:</span></span>

1. <span data-ttu-id="af580-167">Um serviço vinculado do tipo [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="af580-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="af580-168">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="af580-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="af580-169">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="af580-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="af580-170">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="af580-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="af580-171">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [WebSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="af580-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="af580-172">exemplo Hello copia dados de uma tabela de Web tooan BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="af580-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="af580-173">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="af580-174">saudação de exemplo a seguir mostra como toocopy dados de uma tabela de Web tooan Azure blob.</span><span class="sxs-lookup"><span data-stu-id="af580-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="af580-175">No entanto, os dados podem ser copiados diretamente tooany de saudação coletores Olá indicado em [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="af580-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="af580-176">**Serviço vinculado do Web** Este exemplo usa Olá Web vinculado de serviço com a autenticação anônima.</span><span class="sxs-lookup"><span data-stu-id="af580-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="af580-177">Confira a seção [Serviço vinculado à Web](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="af580-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="af580-178">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="af580-178">**Azure Storage linked service**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="af580-179">**Conjunto de dados de entrada do WebTable** configuração **externo** muito**true** informa o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade em Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="af580-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="af580-180">Consulte [índice de obtenção de uma tabela em uma página HTML](#get-index-of-a-table-in-an-html-page) seção de índice de toogetting de etapas de uma tabela em uma página HTML.</span><span class="sxs-lookup"><span data-stu-id="af580-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="af580-181">**Conjunto de dados de saída de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="af580-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="af580-182">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="af580-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="af580-183">**Pipeline com Atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="af580-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="af580-184">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="af580-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="af580-185">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**WebSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="af580-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="af580-186">Consulte [propriedades de tipo WebSource](#copy-activity-type-properties) para lista de saudação de propriedades com suporte pelo Olá WebSource.</span><span class="sxs-lookup"><span data-stu-id="af580-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="af580-187">Obter índice de uma tabela em uma página HTML</span><span class="sxs-lookup"><span data-stu-id="af580-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="af580-188">Iniciar **Excel 2016** e alternar toohello **dados** guia.</span><span class="sxs-lookup"><span data-stu-id="af580-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="af580-189">Clique em **nova consulta** na barra de ferramentas hello, ponto muito**de outras fontes** e clique em **da Web**.</span><span class="sxs-lookup"><span data-stu-id="af580-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Menu do Power Query](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="af580-191">Em Olá **da Web** caixa de diálogo, digite **URL** que você usaria no serviço JSON vinculado (por exemplo: https://en.wikipedia.org/wiki/) juntamente com o caminho, você especificaria Olá conjunto de dados (por exemplo: AFI % 27s_100_Years... 100_Movies) e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="af580-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Do diálogo da Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="af580-193">URL usada neste exemplo: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="af580-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="af580-194">Se você vir **conteúdo da Web de acesso** caixa de diálogo, o direito de saudação selecione **URL**, **autenticação**e clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="af580-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Acessar caixa de diálogo de conteúdo da Web](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="af580-196">Clique em uma **tabela** Olá árvore exibir toosee o conteúdo da tabela de saudação de item e, em seguida, clique em **editar** botão na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![Diálogo de navegador](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="af580-198">Em Olá **Editor de consultas** janela, clique em **Editor Avançado** botão na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![Botão Editor Avançado](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="af580-200">Na caixa de diálogo Editor Avançado hello, Olá número próximo muito "Origem" é o índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![Editor Avançado – índice](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="af580-202">Se você estiver usando o Excel 2013, use [Microsoft Power Query para Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="af580-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="af580-203">Consulte [página de web conectar tooa](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="af580-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="af580-204">etapas de saudação são semelhantes, se você estiver usando [Microsoft Power BI para a área de trabalho](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="af580-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="af580-205">colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="af580-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="af580-206">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="af580-206">Performance and Tuning</span></span>
<span data-ttu-id="af580-207">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="af580-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
