---
title: "dados de aaaMove do Salesforce usando a fábrica de dados | Microsoft Docs"
description: Saiba mais sobre como dados de toomove do Salesforce usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="f2356-103">Mover dados do Salesforce usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f2356-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="f2356-104">Este artigo descreve como você pode usar a atividade de cópia em um Azure fábrica toocopy de dados de repositório de dados do Salesforce tooany listado na coluna coletor Olá Olá [suporte para origens e coletores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="f2356-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="f2356-105">Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia e combinações de repositório de dados com suporte.</span><span class="sxs-lookup"><span data-stu-id="f2356-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="f2356-106">A fábrica de dados do Azure atualmente suporta somente a movimentação de dados do Salesforce muito[suporte para armazenamentos de dados do coletor](data-factory-data-movement-activities.md#supported-data-stores-and-formats), mas não oferece suporte a movimentação de dados de outros tooSalesforce de repositórios de dados.</span><span class="sxs-lookup"><span data-stu-id="f2356-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="f2356-107">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="f2356-107">Supported versions</span></span>
<span data-ttu-id="f2356-108">Esse conector dá suporte a saudação seguintes edições do Salesforce: Developer Edition, Professional Edition, Enterprise Edition ou edição ilimitado.</span><span class="sxs-lookup"><span data-stu-id="f2356-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="f2356-109">E ele dá suporte à cópia na produção, da área restrita e do domínio personalizado do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f2356-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2356-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f2356-110">Prerequisites</span></span>
* <span data-ttu-id="f2356-111">A permissão de API deve estar habilitada.</span><span class="sxs-lookup"><span data-stu-id="f2356-111">API permission must be enabled.</span></span> <span data-ttu-id="f2356-112">Consulte [Como habilito o acesso à API no Salesforce por conjunto de permissões?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="f2356-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="f2356-113">toocopy dados de armazenamentos de dados do Salesforce tooon local, você deve ter pelo menos Data Management Gateway 2.0 instalado no seu ambiente local.</span><span class="sxs-lookup"><span data-stu-id="f2356-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="f2356-114">Limites da solicitação Salesforce</span><span class="sxs-lookup"><span data-stu-id="f2356-114">Salesforce request limits</span></span>
<span data-ttu-id="f2356-115">O Salesforce tem limites para o total de solicitações de API e as solicitações simultâneas de API.</span><span class="sxs-lookup"><span data-stu-id="f2356-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="f2356-116">Observe Olá pontos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2356-116">Note hello following points:</span></span>

- <span data-ttu-id="f2356-117">Se o número de saudação de solicitações simultâneas exceder o limite de hello, a limitação ocorre e você verá falhas aleatórias.</span><span class="sxs-lookup"><span data-stu-id="f2356-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="f2356-118">Se o número total de saudação de solicitações excede o limite de hello, Olá conta Salesforce será bloqueado por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="f2356-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="f2356-119">Você também pode receber um erro de "REQUEST_LIMIT_EXCEEDED" hello em ambos os cenários.</span><span class="sxs-lookup"><span data-stu-id="f2356-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="f2356-120">Consulte a seção hello "limites de solicitação de API" hello [limites de desenvolvedor da equipe de vendas](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="f2356-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f2356-121">Introdução</span><span class="sxs-lookup"><span data-stu-id="f2356-121">Getting started</span></span>
<span data-ttu-id="f2356-122">Você pode criar um pipeline com uma atividade de cópia que mova dados do Salesforce usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="f2356-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="f2356-123">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="f2356-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="f2356-124">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="f2356-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="f2356-125">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="f2356-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f2356-126">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="f2356-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f2356-127">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2356-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="f2356-128">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="f2356-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="f2356-129">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="f2356-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="f2356-130">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="f2356-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="f2356-131">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="f2356-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="f2356-132">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2356-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="f2356-133">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados do Salesforce, consulte [exemplo JSON: copiar dados de Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="f2356-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="f2356-134">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooSalesforce:</span><span class="sxs-lookup"><span data-stu-id="f2356-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="f2356-135">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="f2356-135">Linked service properties</span></span>
<span data-ttu-id="f2356-136">Olá a tabela a seguir fornece descrições dos elementos JSON toohello específico do serviço vinculado da equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="f2356-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="f2356-137">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f2356-137">Property</span></span> | <span data-ttu-id="f2356-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="f2356-138">Description</span></span> | <span data-ttu-id="f2356-139">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f2356-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2356-140">type</span><span class="sxs-lookup"><span data-stu-id="f2356-140">type</span></span> |<span data-ttu-id="f2356-141">propriedade de tipo Hello deve ser definida como: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="f2356-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="f2356-142">Sim</span><span class="sxs-lookup"><span data-stu-id="f2356-142">Yes</span></span> |
| <span data-ttu-id="f2356-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="f2356-143">environmentUrl</span></span> | <span data-ttu-id="f2356-144">Especifique a instância de URL da equipe de vendas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2356-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="f2356-145">– O padrão é "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="f2356-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="f2356-146">-toocopy dados de área restrita, especifique "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="f2356-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="f2356-147">-toocopy dados do domínio personalizado, especificar, por exemplo, "https://[domain].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="f2356-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="f2356-148">Não</span><span class="sxs-lookup"><span data-stu-id="f2356-148">No</span></span> |
| <span data-ttu-id="f2356-149">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="f2356-149">username</span></span> |<span data-ttu-id="f2356-150">Especifique um nome de usuário para a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2356-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="f2356-151">Sim</span><span class="sxs-lookup"><span data-stu-id="f2356-151">Yes</span></span> |
| <span data-ttu-id="f2356-152">Senha</span><span class="sxs-lookup"><span data-stu-id="f2356-152">password</span></span> |<span data-ttu-id="f2356-153">Especifique uma senha para a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2356-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="f2356-154">Sim</span><span class="sxs-lookup"><span data-stu-id="f2356-154">Yes</span></span> |
| <span data-ttu-id="f2356-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="f2356-155">securityToken</span></span> |<span data-ttu-id="f2356-156">Especifique um token de segurança para a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2356-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="f2356-157">Consulte [obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obter instruções sobre como tooreset/obter um token de segurança.</span><span class="sxs-lookup"><span data-stu-id="f2356-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="f2356-158">em geral, consulte toolearn sobre tokens de segurança [API de segurança e hello](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="f2356-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="f2356-159">Sim</span><span class="sxs-lookup"><span data-stu-id="f2356-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="f2356-160">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="f2356-160">Dataset properties</span></span>
<span data-ttu-id="f2356-161">Para obter uma lista completa de seções e propriedades que estão disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f2356-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f2356-162">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure e outros).</span><span class="sxs-lookup"><span data-stu-id="f2356-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="f2356-163">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2356-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="f2356-164">Olá typeProperties seção um conjunto de dados do tipo hello **RelationalTable** tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2356-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="f2356-165">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f2356-165">Property</span></span> | <span data-ttu-id="f2356-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="f2356-166">Description</span></span> | <span data-ttu-id="f2356-167">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f2356-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f2356-168">tableName</span><span class="sxs-lookup"><span data-stu-id="f2356-168">tableName</span></span> |<span data-ttu-id="f2356-169">Nome da tabela de saudação na equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="f2356-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="f2356-170">Não (se uma **consulta** de **RelationalSource** for especificada)</span><span class="sxs-lookup"><span data-stu-id="f2356-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f2356-171">parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="f2356-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="f2356-173">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="f2356-173">Copy activity properties</span></span>
<span data-ttu-id="f2356-174">Para obter uma lista completa de seções e propriedades que estão disponíveis para a definição de atividades, consulte Olá [criar pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="f2356-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f2356-175">As propriedades como o nome, descrição, tabelas de entrada e saída, e várias políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="f2356-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="f2356-176">Propriedades de saudação que estão disponíveis em Olá typeProperties seção de atividade hello, Olá outro lado, variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="f2356-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="f2356-177">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="f2356-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="f2356-178">Atividade de cópia, quando a fonte de saudação é do tipo hello **RelationalSource** (que inclui a equipe de vendas), Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="f2356-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="f2356-179">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f2356-179">Property</span></span> | <span data-ttu-id="f2356-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="f2356-180">Description</span></span> | <span data-ttu-id="f2356-181">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="f2356-181">Allowed values</span></span> | <span data-ttu-id="f2356-182">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="f2356-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f2356-183">query</span><span class="sxs-lookup"><span data-stu-id="f2356-183">query</span></span> |<span data-ttu-id="f2356-184">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="f2356-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="f2356-185">Uma consulta SQL-92 ou uma consulta [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="f2356-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="f2356-186">Por exemplo: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="f2356-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="f2356-187">Não (se hello **tableName** de saudação **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="f2356-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="f2356-188">parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="f2356-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="f2356-190">Dicas de consulta</span><span class="sxs-lookup"><span data-stu-id="f2356-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="f2356-191">Recuperando dados usando a cláusula where na coluna DateTime</span><span class="sxs-lookup"><span data-stu-id="f2356-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="f2356-192">Especifique quando a consulta SOQL ou SQL hello, preste atenção toohello diferença de formato de data e hora.</span><span class="sxs-lookup"><span data-stu-id="f2356-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="f2356-193">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f2356-193">For example:</span></span>

* <span data-ttu-id="f2356-194">**Exemplo de SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="f2356-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="f2356-195">**Exemplo de SQL**:</span><span class="sxs-lookup"><span data-stu-id="f2356-195">**SQL sample**:</span></span>
    * <span data-ttu-id="f2356-196">**Usando a consulta de saudação do Assistente de cópia toospecify:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="f2356-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="f2356-197">**Usando JSON editando toospecify Olá consulta (escape char adequadamente):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="f2356-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="f2356-198">Recuperando dados do relatório do Salesforce</span><span class="sxs-lookup"><span data-stu-id="f2356-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="f2356-199">Você pode recuperar dados de relatórios do Salesforce especificando a consulta como `{call "<report name>"}`, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2356-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="f2356-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="f2356-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="f2356-201">Recuperar registros excluídos da lixeira do Salesforce</span><span class="sxs-lookup"><span data-stu-id="f2356-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="f2356-202">tooquery registros de saudação flexíveis excluído da Lixeira do Salesforce, você pode especificar **"IsDeleted = 1"** em sua consulta.</span><span class="sxs-lookup"><span data-stu-id="f2356-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="f2356-203">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f2356-203">For example,</span></span>

* <span data-ttu-id="f2356-204">tooquery somente os registros Olá excluído, especifique "Selecione * de MyTable__c **onde IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="f2356-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="f2356-205">tooquery todos Olá registros incluindo Olá existente e hello excluído, especifique "Selecione * de MyTable__c **onde IsDeleted = 0 ou IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="f2356-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="f2356-206">Exemplo JSON: copiar dados de Salesforce tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="f2356-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="f2356-207">Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f2356-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f2356-208">Eles mostram como dados de toocopy da equipe de vendas tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="f2356-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="f2356-209">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2356-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="f2356-210">Aqui estão os artefatos de fábrica de dados Olá que você precisará de cenário de saudação do toocreate tooimplement.</span><span class="sxs-lookup"><span data-stu-id="f2356-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="f2356-211">seções de saudação que siga a lista de saudação fornecem detalhes sobre essas etapas.</span><span class="sxs-lookup"><span data-stu-id="f2356-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="f2356-212">Um serviço vinculado do tipo hello [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="f2356-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="f2356-213">Um serviço vinculado do tipo hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="f2356-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="f2356-214">Uma entrada [dataset](data-factory-create-datasets.md) do tipo hello [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="f2356-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="f2356-215">Uma saída [dataset](data-factory-create-datasets.md) do tipo hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="f2356-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="f2356-216">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="f2356-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="f2356-217">**Serviço vinculado Salesforce**</span><span class="sxs-lookup"><span data-stu-id="f2356-217">**Salesforce linked service**</span></span>

<span data-ttu-id="f2356-218">Este exemplo usa Olá **Salesforce** serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="f2356-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="f2356-219">Consulte Olá [serviço vinculado do Salesforce](#linked-service-properties) seção de propriedades de saudação que são suportados por esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="f2356-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="f2356-220">Consulte [obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para obter instruções sobre como tooreset/get hello token de segurança.</span><span class="sxs-lookup"><span data-stu-id="f2356-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="f2356-221">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="f2356-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="f2356-222">**Conjunto de dados de entrada do Salesforce**</span><span class="sxs-lookup"><span data-stu-id="f2356-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="f2356-223">Configuração **externo** muito**true** informa o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="f2356-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2356-224">parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="f2356-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="f2356-226">**Conjunto de dados de saída do blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="f2356-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="f2356-227">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="f2356-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="f2356-228">**Pipeline com Atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="f2356-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="f2356-229">Olá, pipeline contém atividade de cópia, o que é configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="f2356-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="f2356-230">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource**e hello **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f2356-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="f2356-231">Consulte [propriedades de tipo RelationalSource](#copy-activity-properties) para lista de saudação de propriedades que são suportados pelo Olá RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="f2356-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> <span data-ttu-id="f2356-232">parte "__c" Olá Olá nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="f2356-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="f2356-234">Mapeamento de tipo para Salesforce</span><span class="sxs-lookup"><span data-stu-id="f2356-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="f2356-235">Tipo Salesforce</span><span class="sxs-lookup"><span data-stu-id="f2356-235">Salesforce type</span></span> | <span data-ttu-id="f2356-236">Tipo baseado no .NET</span><span class="sxs-lookup"><span data-stu-id="f2356-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="f2356-237">Numeração automática</span><span class="sxs-lookup"><span data-stu-id="f2356-237">Auto Number</span></span> |<span data-ttu-id="f2356-238">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-238">String</span></span> |
| <span data-ttu-id="f2356-239">Caixa de seleção</span><span class="sxs-lookup"><span data-stu-id="f2356-239">Checkbox</span></span> |<span data-ttu-id="f2356-240">Booliano</span><span class="sxs-lookup"><span data-stu-id="f2356-240">Boolean</span></span> |
| <span data-ttu-id="f2356-241">Moeda</span><span class="sxs-lookup"><span data-stu-id="f2356-241">Currency</span></span> |<span data-ttu-id="f2356-242">Duplo</span><span class="sxs-lookup"><span data-stu-id="f2356-242">Double</span></span> |
| <span data-ttu-id="f2356-243">Data</span><span class="sxs-lookup"><span data-stu-id="f2356-243">Date</span></span> |<span data-ttu-id="f2356-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="f2356-244">DateTime</span></span> |
| <span data-ttu-id="f2356-245">Data/hora</span><span class="sxs-lookup"><span data-stu-id="f2356-245">Date/Time</span></span> |<span data-ttu-id="f2356-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="f2356-246">DateTime</span></span> |
| <span data-ttu-id="f2356-247">Email</span><span class="sxs-lookup"><span data-stu-id="f2356-247">Email</span></span> |<span data-ttu-id="f2356-248">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-248">String</span></span> |
| <span data-ttu-id="f2356-249">ID</span><span class="sxs-lookup"><span data-stu-id="f2356-249">Id</span></span> |<span data-ttu-id="f2356-250">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-250">String</span></span> |
| <span data-ttu-id="f2356-251">Relação de pesquisa</span><span class="sxs-lookup"><span data-stu-id="f2356-251">Lookup Relationship</span></span> |<span data-ttu-id="f2356-252">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-252">String</span></span> |
| <span data-ttu-id="f2356-253">Lista de seleção múltipla</span><span class="sxs-lookup"><span data-stu-id="f2356-253">Multi-Select Picklist</span></span> |<span data-ttu-id="f2356-254">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-254">String</span></span> |
| <span data-ttu-id="f2356-255">Número</span><span class="sxs-lookup"><span data-stu-id="f2356-255">Number</span></span> |<span data-ttu-id="f2356-256">Duplo</span><span class="sxs-lookup"><span data-stu-id="f2356-256">Double</span></span> |
| <span data-ttu-id="f2356-257">Porcentagem</span><span class="sxs-lookup"><span data-stu-id="f2356-257">Percent</span></span> |<span data-ttu-id="f2356-258">Duplo</span><span class="sxs-lookup"><span data-stu-id="f2356-258">Double</span></span> |
| <span data-ttu-id="f2356-259">Telefone</span><span class="sxs-lookup"><span data-stu-id="f2356-259">Phone</span></span> |<span data-ttu-id="f2356-260">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-260">String</span></span> |
| <span data-ttu-id="f2356-261">Lista de seleção</span><span class="sxs-lookup"><span data-stu-id="f2356-261">Picklist</span></span> |<span data-ttu-id="f2356-262">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-262">String</span></span> |
| <span data-ttu-id="f2356-263">Texto</span><span class="sxs-lookup"><span data-stu-id="f2356-263">Text</span></span> |<span data-ttu-id="f2356-264">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-264">String</span></span> |
| <span data-ttu-id="f2356-265">Área de texto</span><span class="sxs-lookup"><span data-stu-id="f2356-265">Text Area</span></span> |<span data-ttu-id="f2356-266">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-266">String</span></span> |
| <span data-ttu-id="f2356-267">Área de texto (longo)</span><span class="sxs-lookup"><span data-stu-id="f2356-267">Text Area (Long)</span></span> |<span data-ttu-id="f2356-268">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-268">String</span></span> |
| <span data-ttu-id="f2356-269">Área de texto (Rich)</span><span class="sxs-lookup"><span data-stu-id="f2356-269">Text Area (Rich)</span></span> |<span data-ttu-id="f2356-270">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-270">String</span></span> |
| <span data-ttu-id="f2356-271">Texto (criptografado)</span><span class="sxs-lookup"><span data-stu-id="f2356-271">Text (Encrypted)</span></span> |<span data-ttu-id="f2356-272">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-272">String</span></span> |
| <span data-ttu-id="f2356-273">URL</span><span class="sxs-lookup"><span data-stu-id="f2356-273">URL</span></span> |<span data-ttu-id="f2356-274">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="f2356-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="f2356-275">colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f2356-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="f2356-276">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="f2356-276">Performance and tuning</span></span>
<span data-ttu-id="f2356-277">Consulte Olá [atividade de cópia guia de desempenho e ajuste](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="f2356-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
