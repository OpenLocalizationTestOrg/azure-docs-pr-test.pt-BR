---
title: Mover dados do Salesforce usando o Data Factory | Microsoft Docs
description: Saiba mais sobre como mover os dados do Salesforce usando o Azure Data Factory.
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
ms.openlocfilehash: 9390b992bce2dede750c3fc55b7783a6b0db678f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="7024e-103">Mover dados do Salesforce usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7024e-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="7024e-104">Este artigo descreve como você pode usar a Atividade de Cópia no Azure Data Factory para copiar os dados do Salesforce para qualquer armazenamento de dados listado na coluna Coletores tabela de [fontes de dados e coletores com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats) .</span><span class="sxs-lookup"><span data-stu-id="7024e-104">This article outlines how you can use Copy Activity in an Azure data factory to copy data from Salesforce to any data store that is listed under the Sink column in the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="7024e-105">Este artigo se baseia no artigo de [atividades de movimentação de dados](data-factory-data-movement-activities.md) , que apresenta uma visão geral de movimentação de dados com a Atividade de Cópia e combinações de armazenamentos de dados com suporte.</span><span class="sxs-lookup"><span data-stu-id="7024e-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="7024e-106">Atualmente, o Azure Data Factory dá suporte apenas para a movimentação dos dados do Salesforce para os [armazenamentos de dados do coletor com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats), mas não dá suporte para a movimentação dos dados de outros armazenamentos de dados para o Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7024e-106">Azure Data Factory currently supports only moving data from Salesforce to [supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores to Salesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="7024e-107">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="7024e-107">Supported versions</span></span>
<span data-ttu-id="7024e-108">Esse conector dá suporte para as seguintes edições do Salesforce: Developer Edition, Professional Edition, Enterprise Edition ou Unlimited Edition.</span><span class="sxs-lookup"><span data-stu-id="7024e-108">This connector supports the following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="7024e-109">E ele dá suporte à cópia na produção, da área restrita e do domínio personalizado do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7024e-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7024e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7024e-110">Prerequisites</span></span>
* <span data-ttu-id="7024e-111">A permissão de API deve estar habilitada.</span><span class="sxs-lookup"><span data-stu-id="7024e-111">API permission must be enabled.</span></span> <span data-ttu-id="7024e-112">Consulte [Como habilito o acesso à API no Salesforce por conjunto de permissões?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="7024e-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="7024e-113">Para copiar os dados do Salesforce para os armazenamentos de dados locais, você deve ter, pelo menos, o Gateway de Gerenciamento de Dados 2.0 instalado no ambiente local.</span><span class="sxs-lookup"><span data-stu-id="7024e-113">To copy data from Salesforce to on-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="7024e-114">Limites da solicitação Salesforce</span><span class="sxs-lookup"><span data-stu-id="7024e-114">Salesforce request limits</span></span>
<span data-ttu-id="7024e-115">O Salesforce tem limites para o total de solicitações de API e as solicitações simultâneas de API.</span><span class="sxs-lookup"><span data-stu-id="7024e-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="7024e-116">Observe os seguintes pontos:</span><span class="sxs-lookup"><span data-stu-id="7024e-116">Note the following points:</span></span>

- <span data-ttu-id="7024e-117">Se o número de solicitações simultâneas exceder o limite, a limitação será atingida e você verá falhas aleatórias.</span><span class="sxs-lookup"><span data-stu-id="7024e-117">If the number of concurrent requests exceeds the limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="7024e-118">Se o número total de solicitações exceder o limite, a conta do Salesforce será bloqueada por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="7024e-118">If the total number of requests exceeds the limit, the Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="7024e-119">Você também pode receber o erro "REQUEST_LIMIT_EXCEEDED" em ambos os cenários.</span><span class="sxs-lookup"><span data-stu-id="7024e-119">You might also receive the “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="7024e-120">Veja a seção "Limites de Solicitações da API" no artigo [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) (Limites do Desenvolvedor Salesforce) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="7024e-120">See the "API Request Limits" section in the [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7024e-121">Introdução</span><span class="sxs-lookup"><span data-stu-id="7024e-121">Getting started</span></span>
<span data-ttu-id="7024e-122">Você pode criar um pipeline com uma atividade de cópia que mova dados do Salesforce usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="7024e-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="7024e-123">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="7024e-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="7024e-124">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="7024e-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="7024e-125">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="7024e-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="7024e-126">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="7024e-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="7024e-127">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="7024e-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="7024e-128">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="7024e-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="7024e-129">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="7024e-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="7024e-130">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="7024e-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="7024e-131">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="7024e-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="7024e-132">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="7024e-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="7024e-133">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados do Salesforce, confira a seção [Exemplo de JSON: Copiar dados do Salesforce para o blob do Azure](#json-example-copy-data-from-salesforce-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="7024e-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from Salesforce, see [JSON example: Copy data from Salesforce to Azure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="7024e-134">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao Salesforce:</span><span class="sxs-lookup"><span data-stu-id="7024e-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Salesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="7024e-135">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="7024e-135">Linked service properties</span></span>
<span data-ttu-id="7024e-136">A tabela a seguir fornece descrições dos elementos JSON específicos para o serviço vinculado Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7024e-136">The following table provides descriptions for JSON elements that are specific to the Salesforce linked service.</span></span>

| <span data-ttu-id="7024e-137">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7024e-137">Property</span></span> | <span data-ttu-id="7024e-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="7024e-138">Description</span></span> | <span data-ttu-id="7024e-139">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7024e-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7024e-140">type</span><span class="sxs-lookup"><span data-stu-id="7024e-140">type</span></span> |<span data-ttu-id="7024e-141">A propriedade type deve ser definida para: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="7024e-141">The type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="7024e-142">Sim</span><span class="sxs-lookup"><span data-stu-id="7024e-142">Yes</span></span> |
| <span data-ttu-id="7024e-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="7024e-143">environmentUrl</span></span> | <span data-ttu-id="7024e-144">Especifica a URL da instância do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7024e-144">Specify the URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="7024e-145">– O padrão é "https://login.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="7024e-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="7024e-146">– Para copiar dados da área restrita, especifique "https://test.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="7024e-146">- To copy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="7024e-147">– Para copiar dados do domínio personalizado, especifique, por exemplo, "https://[domínio].my.salesforce.com".</span><span class="sxs-lookup"><span data-stu-id="7024e-147">- To copy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="7024e-148">Não</span><span class="sxs-lookup"><span data-stu-id="7024e-148">No</span></span> |
| <span data-ttu-id="7024e-149">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="7024e-149">username</span></span> |<span data-ttu-id="7024e-150">Especifique um nome de usuário para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="7024e-150">Specify a user name for the user account.</span></span> |<span data-ttu-id="7024e-151">Sim</span><span class="sxs-lookup"><span data-stu-id="7024e-151">Yes</span></span> |
| <span data-ttu-id="7024e-152">Senha</span><span class="sxs-lookup"><span data-stu-id="7024e-152">password</span></span> |<span data-ttu-id="7024e-153">Especifique um senha para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="7024e-153">Specify a password for the user account.</span></span> |<span data-ttu-id="7024e-154">Sim</span><span class="sxs-lookup"><span data-stu-id="7024e-154">Yes</span></span> |
| <span data-ttu-id="7024e-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="7024e-155">securityToken</span></span> |<span data-ttu-id="7024e-156">Especifique um token de segurança para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="7024e-156">Specify a security token for the user account.</span></span> <span data-ttu-id="7024e-157">Veja [Obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para ver instruções sobre como redefinir/obter o token de segurança.</span><span class="sxs-lookup"><span data-stu-id="7024e-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get a security token.</span></span> <span data-ttu-id="7024e-158">Para saber mais sobre os tokens de segurança em geral, veja [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm) (Segurança e a API).</span><span class="sxs-lookup"><span data-stu-id="7024e-158">To learn about security tokens in general, see [Security and the API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="7024e-159">Sim</span><span class="sxs-lookup"><span data-stu-id="7024e-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="7024e-160">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="7024e-160">Dataset properties</span></span>
<span data-ttu-id="7024e-161">Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, veja o artigo [Criando conjuntos de dados](data-factory-create-datasets.md) .</span><span class="sxs-lookup"><span data-stu-id="7024e-161">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="7024e-162">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure e outros).</span><span class="sxs-lookup"><span data-stu-id="7024e-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="7024e-163">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="7024e-163">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="7024e-164">A seção typeProperties para um conjunto de dados do tipo **RelationalTable** tem as propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="7024e-164">The typeProperties section for a dataset of the type **RelationalTable** has the following properties:</span></span>

| <span data-ttu-id="7024e-165">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7024e-165">Property</span></span> | <span data-ttu-id="7024e-166">Descrição</span><span class="sxs-lookup"><span data-stu-id="7024e-166">Description</span></span> | <span data-ttu-id="7024e-167">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7024e-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7024e-168">tableName</span><span class="sxs-lookup"><span data-stu-id="7024e-168">tableName</span></span> |<span data-ttu-id="7024e-169">Nome da tabela no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="7024e-169">Name of the table in Salesforce.</span></span> |<span data-ttu-id="7024e-170">Não (se uma **consulta** de **RelationalSource** for especificada)</span><span class="sxs-lookup"><span data-stu-id="7024e-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="7024e-171">A parte "__c" do Nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="7024e-171">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="7024e-173">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="7024e-173">Copy activity properties</span></span>
<span data-ttu-id="7024e-174">Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, veja o artigo [Criando pipelines](data-factory-create-pipelines.md) .</span><span class="sxs-lookup"><span data-stu-id="7024e-174">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7024e-175">As propriedades como o nome, descrição, tabelas de entrada e saída, e várias políticas estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="7024e-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="7024e-176">As propriedades que estão disponíveis na seção typeProperties da atividade, por outro lado, variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="7024e-176">The properties that are available in the typeProperties section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="7024e-177">Para a Atividade de Cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="7024e-177">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="7024e-178">Em Atividade de Cópia, quando a origem for do tipo **RelationalSource** (que inclui Salesforce), as seguintes propriedades estarão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="7024e-178">In copy activity, when the source is of the type **RelationalSource** (which includes Salesforce), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="7024e-179">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7024e-179">Property</span></span> | <span data-ttu-id="7024e-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="7024e-180">Description</span></span> | <span data-ttu-id="7024e-181">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="7024e-181">Allowed values</span></span> | <span data-ttu-id="7024e-182">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="7024e-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7024e-183">query</span><span class="sxs-lookup"><span data-stu-id="7024e-183">query</span></span> |<span data-ttu-id="7024e-184">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="7024e-184">Use the custom query to read data.</span></span> |<span data-ttu-id="7024e-185">Uma consulta SQL-92 ou uma consulta [SOQL (Salesforce Object Query Language)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm).</span><span class="sxs-lookup"><span data-stu-id="7024e-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="7024e-186">Por exemplo: `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="7024e-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="7024e-187">Não (se **tableName** do **conjunto de dados** for especificado)</span><span class="sxs-lookup"><span data-stu-id="7024e-187">No (if the **tableName** of the **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="7024e-188">A parte "__c" do Nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="7024e-188">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="7024e-190">Dicas de consulta</span><span class="sxs-lookup"><span data-stu-id="7024e-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="7024e-191">Recuperando dados usando a cláusula where na coluna DateTime</span><span class="sxs-lookup"><span data-stu-id="7024e-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="7024e-192">Ao especificar a consulta SQL ou SOQL, preste atenção à diferença de formato DateTime.</span><span class="sxs-lookup"><span data-stu-id="7024e-192">When specify the SOQL or SQL query, pay attention to the DateTime format difference.</span></span> <span data-ttu-id="7024e-193">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7024e-193">For example:</span></span>

* <span data-ttu-id="7024e-194">**Exemplo de SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="7024e-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="7024e-195">**Exemplo de SQL**:</span><span class="sxs-lookup"><span data-stu-id="7024e-195">**SQL sample**:</span></span>
    * <span data-ttu-id="7024e-196">**Use o assistente de cópia para especificar a consulta:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="7024e-196">**Using copy wizard to specify the query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="7024e-197">**Use a edição de JSON para especificar a consulta (escape char corretamente):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="7024e-197">**Using JSON editing to specify the query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="7024e-198">Recuperando dados do relatório do Salesforce</span><span class="sxs-lookup"><span data-stu-id="7024e-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="7024e-199">Você pode recuperar dados de relatórios do Salesforce especificando a consulta como `{call "<report name>"}`, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="7024e-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="7024e-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="7024e-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="7024e-201">Recuperar registros excluídos da lixeira do Salesforce</span><span class="sxs-lookup"><span data-stu-id="7024e-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="7024e-202">Para consultar os registros excluídos pelo software da lixeira do Salesforce, você poderá especificar **"IsDeleted = 1"** em sua consulta.</span><span class="sxs-lookup"><span data-stu-id="7024e-202">To query the soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="7024e-203">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="7024e-203">For example,</span></span>

* <span data-ttu-id="7024e-204">Para consultar apenas os registros excluídos, especifique "select * from MyTable__c **where IsDeleted= 1**"</span><span class="sxs-lookup"><span data-stu-id="7024e-204">To query only the deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="7024e-205">Para consultar todos os registros, incluindo existentes e excluídos, especifique "select * from MyTable__c **m que IsDeleted = 0 ou IsDeleted = 1**"</span><span class="sxs-lookup"><span data-stu-id="7024e-205">To query all the records including the existing and the deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-to-azure-blob"></a><span data-ttu-id="7024e-206">Exemplo de JSON: copiar dados do Salesforce para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="7024e-206">JSON example: Copy data from Salesforce to Azure Blob</span></span>
<span data-ttu-id="7024e-207">O exemplo a seguir fornece as definições JSON de exemplo que você pode utilizar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7024e-207">The following example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="7024e-208">Eles mostram como copiar dados do Salesforce para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="7024e-208">They show how to copy data from Salesforce to Azure Blob Storage.</span></span> <span data-ttu-id="7024e-209">No entanto, os dados podem ser copiados para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7024e-209">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="7024e-210">Aqui estão os artefatos Data Factory que você precisará criar para implementar o cenário.</span><span class="sxs-lookup"><span data-stu-id="7024e-210">Here are the Data Factory artifacts that you'll need to create to implement the scenario.</span></span> <span data-ttu-id="7024e-211">As seções depois da lista fornecem detalhes sobre essas etapas.</span><span class="sxs-lookup"><span data-stu-id="7024e-211">The sections that follow the list provide details about these steps.</span></span>

* <span data-ttu-id="7024e-212">Um serviço vinculado do tipo [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="7024e-212">A linked service of the type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="7024e-213">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="7024e-213">A linked service of the type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="7024e-214">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="7024e-214">An input [dataset](data-factory-create-datasets.md) of the type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="7024e-215">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="7024e-215">An output [dataset](data-factory-create-datasets.md) of the type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="7024e-216">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="7024e-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="7024e-217">**Serviço vinculado Salesforce**</span><span class="sxs-lookup"><span data-stu-id="7024e-217">**Salesforce linked service**</span></span>

<span data-ttu-id="7024e-218">Este exemplo usa o serviço vinculado **Salesforce** .</span><span class="sxs-lookup"><span data-stu-id="7024e-218">This example uses the **Salesforce** linked service.</span></span> <span data-ttu-id="7024e-219">Veja a seção [Serviço vinculado do Salesforce](#linked-service-properties) para ver as propriedades com suporte para esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="7024e-219">See the [Salesforce linked service](#linked-service-properties) section for the properties that are supported by this linked service.</span></span>  <span data-ttu-id="7024e-220">Veja [Obter token de segurança](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) para ver instruções sobre como redefinir/obter o token de segurança.</span><span class="sxs-lookup"><span data-stu-id="7024e-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how to reset/get the security token.</span></span>

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
<span data-ttu-id="7024e-221">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="7024e-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="7024e-222">**Conjunto de dados de entrada do Salesforce**</span><span class="sxs-lookup"><span data-stu-id="7024e-222">**Salesforce input dataset**</span></span>

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

<span data-ttu-id="7024e-223">Configurar **external** como **true** informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7024e-223">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7024e-224">A parte "__c" do Nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="7024e-224">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="7024e-226">**Conjunto de dados de saída do blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="7024e-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="7024e-227">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="7024e-227">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="7024e-228">**Pipeline com Atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="7024e-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="7024e-229">O pipeline contém uma Atividade de Cópia, que está configurada para usar os conjuntos de dados de entrada e saída, e está agendado para ser executado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="7024e-229">The pipeline contains Copy Activity, which is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="7024e-230">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="7024e-230">In the pipeline JSON definition, the **source** type is set to **RelationalSource**, and the **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="7024e-231">Veja [Propriedades do tipo RelationalSource](#copy-activity-properties) para obter a lista de propriedades com suporte para o RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="7024e-231">See [RelationalSource type properties](#copy-activity-properties) for the list of properties that are supported by the RelationalSource.</span></span>

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
            "description": "Copy from Salesforce to an Azure blob",
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
> <span data-ttu-id="7024e-232">A parte "__c" do Nome da API é necessária para qualquer objeto personalizado.</span><span class="sxs-lookup"><span data-stu-id="7024e-232">The "__c" part of the API Name is needed for any custom object.</span></span>

![Data Factory — conexão Salesforce — nome da API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="7024e-234">Mapeamento de tipo para Salesforce</span><span class="sxs-lookup"><span data-stu-id="7024e-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="7024e-235">Tipo Salesforce</span><span class="sxs-lookup"><span data-stu-id="7024e-235">Salesforce type</span></span> | <span data-ttu-id="7024e-236">Tipo baseado no .NET</span><span class="sxs-lookup"><span data-stu-id="7024e-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="7024e-237">Numeração automática</span><span class="sxs-lookup"><span data-stu-id="7024e-237">Auto Number</span></span> |<span data-ttu-id="7024e-238">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-238">String</span></span> |
| <span data-ttu-id="7024e-239">Caixa de seleção</span><span class="sxs-lookup"><span data-stu-id="7024e-239">Checkbox</span></span> |<span data-ttu-id="7024e-240">Booliano</span><span class="sxs-lookup"><span data-stu-id="7024e-240">Boolean</span></span> |
| <span data-ttu-id="7024e-241">Moeda</span><span class="sxs-lookup"><span data-stu-id="7024e-241">Currency</span></span> |<span data-ttu-id="7024e-242">Duplo</span><span class="sxs-lookup"><span data-stu-id="7024e-242">Double</span></span> |
| <span data-ttu-id="7024e-243">Data</span><span class="sxs-lookup"><span data-stu-id="7024e-243">Date</span></span> |<span data-ttu-id="7024e-244">DateTime</span><span class="sxs-lookup"><span data-stu-id="7024e-244">DateTime</span></span> |
| <span data-ttu-id="7024e-245">Data/hora</span><span class="sxs-lookup"><span data-stu-id="7024e-245">Date/Time</span></span> |<span data-ttu-id="7024e-246">DateTime</span><span class="sxs-lookup"><span data-stu-id="7024e-246">DateTime</span></span> |
| <span data-ttu-id="7024e-247">Email</span><span class="sxs-lookup"><span data-stu-id="7024e-247">Email</span></span> |<span data-ttu-id="7024e-248">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-248">String</span></span> |
| <span data-ttu-id="7024e-249">ID</span><span class="sxs-lookup"><span data-stu-id="7024e-249">Id</span></span> |<span data-ttu-id="7024e-250">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-250">String</span></span> |
| <span data-ttu-id="7024e-251">Relação de pesquisa</span><span class="sxs-lookup"><span data-stu-id="7024e-251">Lookup Relationship</span></span> |<span data-ttu-id="7024e-252">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-252">String</span></span> |
| <span data-ttu-id="7024e-253">Lista de seleção múltipla</span><span class="sxs-lookup"><span data-stu-id="7024e-253">Multi-Select Picklist</span></span> |<span data-ttu-id="7024e-254">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-254">String</span></span> |
| <span data-ttu-id="7024e-255">Número</span><span class="sxs-lookup"><span data-stu-id="7024e-255">Number</span></span> |<span data-ttu-id="7024e-256">Duplo</span><span class="sxs-lookup"><span data-stu-id="7024e-256">Double</span></span> |
| <span data-ttu-id="7024e-257">Porcentagem</span><span class="sxs-lookup"><span data-stu-id="7024e-257">Percent</span></span> |<span data-ttu-id="7024e-258">Duplo</span><span class="sxs-lookup"><span data-stu-id="7024e-258">Double</span></span> |
| <span data-ttu-id="7024e-259">Telefone</span><span class="sxs-lookup"><span data-stu-id="7024e-259">Phone</span></span> |<span data-ttu-id="7024e-260">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-260">String</span></span> |
| <span data-ttu-id="7024e-261">Lista de seleção</span><span class="sxs-lookup"><span data-stu-id="7024e-261">Picklist</span></span> |<span data-ttu-id="7024e-262">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-262">String</span></span> |
| <span data-ttu-id="7024e-263">Texto</span><span class="sxs-lookup"><span data-stu-id="7024e-263">Text</span></span> |<span data-ttu-id="7024e-264">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-264">String</span></span> |
| <span data-ttu-id="7024e-265">Área de texto</span><span class="sxs-lookup"><span data-stu-id="7024e-265">Text Area</span></span> |<span data-ttu-id="7024e-266">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-266">String</span></span> |
| <span data-ttu-id="7024e-267">Área de texto (longo)</span><span class="sxs-lookup"><span data-stu-id="7024e-267">Text Area (Long)</span></span> |<span data-ttu-id="7024e-268">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-268">String</span></span> |
| <span data-ttu-id="7024e-269">Área de texto (Rich)</span><span class="sxs-lookup"><span data-stu-id="7024e-269">Text Area (Rich)</span></span> |<span data-ttu-id="7024e-270">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-270">String</span></span> |
| <span data-ttu-id="7024e-271">Texto (criptografado)</span><span class="sxs-lookup"><span data-stu-id="7024e-271">Text (Encrypted)</span></span> |<span data-ttu-id="7024e-272">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-272">String</span></span> |
| <span data-ttu-id="7024e-273">URL</span><span class="sxs-lookup"><span data-stu-id="7024e-273">URL</span></span> |<span data-ttu-id="7024e-274">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="7024e-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="7024e-275">Para mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="7024e-275">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="7024e-276">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="7024e-276">Performance and tuning</span></span>
<span data-ttu-id="7024e-277">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho e a movimentação dos dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar.</span><span class="sxs-lookup"><span data-stu-id="7024e-277">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
