---
title: aaaMove dados de fontes de OData | Microsoft Docs
description: "Saiba mais sobre como toomove de OData – fontes de dados usando o Azure Data Factory."
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
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="21c5d-103">Mover dados De uma origem de OData usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="21c5d-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="21c5d-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de uma fonte OData.</span><span class="sxs-lookup"><span data-stu-id="21c5d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="21c5d-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="21c5d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="21c5d-106">Você pode copiar dados de um repositório de dados OData source tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="21c5d-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="21c5d-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="21c5d-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="21c5d-108">Fábrica de dados atualmente suporta apenas mover armazena dados de um banco de dados fonte tooother do OData, mas não para mover dados de outros dados armazena tooan OData source.</span><span class="sxs-lookup"><span data-stu-id="21c5d-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="21c5d-109">Versões com suporte e tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="21c5d-109">Supported versions and authentication types</span></span>
<span data-ttu-id="21c5d-110">Esse conector OData dá suporte a OData versões 3.0 e 4.0 e você pode copiar dados de OData da nuvem e de fontes OData locais.</span><span class="sxs-lookup"><span data-stu-id="21c5d-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="21c5d-111">Para Olá último, você precisa tooinstall Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="21c5d-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="21c5d-112">Consulte o artigo [Mover dados entre local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="21c5d-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="21c5d-113">Os tipos de autenticação abaixo têm suporte:</span><span class="sxs-lookup"><span data-stu-id="21c5d-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="21c5d-114">tooaccess **nuvem** feed OData, você pode usar anônima, básica (nome de usuário e senha) ou o Active Directory do Azure com base em autenticação OAuth.</span><span class="sxs-lookup"><span data-stu-id="21c5d-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="21c5d-115">tooaccess **local** feed OData, você pode usar anônima, básica (nome de usuário e senha) ou autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="21c5d-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="21c5d-116">Introdução</span><span class="sxs-lookup"><span data-stu-id="21c5d-116">Getting started</span></span>
<span data-ttu-id="21c5d-117">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem OData usando ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="21c5d-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="21c5d-118">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="21c5d-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="21c5d-119">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="21c5d-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="21c5d-120">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="21c5d-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="21c5d-121">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="21c5d-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="21c5d-122">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="21c5d-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="21c5d-123">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="21c5d-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="21c5d-124">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="21c5d-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="21c5d-125">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="21c5d-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="21c5d-126">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="21c5d-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="21c5d-127">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="21c5d-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="21c5d-128">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de uma fonte OData, consulte [exemplo JSON: copiar dados de OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="21c5d-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="21c5d-129">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específicas tooOData origem:</span><span class="sxs-lookup"><span data-stu-id="21c5d-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="21c5d-130">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="21c5d-130">Linked Service properties</span></span>
<span data-ttu-id="21c5d-131">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooOData vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="21c5d-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="21c5d-132">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21c5d-132">Property</span></span> | <span data-ttu-id="21c5d-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="21c5d-133">Description</span></span> | <span data-ttu-id="21c5d-134">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="21c5d-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21c5d-135">type</span><span class="sxs-lookup"><span data-stu-id="21c5d-135">type</span></span> |<span data-ttu-id="21c5d-136">propriedade de tipo Hello deve ser definida como: **OData**</span><span class="sxs-lookup"><span data-stu-id="21c5d-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="21c5d-137">Sim</span><span class="sxs-lookup"><span data-stu-id="21c5d-137">Yes</span></span> |
| <span data-ttu-id="21c5d-138">url</span><span class="sxs-lookup"><span data-stu-id="21c5d-138">url</span></span> |<span data-ttu-id="21c5d-139">URL da saudação serviço OData.</span><span class="sxs-lookup"><span data-stu-id="21c5d-139">Url of hello OData service.</span></span> |<span data-ttu-id="21c5d-140">Sim</span><span class="sxs-lookup"><span data-stu-id="21c5d-140">Yes</span></span> |
| <span data-ttu-id="21c5d-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="21c5d-141">authenticationType</span></span> |<span data-ttu-id="21c5d-142">Tipo de autenticação usado tooconnect toohello OData source.</span><span class="sxs-lookup"><span data-stu-id="21c5d-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="21c5d-143">Para o OData de nuvem, os valores possíveis são Anônimo, Básico e OAuth (observe que o Azure Data Factory dá suporte no momento apenas a OAuth baseado no Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="21c5d-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="21c5d-144">Para OData local, os valores possíveis são Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="21c5d-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="21c5d-145">Sim</span><span class="sxs-lookup"><span data-stu-id="21c5d-145">Yes</span></span> |
| <span data-ttu-id="21c5d-146">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="21c5d-146">username</span></span> |<span data-ttu-id="21c5d-147">Especifique o nome de usuário se você estiver usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="21c5d-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="21c5d-148">Sim (apenas se você estiver usando a autenticação Básica)</span><span class="sxs-lookup"><span data-stu-id="21c5d-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="21c5d-149">Senha</span><span class="sxs-lookup"><span data-stu-id="21c5d-149">password</span></span> |<span data-ttu-id="21c5d-150">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="21c5d-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="21c5d-151">Sim (apenas se você estiver usando a autenticação Básica)</span><span class="sxs-lookup"><span data-stu-id="21c5d-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="21c5d-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="21c5d-152">authorizedCredential</span></span> |<span data-ttu-id="21c5d-153">Se você estiver usando o OAuth, clique em **autorizar** botão no hello Assistente para cópia de fábrica de dados ou no Editor e insira suas credenciais, valor Olá dessa propriedade será gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="21c5d-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="21c5d-154">Sim (apenas se você estiver usando a autenticação OAuth)</span><span class="sxs-lookup"><span data-stu-id="21c5d-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="21c5d-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="21c5d-155">gatewayName</span></span> |<span data-ttu-id="21c5d-156">Nome do gateway Olá Olá serviço da fábrica de dados deve usar um serviço OData do tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="21c5d-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="21c5d-157">Só especifique se você estiver copiando dados da fonte OData local.</span><span class="sxs-lookup"><span data-stu-id="21c5d-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="21c5d-158">Não</span><span class="sxs-lookup"><span data-stu-id="21c5d-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="21c5d-159">Usando a autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="21c5d-159">Using Basic authentication</span></span>
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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="21c5d-160">Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="21c5d-160">Using Anonymous authentication</span></span>
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

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="21c5d-161">Usando a autenticação do Windows para acessar uma fonte OData local</span><span class="sxs-lookup"><span data-stu-id="21c5d-161">Using Windows authentication accessing on-premises OData source</span></span>
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

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="21c5d-162">Usando autenticação OAuth para acessar a fonte OData da nuvem</span><span class="sxs-lookup"><span data-stu-id="21c5d-162">Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="21c5d-163">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="21c5d-163">Dataset properties</span></span>
<span data-ttu-id="21c5d-164">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="21c5d-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="21c5d-165">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="21c5d-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="21c5d-166">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="21c5d-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="21c5d-167">Olá typeProperties seção de conjunto de dados do tipo **ODataResource** (que inclui o conjunto de dados OData) tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="21c5d-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="21c5d-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21c5d-168">Property</span></span> | <span data-ttu-id="21c5d-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="21c5d-169">Description</span></span> | <span data-ttu-id="21c5d-170">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="21c5d-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21c5d-171">path</span><span class="sxs-lookup"><span data-stu-id="21c5d-171">path</span></span> |<span data-ttu-id="21c5d-172">Caminho toohello recurso do OData</span><span class="sxs-lookup"><span data-stu-id="21c5d-172">Path toohello OData resource</span></span> |<span data-ttu-id="21c5d-173">Não</span><span class="sxs-lookup"><span data-stu-id="21c5d-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="21c5d-174">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="21c5d-174">Copy activity properties</span></span>
<span data-ttu-id="21c5d-175">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="21c5d-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="21c5d-176">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="21c5d-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="21c5d-177">Propriedades disponíveis na seção de typeProperties Olá de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="21c5d-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="21c5d-178">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="21c5d-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="21c5d-179">Quando a fonte é do tipo **RelationalSource** (que inclui OData) Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="21c5d-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="21c5d-180">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21c5d-180">Property</span></span> | <span data-ttu-id="21c5d-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="21c5d-181">Description</span></span> | <span data-ttu-id="21c5d-182">Exemplo</span><span class="sxs-lookup"><span data-stu-id="21c5d-182">Example</span></span> | <span data-ttu-id="21c5d-183">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="21c5d-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21c5d-184">query</span><span class="sxs-lookup"><span data-stu-id="21c5d-184">query</span></span> |<span data-ttu-id="21c5d-185">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="21c5d-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="21c5d-186">"?$select=Name, Description&$top=5"</span><span class="sxs-lookup"><span data-stu-id="21c5d-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="21c5d-187">Não</span><span class="sxs-lookup"><span data-stu-id="21c5d-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="21c5d-188">Mapeamento de tipos para OData</span><span class="sxs-lookup"><span data-stu-id="21c5d-188">Type Mapping for OData</span></span>
<span data-ttu-id="21c5d-189">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="21c5d-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="21c5d-190">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="21c5d-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="21c5d-191">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="21c5d-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="21c5d-192">Ao mover dados do OData, hello mapeamentos a seguir são usados de tipo de too.NET de tipos do OData.</span><span class="sxs-lookup"><span data-stu-id="21c5d-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="21c5d-193">Tipo de dados OData</span><span class="sxs-lookup"><span data-stu-id="21c5d-193">OData Data Type</span></span> | <span data-ttu-id="21c5d-194">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="21c5d-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="21c5d-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="21c5d-195">Edm.Binary</span></span> |<span data-ttu-id="21c5d-196">Byte[]</span><span class="sxs-lookup"><span data-stu-id="21c5d-196">Byte[]</span></span> |
| <span data-ttu-id="21c5d-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="21c5d-197">Edm.Boolean</span></span> |<span data-ttu-id="21c5d-198">Bool</span><span class="sxs-lookup"><span data-stu-id="21c5d-198">Bool</span></span> |
| <span data-ttu-id="21c5d-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="21c5d-199">Edm.Byte</span></span> |<span data-ttu-id="21c5d-200">Byte[]</span><span class="sxs-lookup"><span data-stu-id="21c5d-200">Byte[]</span></span> |
| <span data-ttu-id="21c5d-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="21c5d-201">Edm.DateTime</span></span> |<span data-ttu-id="21c5d-202">DateTime</span><span class="sxs-lookup"><span data-stu-id="21c5d-202">DateTime</span></span> |
| <span data-ttu-id="21c5d-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="21c5d-203">Edm.Decimal</span></span> |<span data-ttu-id="21c5d-204">Decimal</span><span class="sxs-lookup"><span data-stu-id="21c5d-204">Decimal</span></span> |
| <span data-ttu-id="21c5d-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="21c5d-205">Edm.Double</span></span> |<span data-ttu-id="21c5d-206">Duplo</span><span class="sxs-lookup"><span data-stu-id="21c5d-206">Double</span></span> |
| <span data-ttu-id="21c5d-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="21c5d-207">Edm.Single</span></span> |<span data-ttu-id="21c5d-208">Single</span><span class="sxs-lookup"><span data-stu-id="21c5d-208">Single</span></span> |
| <span data-ttu-id="21c5d-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="21c5d-209">Edm.Guid</span></span> |<span data-ttu-id="21c5d-210">Guid</span><span class="sxs-lookup"><span data-stu-id="21c5d-210">Guid</span></span> |
| <span data-ttu-id="21c5d-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="21c5d-211">Edm.Int16</span></span> |<span data-ttu-id="21c5d-212">Int16</span><span class="sxs-lookup"><span data-stu-id="21c5d-212">Int16</span></span> |
| <span data-ttu-id="21c5d-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="21c5d-213">Edm.Int32</span></span> |<span data-ttu-id="21c5d-214">Int32</span><span class="sxs-lookup"><span data-stu-id="21c5d-214">Int32</span></span> |
| <span data-ttu-id="21c5d-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="21c5d-215">Edm.Int64</span></span> |<span data-ttu-id="21c5d-216">Int64</span><span class="sxs-lookup"><span data-stu-id="21c5d-216">Int64</span></span> |
| <span data-ttu-id="21c5d-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="21c5d-217">Edm.SByte</span></span> |<span data-ttu-id="21c5d-218">Int16</span><span class="sxs-lookup"><span data-stu-id="21c5d-218">Int16</span></span> |
| <span data-ttu-id="21c5d-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="21c5d-219">Edm.String</span></span> |<span data-ttu-id="21c5d-220">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21c5d-220">String</span></span> |
| <span data-ttu-id="21c5d-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="21c5d-221">Edm.Time</span></span> |<span data-ttu-id="21c5d-222">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21c5d-222">TimeSpan</span></span> |
| <span data-ttu-id="21c5d-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="21c5d-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="21c5d-224">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="21c5d-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="21c5d-225">Tipos de dados complexos do OData, por exemplo, o objeto não tem suporte.</span><span class="sxs-lookup"><span data-stu-id="21c5d-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="21c5d-226">Exemplo JSON: copiar dados de OData source tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="21c5d-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="21c5d-227">Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="21c5d-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="21c5d-228">Eles mostram como fonte de dados toocopy do OData tooan armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="21c5d-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="21c5d-229">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="21c5d-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="21c5d-230">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="21c5d-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="21c5d-231">Um serviço vinculado do tipo [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="21c5d-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="21c5d-232">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="21c5d-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="21c5d-233">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="21c5d-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="21c5d-234">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="21c5d-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="21c5d-235">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="21c5d-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="21c5d-236">exemplo Hello copia dados de consulta em um tooan de origem OData BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="21c5d-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="21c5d-237">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="21c5d-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="21c5d-238">**Serviço vinculado do OData:** Este exemplo usa Olá autenticação anônima.</span><span class="sxs-lookup"><span data-stu-id="21c5d-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="21c5d-239">Consulte a seção [Serviço vinculado a OData](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="21c5d-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="21c5d-240">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="21c5d-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="21c5d-241">**Conjunto de dados de entrada do OData:**</span><span class="sxs-lookup"><span data-stu-id="21c5d-241">**OData input dataset:**</span></span>

<span data-ttu-id="21c5d-242">Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="21c5d-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="21c5d-243">Especificando **caminho** no conjunto de dados Olá definição é opcional.</span><span class="sxs-lookup"><span data-stu-id="21c5d-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="21c5d-244">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="21c5d-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="21c5d-245">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="21c5d-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="21c5d-246">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="21c5d-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="21c5d-247">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="21c5d-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="21c5d-248">**Atividade de cópia em um pipeline com origem OData e coletor Blob:**</span><span class="sxs-lookup"><span data-stu-id="21c5d-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="21c5d-249">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="21c5d-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="21c5d-250">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="21c5d-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="21c5d-251">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados (mais recentes) mais recentes de saudação da origem do OData hello.</span><span class="sxs-lookup"><span data-stu-id="21c5d-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

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

<span data-ttu-id="21c5d-252">Especificando **consulta** no pipeline de saudação definição é opcional.</span><span class="sxs-lookup"><span data-stu-id="21c5d-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="21c5d-253">Olá **URL** é que o serviço de fábrica de dados de saudação usa dados tooretrieve: URL especificado no hello serviço vinculado (obrigatório) + no caminho especificado no conjunto de dados de saudação (opcional) + consulta no pipeline de saudação (opcional).</span><span class="sxs-lookup"><span data-stu-id="21c5d-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="21c5d-254">Mapeamento de tipos para OData</span><span class="sxs-lookup"><span data-stu-id="21c5d-254">Type mapping for OData</span></span>
<span data-ttu-id="21c5d-255">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="21c5d-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="21c5d-256">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="21c5d-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="21c5d-257">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="21c5d-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="21c5d-258">Ao mover dados de armazenamentos de dados OData, tipos de dados OData são tipos de too.NET mapeada.</span><span class="sxs-lookup"><span data-stu-id="21c5d-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="21c5d-259">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="21c5d-259">Map source toosink columns</span></span>
<span data-ttu-id="21c5d-260">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="21c5d-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="21c5d-261">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="21c5d-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="21c5d-262">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="21c5d-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="21c5d-263">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="21c5d-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="21c5d-264">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="21c5d-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="21c5d-265">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="21c5d-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="21c5d-266">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="21c5d-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="21c5d-267">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="21c5d-267">Performance and Tuning</span></span>
<span data-ttu-id="21c5d-268">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="21c5d-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
