---
title: "aaaMove dados do Amazon Redshift utilizando a fábrica de dados | Microsoft Docs"
description: Saiba mais sobre como toomove dados do Amazon Redshift usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="42091-103">Mover dados do Amazon Redshift usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="42091-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="42091-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove do Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="42091-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="42091-105">Olá artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="42091-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="42091-106">Você pode copiar dados de repositório de dados do Amazon Redshift tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="42091-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="42091-107">Para obter uma lista de repositórios de dados com suporte como coletores de atividade de cópia hello, consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="42091-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="42091-108">Fábrica de dados atualmente oferece suporte à movimentação de dados de armazenamentos de dados do Amazon Redshift tooother, mas não para mover dados de outros armazenamentos de dados tooAmazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="42091-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42091-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="42091-109">Prerequisites</span></span>
* <span data-ttu-id="42091-110">Se você estiver movendo o repositório de dados do local de tooan dados, instalar [Data Management Gateway](data-factory-data-management-gateway.md) em uma máquina local.</span><span class="sxs-lookup"><span data-stu-id="42091-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="42091-111">Em seguida, conceder Data Management Gateway (use o endereço IP da máquina de saudação) Olá tooAmazon Redshift cluster de acesso.</span><span class="sxs-lookup"><span data-stu-id="42091-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="42091-112">Consulte [cluster do autorizar acesso toohello](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="42091-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="42091-113">Se você estiver movendo o repositório de dados do Azure tooan dados, consulte [intervalos de IP do Azure Data Center](https://www.microsoft.com/download/details.aspx?id=41653) para endereço de IP de computação hello e intervalos SQL usados pelo Olá data centers do Azure.</span><span class="sxs-lookup"><span data-stu-id="42091-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="42091-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="42091-114">Getting started</span></span>
<span data-ttu-id="42091-115">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem do Amazon Redshift usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="42091-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="42091-116">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="42091-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="42091-117">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="42091-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="42091-118">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="42091-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="42091-119">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="42091-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="42091-120">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="42091-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="42091-121">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="42091-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="42091-122">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="42091-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="42091-123">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="42091-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="42091-124">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="42091-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="42091-125">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="42091-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="42091-126">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados do Amazon Redshift, consulte [exemplo JSON: copiar dados do Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="42091-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="42091-127">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAmazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="42091-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="42091-128">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="42091-128">Linked service properties</span></span>
<span data-ttu-id="42091-129">Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooAmazon Redshift vinculado de serviço.</span><span class="sxs-lookup"><span data-stu-id="42091-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="42091-130">Propriedade</span><span class="sxs-lookup"><span data-stu-id="42091-130">Property</span></span> | <span data-ttu-id="42091-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="42091-131">Description</span></span> | <span data-ttu-id="42091-132">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="42091-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="42091-133">type</span><span class="sxs-lookup"><span data-stu-id="42091-133">type</span></span> |<span data-ttu-id="42091-134">propriedade de tipo Hello deve ser definida como: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="42091-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="42091-135">Sim</span><span class="sxs-lookup"><span data-stu-id="42091-135">Yes</span></span> |
| <span data-ttu-id="42091-136">server</span><span class="sxs-lookup"><span data-stu-id="42091-136">server</span></span> |<span data-ttu-id="42091-137">IP endereço ou nome de host do servidor do Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="42091-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="42091-138">Sim</span><span class="sxs-lookup"><span data-stu-id="42091-138">Yes</span></span> |
| <span data-ttu-id="42091-139">porta</span><span class="sxs-lookup"><span data-stu-id="42091-139">port</span></span> |<span data-ttu-id="42091-140">número de saudação de porta TCP Olá Olá Amazon Redshift server usa toolisten para conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="42091-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="42091-141">Não, valor padrão: 5439</span><span class="sxs-lookup"><span data-stu-id="42091-141">No, default value: 5439</span></span> |
| <span data-ttu-id="42091-142">database</span><span class="sxs-lookup"><span data-stu-id="42091-142">database</span></span> |<span data-ttu-id="42091-143">Nome do banco de dados do Amazon Redshift hello.</span><span class="sxs-lookup"><span data-stu-id="42091-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="42091-144">Sim</span><span class="sxs-lookup"><span data-stu-id="42091-144">Yes</span></span> |
| <span data-ttu-id="42091-145">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="42091-145">username</span></span> |<span data-ttu-id="42091-146">Nome de usuário que tem o banco de dados do access toohello.</span><span class="sxs-lookup"><span data-stu-id="42091-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="42091-147">Sim</span><span class="sxs-lookup"><span data-stu-id="42091-147">Yes</span></span> |
| <span data-ttu-id="42091-148">Senha</span><span class="sxs-lookup"><span data-stu-id="42091-148">password</span></span> |<span data-ttu-id="42091-149">Senha da conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="42091-149">Password for hello user account.</span></span> |<span data-ttu-id="42091-150">Sim</span><span class="sxs-lookup"><span data-stu-id="42091-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="42091-151">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="42091-151">Dataset properties</span></span>
<span data-ttu-id="42091-152">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="42091-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="42091-153">As seções como structure, availability e policy são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="42091-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="42091-154">Olá **typeProperties** seção é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="42091-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="42091-155">Ele fornece informações sobre localização de saudação do dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="42091-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="42091-156">Olá typeProperties seção de conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados do Amazon Redshift) tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="42091-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="42091-157">Propriedade</span><span class="sxs-lookup"><span data-stu-id="42091-157">Property</span></span> | <span data-ttu-id="42091-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="42091-158">Description</span></span> | <span data-ttu-id="42091-159">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="42091-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="42091-160">tableName</span><span class="sxs-lookup"><span data-stu-id="42091-160">tableName</span></span> |<span data-ttu-id="42091-161">Nome de tabela Olá Olá Amazon Redshift banco de dados do qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="42091-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="42091-162">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="42091-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="42091-163">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="42091-163">Copy activity properties</span></span>
<span data-ttu-id="42091-164">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="42091-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="42091-165">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="42091-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="42091-166">Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="42091-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="42091-167">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="42091-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="42091-168">Quando a origem da atividade de cópia é do tipo **RelationalSource** (que inclui Amazon Redshift), Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="42091-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="42091-169">Propriedade</span><span class="sxs-lookup"><span data-stu-id="42091-169">Property</span></span> | <span data-ttu-id="42091-170">Descrição</span><span class="sxs-lookup"><span data-stu-id="42091-170">Description</span></span> | <span data-ttu-id="42091-171">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="42091-171">Allowed values</span></span> | <span data-ttu-id="42091-172">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="42091-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="42091-173">query</span><span class="sxs-lookup"><span data-stu-id="42091-173">query</span></span> |<span data-ttu-id="42091-174">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="42091-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="42091-175">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="42091-175">SQL query string.</span></span> <span data-ttu-id="42091-176">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="42091-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="42091-177">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="42091-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="42091-178">Exemplo JSON: copiar dados do Amazon Redshift tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="42091-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="42091-179">Este exemplo mostra como banco de dados toocopy um Amazon Redshift dados tooan armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="42091-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="42091-180">No entanto, os dados podem ser copiados **diretamente** tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="42091-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="42091-181">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="42091-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="42091-182">Um serviço vinculado do tipo [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="42091-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="42091-183">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="42091-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="42091-184">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="42091-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="42091-185">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="42091-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="42091-186">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="42091-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="42091-187">exemplo Hello copia dados de um resultado de consulta no Amazon Redshift tooa blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="42091-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="42091-188">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="42091-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="42091-189">**Serviço vinculado do Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="42091-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="42091-190">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="42091-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="42091-191">**Conjunto de dados de entrada do Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="42091-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="42091-192">Configuração `"external": true` informa o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="42091-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="42091-193">Defina essa propriedade tootrue em um conjunto de dados de entrada não é produzido por uma atividade no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="42091-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="42091-194">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="42091-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="42091-195">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="42091-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="42091-196">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="42091-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="42091-197">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="42091-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="42091-198">**Atividade de cópia em um pipeline com origem Azure Redshift (RelationalSource) e coletor Blob:**</span><span class="sxs-lookup"><span data-stu-id="42091-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="42091-199">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="42091-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="42091-200">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="42091-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="42091-201">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="42091-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="42091-202">Mapeamento de tipo para o Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="42091-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="42091-203">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="42091-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="42091-204">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="42091-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="42091-205">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="42091-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="42091-206">Ao mover dados tooAmazon Redshift, Olá mapeamentos a seguir é usado de tipos do Amazon Redshift tipos too.NET.</span><span class="sxs-lookup"><span data-stu-id="42091-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="42091-207">Tipo do Redshift Amazon</span><span class="sxs-lookup"><span data-stu-id="42091-207">Amazon Redshift Type</span></span> | <span data-ttu-id="42091-208">Tipo baseado no .NET</span><span class="sxs-lookup"><span data-stu-id="42091-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="42091-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="42091-209">SMALLINT</span></span> |<span data-ttu-id="42091-210">Int16</span><span class="sxs-lookup"><span data-stu-id="42091-210">Int16</span></span> |
| <span data-ttu-id="42091-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="42091-211">INTEGER</span></span> |<span data-ttu-id="42091-212">Int32</span><span class="sxs-lookup"><span data-stu-id="42091-212">Int32</span></span> |
| <span data-ttu-id="42091-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="42091-213">BIGINT</span></span> |<span data-ttu-id="42091-214">Int64</span><span class="sxs-lookup"><span data-stu-id="42091-214">Int64</span></span> |
| <span data-ttu-id="42091-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="42091-215">DECIMAL</span></span> |<span data-ttu-id="42091-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="42091-216">Decimal</span></span> |
| <span data-ttu-id="42091-217">REAL</span><span class="sxs-lookup"><span data-stu-id="42091-217">REAL</span></span> |<span data-ttu-id="42091-218">Single</span><span class="sxs-lookup"><span data-stu-id="42091-218">Single</span></span> |
| <span data-ttu-id="42091-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="42091-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="42091-220">Duplo</span><span class="sxs-lookup"><span data-stu-id="42091-220">Double</span></span> |
| <span data-ttu-id="42091-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="42091-221">BOOLEAN</span></span> |<span data-ttu-id="42091-222">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="42091-222">String</span></span> |
| <span data-ttu-id="42091-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="42091-223">CHAR</span></span> |<span data-ttu-id="42091-224">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="42091-224">String</span></span> |
| <span data-ttu-id="42091-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="42091-225">VARCHAR</span></span> |<span data-ttu-id="42091-226">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="42091-226">String</span></span> |
| <span data-ttu-id="42091-227">DATE</span><span class="sxs-lookup"><span data-stu-id="42091-227">DATE</span></span> |<span data-ttu-id="42091-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="42091-228">DateTime</span></span> |
| <span data-ttu-id="42091-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="42091-229">TIMESTAMP</span></span> |<span data-ttu-id="42091-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="42091-230">DateTime</span></span> |
| <span data-ttu-id="42091-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="42091-231">TEXT</span></span> |<span data-ttu-id="42091-232">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="42091-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="42091-233">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="42091-233">Map source toosink columns</span></span>
<span data-ttu-id="42091-234">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="42091-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="42091-235">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="42091-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="42091-236">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="42091-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="42091-237">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="42091-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="42091-238">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="42091-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="42091-239">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="42091-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="42091-240">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="42091-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="42091-241">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="42091-241">Performance and Tuning</span></span>
<span data-ttu-id="42091-242">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="42091-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42091-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42091-243">Next Steps</span></span>
<span data-ttu-id="42091-244">Consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="42091-244">See hello following articles:</span></span>

* <span data-ttu-id="42091-245">[Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criação de um pipeline com uma Atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="42091-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
