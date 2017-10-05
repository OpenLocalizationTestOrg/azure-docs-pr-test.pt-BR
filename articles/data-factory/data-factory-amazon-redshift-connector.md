---
title: Mover dados do Amazon Redshift usando o Data Factory | Microsoft Docs
description: Saiba mais sobre como mover dados do Amazon Redshift usando o Azure Data Factory.
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
ms.openlocfilehash: bccb941363952bb2251629240a88148a6527d62e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="be3df-103">Mover dados do Amazon Redshift usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="be3df-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="be3df-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados do Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="be3df-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from Amazon Redshift.</span></span> <span data-ttu-id="be3df-105">O artigo se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="be3df-105">The article builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="be3df-106">Você pode copiar dados do Amazon Redshift para qualquer repositório de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="be3df-106">You can copy data from Amazon Redshift to any supported sink data store.</span></span> <span data-ttu-id="be3df-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="be3df-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="be3df-108">Atualmente, a data factory dá suporte para a movimentação de dados do Amazon Redshift para outros armazenamentos de dados, mas não para a movimentação de dados de outros armazenamentos de dados para o Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="be3df-108">Data factory currently supports moving data from Amazon Redshift to other data stores, but not for moving data from other data stores to Amazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be3df-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="be3df-109">Prerequisites</span></span>
* <span data-ttu-id="be3df-110">Se estiver movendo dados para um repositório de dados local, instale o [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) em um computador local.</span><span class="sxs-lookup"><span data-stu-id="be3df-110">If you are moving data to an on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="be3df-111">Em seguida, conceda ao Gateway de Gerenciamento de Dados (use o endereço IP do computador) acesso ao cluster do Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="be3df-111">Then, Grant Data Management Gateway (use IP address of the machine) the access to Amazon Redshift cluster.</span></span> <span data-ttu-id="be3df-112">Veja [Autorizar o acesso ao cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="be3df-112">See [Authorize access to the cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="be3df-113">Se você estiver movendo dados para um armazenamento de dados do Azure, veja [Intervalos de IP do Azure Data Center](https://www.microsoft.com/download/details.aspx?id=41653) para os intervalos de endereços IP de computação e SQL usados pelos data centers do Azure.</span><span class="sxs-lookup"><span data-stu-id="be3df-113">If you are moving data to an Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for the Compute IP address and SQL ranges used by the Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="be3df-114">Introdução</span><span class="sxs-lookup"><span data-stu-id="be3df-114">Getting started</span></span>
<span data-ttu-id="be3df-115">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem do Amazon Redshift usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="be3df-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="be3df-116">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="be3df-116">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="be3df-117">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="be3df-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="be3df-118">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="be3df-118">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="be3df-119">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="be3df-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="be3df-120">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="be3df-120">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="be3df-121">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="be3df-121">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="be3df-122">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="be3df-122">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="be3df-123">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="be3df-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="be3df-124">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="be3df-124">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="be3df-125">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="be3df-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="be3df-126">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um repositório de dados do Amazon Redshift, confira a seção [Exemplo de JSON: Copiar dados do Amazon Redshift para o Blob do Azure](#json-example-copy-data-from-amazon-redshift-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="be3df-126">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift to Azure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="be3df-127">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao Amazon Redshift:</span><span class="sxs-lookup"><span data-stu-id="be3df-127">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="be3df-128">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="be3df-128">Linked service properties</span></span>
<span data-ttu-id="be3df-129">A tabela a seguir fornece a descrição para elementos JSON específicas para o serviço vinculado do Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="be3df-129">The following table provides description for JSON elements specific to Amazon Redshift linked service.</span></span>

| <span data-ttu-id="be3df-130">Propriedade</span><span class="sxs-lookup"><span data-stu-id="be3df-130">Property</span></span> | <span data-ttu-id="be3df-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="be3df-131">Description</span></span> | <span data-ttu-id="be3df-132">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="be3df-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="be3df-133">type</span><span class="sxs-lookup"><span data-stu-id="be3df-133">type</span></span> |<span data-ttu-id="be3df-134">A propriedade type deve ser definida como: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="be3df-134">The type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="be3df-135">Sim</span><span class="sxs-lookup"><span data-stu-id="be3df-135">Yes</span></span> |
| <span data-ttu-id="be3df-136">server</span><span class="sxs-lookup"><span data-stu-id="be3df-136">server</span></span> |<span data-ttu-id="be3df-137">Endereço IP ou nome do host do servidor Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="be3df-137">IP address or host name of the Amazon Redshift server.</span></span> |<span data-ttu-id="be3df-138">Sim</span><span class="sxs-lookup"><span data-stu-id="be3df-138">Yes</span></span> |
| <span data-ttu-id="be3df-139">porta</span><span class="sxs-lookup"><span data-stu-id="be3df-139">port</span></span> |<span data-ttu-id="be3df-140">O número da porta TCP usada pelo servidor Amazon Redshift para ouvir conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="be3df-140">The number of the TCP port that the Amazon Redshift server uses to listen for client connections.</span></span> |<span data-ttu-id="be3df-141">Não, valor padrão: 5439</span><span class="sxs-lookup"><span data-stu-id="be3df-141">No, default value: 5439</span></span> |
| <span data-ttu-id="be3df-142">database</span><span class="sxs-lookup"><span data-stu-id="be3df-142">database</span></span> |<span data-ttu-id="be3df-143">Nome do banco de dados do Amazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="be3df-143">Name of the Amazon Redshift database.</span></span> |<span data-ttu-id="be3df-144">Sim</span><span class="sxs-lookup"><span data-stu-id="be3df-144">Yes</span></span> |
| <span data-ttu-id="be3df-145">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="be3df-145">username</span></span> |<span data-ttu-id="be3df-146">Nome de usuário que tem acesso ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="be3df-146">Name of user who has access to the database.</span></span> |<span data-ttu-id="be3df-147">Sim</span><span class="sxs-lookup"><span data-stu-id="be3df-147">Yes</span></span> |
| <span data-ttu-id="be3df-148">Senha</span><span class="sxs-lookup"><span data-stu-id="be3df-148">password</span></span> |<span data-ttu-id="be3df-149">Senha para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="be3df-149">Password for the user account.</span></span> |<span data-ttu-id="be3df-150">Sim</span><span class="sxs-lookup"><span data-stu-id="be3df-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="be3df-151">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="be3df-151">Dataset properties</span></span>
<span data-ttu-id="be3df-152">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="be3df-152">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="be3df-153">As seções como structure, availability e policy são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="be3df-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="be3df-154">A seção **typeProperties** é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="be3df-154">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="be3df-155">Ela fornece informações, como o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="be3df-155">It provides information about the location of the data in the data store.</span></span> <span data-ttu-id="be3df-156">A seção typeProperties de um conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados do Amazon Redshift) tem as propriedades a seguir</span><span class="sxs-lookup"><span data-stu-id="be3df-156">The typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has the following properties</span></span>

| <span data-ttu-id="be3df-157">Propriedade</span><span class="sxs-lookup"><span data-stu-id="be3df-157">Property</span></span> | <span data-ttu-id="be3df-158">Descrição</span><span class="sxs-lookup"><span data-stu-id="be3df-158">Description</span></span> | <span data-ttu-id="be3df-159">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="be3df-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="be3df-160">tableName</span><span class="sxs-lookup"><span data-stu-id="be3df-160">tableName</span></span> |<span data-ttu-id="be3df-161">Nome da tabela na instância do banco de dados do Amazon Redshift à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="be3df-161">Name of the table in the Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="be3df-162">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="be3df-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="be3df-163">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="be3df-163">Copy activity properties</span></span>
<span data-ttu-id="be3df-164">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="be3df-164">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="be3df-165">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="be3df-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="be3df-166">Por outro lado, as propriedades disponíveis na seção **typeProperties** da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="be3df-166">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="be3df-167">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="be3df-167">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="be3df-168">Quando a origem da atividade de cópia é do tipo **RelationalSource** (que inclui o Amazon Redshift), as seguintes propriedades estão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="be3df-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="be3df-169">Propriedade</span><span class="sxs-lookup"><span data-stu-id="be3df-169">Property</span></span> | <span data-ttu-id="be3df-170">Descrição</span><span class="sxs-lookup"><span data-stu-id="be3df-170">Description</span></span> | <span data-ttu-id="be3df-171">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="be3df-171">Allowed values</span></span> | <span data-ttu-id="be3df-172">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="be3df-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="be3df-173">query</span><span class="sxs-lookup"><span data-stu-id="be3df-173">query</span></span> |<span data-ttu-id="be3df-174">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="be3df-174">Use the custom query to read data.</span></span> |<span data-ttu-id="be3df-175">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="be3df-175">SQL query string.</span></span> <span data-ttu-id="be3df-176">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="be3df-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="be3df-177">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="be3df-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-to-azure-blob"></a><span data-ttu-id="be3df-178">Exemplo de JSON: Copiar dados do Amazon Redshift para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="be3df-178">JSON example: Copy data from Amazon Redshift to Azure Blob</span></span>
<span data-ttu-id="be3df-179">Este exemplo mostra como copiar dados de um banco de dados Amazon Redshift para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="be3df-179">This sample shows how to copy data from an Amazon Redshift database to an Azure Blob Storage.</span></span> <span data-ttu-id="be3df-180">No entanto, os dados podem ser copiados **diretamente** para qualquer uma das fontes declaradas [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="be3df-180">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="be3df-181">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="be3df-181">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="be3df-182">Um serviço vinculado do tipo [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="be3df-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="be3df-183">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="be3df-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="be3df-184">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="be3df-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="be3df-185">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="be3df-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="be3df-186">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="be3df-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="be3df-187">O exemplo copia dados de um resultado de consulta no Amazon Redshift para um blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="be3df-187">The sample copies data from a query result in Amazon Redshift to a blob every hour.</span></span> <span data-ttu-id="be3df-188">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="be3df-188">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="be3df-189">**Serviço vinculado do Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="be3df-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< The IP address or host name of the Amazon Redshift server >",
            "port": <The number of the TCP port that the Amazon Redshift server uses to listen for client connections.>,
            "database": "<The database name of the Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="be3df-190">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="be3df-190">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="be3df-191">**Conjunto de dados de entrada do Amazon Redshift:**</span><span class="sxs-lookup"><span data-stu-id="be3df-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="be3df-192">A configuração `"external": true` informa o serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="be3df-192">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="be3df-193">Defina essa propriedade como true em um conjunto de dados de entrada que não é produzido por uma atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="be3df-193">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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

<span data-ttu-id="be3df-194">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="be3df-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="be3df-195">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="be3df-195">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="be3df-196">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="be3df-196">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="be3df-197">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="be3df-197">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="be3df-198">**Atividade de cópia em um pipeline com origem Azure Redshift (RelationalSource) e coletor Blob:**</span><span class="sxs-lookup"><span data-stu-id="be3df-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="be3df-199">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="be3df-199">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="be3df-200">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="be3df-200">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="be3df-201">A consulta SQL especificada para a propriedade **query** seleciona os dados na última hora para copiar.</span><span class="sxs-lookup"><span data-stu-id="be3df-201">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="be3df-202">Mapeamento de tipo para o Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="be3df-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="be3df-203">Conforme mencionado no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) , a Atividade de cópia executa conversões automáticas de tipo de fonte para tipos de coletor, com a abordagem em duas etapas descritas a seguir:</span><span class="sxs-lookup"><span data-stu-id="be3df-203">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="be3df-204">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="be3df-204">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="be3df-205">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="be3df-205">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="be3df-206">Ao mover dados para o Amazon Redshift, os seguintes mapeamentos serão usados dos tipos do Amazon Redshift para os tipos do .NET.</span><span class="sxs-lookup"><span data-stu-id="be3df-206">When moving data to Amazon Redshift, the following mappings are used from Amazon Redshift types to .NET types.</span></span>

| <span data-ttu-id="be3df-207">Tipo do Redshift Amazon</span><span class="sxs-lookup"><span data-stu-id="be3df-207">Amazon Redshift Type</span></span> | <span data-ttu-id="be3df-208">Tipo baseado no .NET</span><span class="sxs-lookup"><span data-stu-id="be3df-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="be3df-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="be3df-209">SMALLINT</span></span> |<span data-ttu-id="be3df-210">Int16</span><span class="sxs-lookup"><span data-stu-id="be3df-210">Int16</span></span> |
| <span data-ttu-id="be3df-211">INTEGER</span><span class="sxs-lookup"><span data-stu-id="be3df-211">INTEGER</span></span> |<span data-ttu-id="be3df-212">Int32</span><span class="sxs-lookup"><span data-stu-id="be3df-212">Int32</span></span> |
| <span data-ttu-id="be3df-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="be3df-213">BIGINT</span></span> |<span data-ttu-id="be3df-214">Int64</span><span class="sxs-lookup"><span data-stu-id="be3df-214">Int64</span></span> |
| <span data-ttu-id="be3df-215">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="be3df-215">DECIMAL</span></span> |<span data-ttu-id="be3df-216">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="be3df-216">Decimal</span></span> |
| <span data-ttu-id="be3df-217">REAL</span><span class="sxs-lookup"><span data-stu-id="be3df-217">REAL</span></span> |<span data-ttu-id="be3df-218">Single</span><span class="sxs-lookup"><span data-stu-id="be3df-218">Single</span></span> |
| <span data-ttu-id="be3df-219">DOUBLE PRECISION</span><span class="sxs-lookup"><span data-stu-id="be3df-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="be3df-220">Duplo</span><span class="sxs-lookup"><span data-stu-id="be3df-220">Double</span></span> |
| <span data-ttu-id="be3df-221">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="be3df-221">BOOLEAN</span></span> |<span data-ttu-id="be3df-222">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="be3df-222">String</span></span> |
| <span data-ttu-id="be3df-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="be3df-223">CHAR</span></span> |<span data-ttu-id="be3df-224">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="be3df-224">String</span></span> |
| <span data-ttu-id="be3df-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="be3df-225">VARCHAR</span></span> |<span data-ttu-id="be3df-226">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="be3df-226">String</span></span> |
| <span data-ttu-id="be3df-227">DATE</span><span class="sxs-lookup"><span data-stu-id="be3df-227">DATE</span></span> |<span data-ttu-id="be3df-228">DateTime</span><span class="sxs-lookup"><span data-stu-id="be3df-228">DateTime</span></span> |
| <span data-ttu-id="be3df-229">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="be3df-229">TIMESTAMP</span></span> |<span data-ttu-id="be3df-230">DateTime</span><span class="sxs-lookup"><span data-stu-id="be3df-230">DateTime</span></span> |
| <span data-ttu-id="be3df-231">TEXT</span><span class="sxs-lookup"><span data-stu-id="be3df-231">TEXT</span></span> |<span data-ttu-id="be3df-232">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="be3df-232">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="be3df-233">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="be3df-233">Map source to sink columns</span></span>
<span data-ttu-id="be3df-234">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="be3df-234">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="be3df-235">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="be3df-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="be3df-236">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="be3df-236">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="be3df-237">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="be3df-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="be3df-238">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="be3df-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="be3df-239">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="be3df-239">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="be3df-240">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="be3df-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="be3df-241">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="be3df-241">Performance and Tuning</span></span>
<span data-ttu-id="be3df-242">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="be3df-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be3df-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be3df-243">Next Steps</span></span>
<span data-ttu-id="be3df-244">Confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="be3df-244">See the following articles:</span></span>

* <span data-ttu-id="be3df-245">[Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criação de um pipeline com uma Atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="be3df-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
