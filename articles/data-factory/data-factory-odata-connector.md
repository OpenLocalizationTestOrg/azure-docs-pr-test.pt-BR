---
title: Mover dados de fontes OData | Microsoft Docs
description: Saiba mais sobre como mover dados de fontes OData usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 624b6c8f317477d83539392c6c2f15c2dc69d401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="66a0e-103">Mover dados De uma origem de OData usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="66a0e-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="66a0e-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de uma origem OData.</span><span class="sxs-lookup"><span data-stu-id="66a0e-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="66a0e-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="66a0e-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="66a0e-106">Você pode copiar dados de uma origem OData para qualquer repositório de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="66a0e-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="66a0e-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="66a0e-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="66a0e-108">Atualmente, o data factory dá suporte apenas para a movimentação de dados de uma origem OData para outros repositórios de dados, mas não para a movimentação de dados de outros repositórios de dados para uma origem OData.</span><span class="sxs-lookup"><span data-stu-id="66a0e-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="66a0e-109">Versões com suporte e tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="66a0e-109">Supported versions and authentication types</span></span>
<span data-ttu-id="66a0e-110">Esse conector OData dá suporte a OData versões 3.0 e 4.0 e você pode copiar dados de OData da nuvem e de fontes OData locais.</span><span class="sxs-lookup"><span data-stu-id="66a0e-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="66a0e-111">Para o último, você precisa instalar o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="66a0e-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="66a0e-112">Consulte o artigo [Mover dados entre local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="66a0e-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="66a0e-113">Os tipos de autenticação abaixo têm suporte:</span><span class="sxs-lookup"><span data-stu-id="66a0e-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="66a0e-114">Para acessar o feed OData da **nuvem**, você poderá usar autenticação anônima, básica (nome de usuário e senha) ou a OAtuth baseada no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="66a0e-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="66a0e-115">Para acessar o feed OData **local**, você poderá usar autenticação anônima, básica (nome de usuário e senha) ou a do Windows.</span><span class="sxs-lookup"><span data-stu-id="66a0e-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="66a0e-116">Introdução</span><span class="sxs-lookup"><span data-stu-id="66a0e-116">Getting started</span></span>
<span data-ttu-id="66a0e-117">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem OData usando ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="66a0e-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="66a0e-118">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="66a0e-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="66a0e-119">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="66a0e-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="66a0e-120">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="66a0e-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="66a0e-121">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="66a0e-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="66a0e-122">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="66a0e-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="66a0e-123">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="66a0e-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="66a0e-124">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="66a0e-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="66a0e-125">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="66a0e-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="66a0e-126">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="66a0e-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="66a0e-127">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="66a0e-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="66a0e-128">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de uma origem OData, confira a seção [Exemplo de JSON: Copiar dados da origem OData para o Blob do Azure](#json-example-copy-data-from-odata-source-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="66a0e-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="66a0e-129">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas a uma origem OData:</span><span class="sxs-lookup"><span data-stu-id="66a0e-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="66a0e-130">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="66a0e-130">Linked Service properties</span></span>
<span data-ttu-id="66a0e-131">A tabela a seguir fornece a descrição para elementos JSON específicos do serviço vinculado do OData.</span><span class="sxs-lookup"><span data-stu-id="66a0e-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="66a0e-132">Propriedade</span><span class="sxs-lookup"><span data-stu-id="66a0e-132">Property</span></span> | <span data-ttu-id="66a0e-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="66a0e-133">Description</span></span> | <span data-ttu-id="66a0e-134">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="66a0e-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66a0e-135">type</span><span class="sxs-lookup"><span data-stu-id="66a0e-135">type</span></span> |<span data-ttu-id="66a0e-136">A propriedade de tipo deve ser definida como: **OData**</span><span class="sxs-lookup"><span data-stu-id="66a0e-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="66a0e-137">Sim</span><span class="sxs-lookup"><span data-stu-id="66a0e-137">Yes</span></span> |
| <span data-ttu-id="66a0e-138">URL</span><span class="sxs-lookup"><span data-stu-id="66a0e-138">url</span></span> |<span data-ttu-id="66a0e-139">URL do serviço OData.</span><span class="sxs-lookup"><span data-stu-id="66a0e-139">Url of the OData service.</span></span> |<span data-ttu-id="66a0e-140">Sim</span><span class="sxs-lookup"><span data-stu-id="66a0e-140">Yes</span></span> |
| <span data-ttu-id="66a0e-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="66a0e-141">authenticationType</span></span> |<span data-ttu-id="66a0e-142">Tipo de autenticação usada para se conectar ao armazenamento de dados OData.</span><span class="sxs-lookup"><span data-stu-id="66a0e-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="66a0e-143">Para o OData de nuvem, os valores possíveis são Anônimo, Básico e OAuth (observe que o Azure Data Factory dá suporte no momento apenas a OAuth baseado no Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="66a0e-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="66a0e-144">Para OData local, os valores possíveis são Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="66a0e-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="66a0e-145">Sim</span><span class="sxs-lookup"><span data-stu-id="66a0e-145">Yes</span></span> |
| <span data-ttu-id="66a0e-146">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="66a0e-146">username</span></span> |<span data-ttu-id="66a0e-147">Especifique o nome de usuário se você estiver usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="66a0e-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="66a0e-148">Sim (apenas se você estiver usando a autenticação Básica)</span><span class="sxs-lookup"><span data-stu-id="66a0e-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="66a0e-149">Senha</span><span class="sxs-lookup"><span data-stu-id="66a0e-149">password</span></span> |<span data-ttu-id="66a0e-150">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="66a0e-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="66a0e-151">Sim (apenas se você estiver usando a autenticação Básica)</span><span class="sxs-lookup"><span data-stu-id="66a0e-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="66a0e-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="66a0e-152">authorizedCredential</span></span> |<span data-ttu-id="66a0e-153">Se você estiver usando OAuth, clique no botão **Autorizar** no Editor ou Assistente de Cópia do Data Factory e digite suas credenciais. O valor dessa propriedade será gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="66a0e-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="66a0e-154">Sim (apenas se você estiver usando a autenticação OAuth)</span><span class="sxs-lookup"><span data-stu-id="66a0e-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="66a0e-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="66a0e-155">gatewayName</span></span> |<span data-ttu-id="66a0e-156">O nome do gateway que o serviço Data Factory deve usar para se conectar ao serviço OData local.</span><span class="sxs-lookup"><span data-stu-id="66a0e-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="66a0e-157">Só especifique se você estiver copiando dados da fonte OData local.</span><span class="sxs-lookup"><span data-stu-id="66a0e-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="66a0e-158">Não</span><span class="sxs-lookup"><span data-stu-id="66a0e-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="66a0e-159">Usando a autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="66a0e-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="66a0e-160">Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="66a0e-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="66a0e-161">Usando a autenticação do Windows para acessar uma fonte OData local</span><span class="sxs-lookup"><span data-stu-id="66a0e-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="66a0e-162">Usando autenticação OAuth para acessar a fonte OData da nuvem</span><span class="sxs-lookup"><span data-stu-id="66a0e-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="66a0e-163">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="66a0e-163">Dataset properties</span></span>
<span data-ttu-id="66a0e-164">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="66a0e-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="66a0e-165">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="66a0e-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="66a0e-166">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="66a0e-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="66a0e-167">A seção typeProperties do conjunto de dados do tipo **ODataResource** (que inclui o conjunto de dados do OData) tem as propriedades a seguir</span><span class="sxs-lookup"><span data-stu-id="66a0e-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="66a0e-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="66a0e-168">Property</span></span> | <span data-ttu-id="66a0e-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="66a0e-169">Description</span></span> | <span data-ttu-id="66a0e-170">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="66a0e-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="66a0e-171">caminho</span><span class="sxs-lookup"><span data-stu-id="66a0e-171">path</span></span> |<span data-ttu-id="66a0e-172">Caminho para o recurso OData</span><span class="sxs-lookup"><span data-stu-id="66a0e-172">Path to the OData resource</span></span> |<span data-ttu-id="66a0e-173">Não</span><span class="sxs-lookup"><span data-stu-id="66a0e-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="66a0e-174">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="66a0e-174">Copy activity properties</span></span>
<span data-ttu-id="66a0e-175">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="66a0e-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="66a0e-176">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="66a0e-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="66a0e-177">As propriedades disponíveis na seção typeProperties da atividade, por outro lado, variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="66a0e-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="66a0e-178">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="66a0e-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="66a0e-179">Quando a fonte é do tipo **RelationalSource** (que inclui o OData), as seguintes propriedades estão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="66a0e-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="66a0e-180">Propriedade</span><span class="sxs-lookup"><span data-stu-id="66a0e-180">Property</span></span> | <span data-ttu-id="66a0e-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="66a0e-181">Description</span></span> | <span data-ttu-id="66a0e-182">Exemplo</span><span class="sxs-lookup"><span data-stu-id="66a0e-182">Example</span></span> | <span data-ttu-id="66a0e-183">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="66a0e-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="66a0e-184">query</span><span class="sxs-lookup"><span data-stu-id="66a0e-184">query</span></span> |<span data-ttu-id="66a0e-185">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="66a0e-185">Use the custom query to read data.</span></span> |<span data-ttu-id="66a0e-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="66a0e-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="66a0e-187">Não</span><span class="sxs-lookup"><span data-stu-id="66a0e-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="66a0e-188">Mapeamento de tipos para OData</span><span class="sxs-lookup"><span data-stu-id="66a0e-188">Type Mapping for OData</span></span>
<span data-ttu-id="66a0e-189">Como mencionado no artigo sobre as [atividades de movimentação de dados](data-factory-data-movement-activities.md) , a atividade de Cópia executa conversões automáticas dos tipos de fonte nos tipos de coletor com a seguinte abordagem de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="66a0e-189">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="66a0e-190">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="66a0e-190">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="66a0e-191">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="66a0e-191">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="66a0e-192">Ao mover dados do OData, os seguintes mapeamentos serão usados dos tipos do OData para os tipos do .NET.</span><span class="sxs-lookup"><span data-stu-id="66a0e-192">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="66a0e-193">Tipo de dados OData</span><span class="sxs-lookup"><span data-stu-id="66a0e-193">OData Data Type</span></span> | <span data-ttu-id="66a0e-194">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="66a0e-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="66a0e-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="66a0e-195">Edm.Binary</span></span> |<span data-ttu-id="66a0e-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="66a0e-196">Byte[]</span></span> |
| <span data-ttu-id="66a0e-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="66a0e-197">Edm.Boolean</span></span> |<span data-ttu-id="66a0e-198">Bool</span><span class="sxs-lookup"><span data-stu-id="66a0e-198">Bool</span></span> |
| <span data-ttu-id="66a0e-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="66a0e-199">Edm.Byte</span></span> |<span data-ttu-id="66a0e-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="66a0e-200">Byte[]</span></span> |
| <span data-ttu-id="66a0e-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="66a0e-201">Edm.DateTime</span></span> |<span data-ttu-id="66a0e-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="66a0e-202">DateTime</span></span> |
| <span data-ttu-id="66a0e-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="66a0e-203">Edm.Decimal</span></span> |<span data-ttu-id="66a0e-204">Decimal</span><span class="sxs-lookup"><span data-stu-id="66a0e-204">Decimal</span></span> |
| <span data-ttu-id="66a0e-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="66a0e-205">Edm.Double</span></span> |<span data-ttu-id="66a0e-206">Duplo</span><span class="sxs-lookup"><span data-stu-id="66a0e-206">Double</span></span> |
| <span data-ttu-id="66a0e-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="66a0e-207">Edm.Single</span></span> |<span data-ttu-id="66a0e-208">Single</span><span class="sxs-lookup"><span data-stu-id="66a0e-208">Single</span></span> |
| <span data-ttu-id="66a0e-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="66a0e-209">Edm.Guid</span></span> |<span data-ttu-id="66a0e-210">Guid</span><span class="sxs-lookup"><span data-stu-id="66a0e-210">Guid</span></span> |
| <span data-ttu-id="66a0e-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="66a0e-211">Edm.Int16</span></span> |<span data-ttu-id="66a0e-212">Int16</span><span class="sxs-lookup"><span data-stu-id="66a0e-212">Int16</span></span> |
| <span data-ttu-id="66a0e-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="66a0e-213">Edm.Int32</span></span> |<span data-ttu-id="66a0e-214">Int32</span><span class="sxs-lookup"><span data-stu-id="66a0e-214">Int32</span></span> |
| <span data-ttu-id="66a0e-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="66a0e-215">Edm.Int64</span></span> |<span data-ttu-id="66a0e-216">Int64</span><span class="sxs-lookup"><span data-stu-id="66a0e-216">Int64</span></span> |
| <span data-ttu-id="66a0e-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="66a0e-217">Edm.SByte</span></span> |<span data-ttu-id="66a0e-218">Int16</span><span class="sxs-lookup"><span data-stu-id="66a0e-218">Int16</span></span> |
| <span data-ttu-id="66a0e-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="66a0e-219">Edm.String</span></span> |<span data-ttu-id="66a0e-220">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="66a0e-220">String</span></span> |
| <span data-ttu-id="66a0e-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="66a0e-221">Edm.Time</span></span> |<span data-ttu-id="66a0e-222">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="66a0e-222">TimeSpan</span></span> |
| <span data-ttu-id="66a0e-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="66a0e-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="66a0e-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="66a0e-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="66a0e-225">Tipos de dados complexos do OData, por exemplo, o objeto não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="66a0e-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="66a0e-226">Exemplo de JSON: copiar dados da origem do OData para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="66a0e-226">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="66a0e-227">Este exemplo fornece as definições de JSON de exemplo que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="66a0e-227">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="66a0e-228">Eles mostram como copiar dados de uma fonte OData para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="66a0e-228">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="66a0e-229">No entanto, os dados podem ser copiados para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="66a0e-229">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="66a0e-230">O exemplo tem as seguintes entidades do Data Factory:</span><span class="sxs-lookup"><span data-stu-id="66a0e-230">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="66a0e-231">Um serviço vinculado do tipo [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="66a0e-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="66a0e-232">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="66a0e-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="66a0e-233">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="66a0e-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="66a0e-234">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="66a0e-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="66a0e-235">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="66a0e-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="66a0e-236">O exemplo copia dados de consulta em relação a uma fonte OData para um blob do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="66a0e-236">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="66a0e-237">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="66a0e-237">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="66a0e-238">**Serviço vinculado ao OData** Esse exemplo usa a autenticação Anônima.</span><span class="sxs-lookup"><span data-stu-id="66a0e-238">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="66a0e-239">Consulte a seção [Serviço vinculado a OData](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="66a0e-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="66a0e-240">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="66a0e-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="66a0e-241">**Conjunto de dados de entrada do OData:**</span><span class="sxs-lookup"><span data-stu-id="66a0e-241">**OData input dataset:**</span></span>

<span data-ttu-id="66a0e-242">Configurar “external”: “true” informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="66a0e-242">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="66a0e-243">A especificação do **caminho** na definição do conjunto de dados é opcional.</span><span class="sxs-lookup"><span data-stu-id="66a0e-243">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="66a0e-244">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="66a0e-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="66a0e-245">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="66a0e-245">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="66a0e-246">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="66a0e-246">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="66a0e-247">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="66a0e-247">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="66a0e-248">**Atividade de cópia em um pipeline com origem OData e coletor Blob:**</span><span class="sxs-lookup"><span data-stu-id="66a0e-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="66a0e-249">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="66a0e-249">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="66a0e-250">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="66a0e-250">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="66a0e-251">A consulta SQL especificada para a propriedade **consulta** seleciona os dados mais recentes (mais novos) da fonte de OData.</span><span class="sxs-lookup"><span data-stu-id="66a0e-251">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="66a0e-252">A especificação da **consulta** na definição do pipeline é opcional.</span><span class="sxs-lookup"><span data-stu-id="66a0e-252">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="66a0e-253">A **URL** que o serviço do Data Factory usa para recuperar dados é: a URL especificada no serviço vinculado (obrigatória) + caminho especificado no conjunto de dados (opcional) + consulta no pipeline (opcional).</span><span class="sxs-lookup"><span data-stu-id="66a0e-253">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="66a0e-254">Mapeamento de tipos para OData</span><span class="sxs-lookup"><span data-stu-id="66a0e-254">Type mapping for OData</span></span>
<span data-ttu-id="66a0e-255">Como mencionado no artigo sobre as [Atividades de Movimentação de Dados](data-factory-data-movement-activities.md) , a atividade de Cópia executa conversões automáticas dos tipos de fonte nos tipos de coletor com a seguinte abordagem de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="66a0e-255">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="66a0e-256">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="66a0e-256">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="66a0e-257">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="66a0e-257">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="66a0e-258">Ao mover dados de repositórios de dados OData, os tipos de dados OData são mapeados para tipos .NET.</span><span class="sxs-lookup"><span data-stu-id="66a0e-258">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="66a0e-259">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="66a0e-259">Map source to sink columns</span></span>
<span data-ttu-id="66a0e-260">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="66a0e-260">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="66a0e-261">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="66a0e-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="66a0e-262">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="66a0e-262">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="66a0e-263">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="66a0e-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="66a0e-264">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="66a0e-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="66a0e-265">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="66a0e-265">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="66a0e-266">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="66a0e-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="66a0e-267">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="66a0e-267">Performance and Tuning</span></span>
<span data-ttu-id="66a0e-268">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="66a0e-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
