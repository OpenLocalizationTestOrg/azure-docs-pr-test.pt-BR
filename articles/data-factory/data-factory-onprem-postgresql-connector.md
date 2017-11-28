---
title: aaaMove dados usando o Azure Data Factory do PostgreSQL | Microsoft Docs
description: "Saiba mais sobre como toomove dados do banco de dados PostgreSQL utilizando a fábrica de dados do Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="e235f-103">Mover dados do PostgreSQL usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e235f-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="e235f-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de banco de dados PostgreSQL local.</span><span class="sxs-lookup"><span data-stu-id="e235f-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="e235f-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="e235f-106">Você pode copiar dados de um repositório de dados local PostgreSQL dados repositório tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="e235f-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="e235f-107">Para obter uma lista de repositórios de dados com suporte como coletores de atividade de cópia hello, consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="e235f-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="e235f-108">Fábrica de dados atualmente oferece suporte à movimentação de dados de um PostgreSQL de banco de dados tooother repositórios de dados, mas não para mover dados de outros dados armazena o banco de dados PostgreSQL tooan.</span><span class="sxs-lookup"><span data-stu-id="e235f-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e235f-109">pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e235f-109">prerequisites</span></span>

<span data-ttu-id="e235f-110">Serviço de fábrica de dados oferece suporte a fontes de PostgreSQL local tooon conectar usando Olá Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="e235f-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="e235f-111">Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="e235f-112">Gateway é necessário mesmo que o banco de dados PostgreSQL Olá é hospedado em uma VM de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="e235f-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="e235f-113">Você pode instalar o gateway em Olá mesmo IaaS VM como Olá dados armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e235f-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="e235f-114">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="e235f-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="e235f-115">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="e235f-115">Supported versions and installation</span></span>
<span data-ttu-id="e235f-116">Para Gateway de gerenciamento de dados tooconnect toohello banco de dados PostgreSQL, instale Olá [Ngpsql o provedor de dados para PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 ou acima em Olá mesmo sistema como Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="e235f-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="e235f-117">Há suporte para o PostgreSQL versão 7.4 e superior.</span><span class="sxs-lookup"><span data-stu-id="e235f-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e235f-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="e235f-118">Getting started</span></span>
<span data-ttu-id="e235f-119">Você pode criar um pipeline com atividade de cópia que mova dados de um repositório de dados local PostgreSQL usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="e235f-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="e235f-120">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="e235f-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e235f-121">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="e235f-122">Você também pode usar o hello ferramentas toocreate um pipeline a seguir:</span><span class="sxs-lookup"><span data-stu-id="e235f-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="e235f-123">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e235f-123">Azure portal</span></span>
    - <span data-ttu-id="e235f-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e235f-124">Visual Studio</span></span>
    - <span data-ttu-id="e235f-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e235f-125">Azure PowerShell</span></span>
    - <span data-ttu-id="e235f-126">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e235f-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="e235f-127">API do .NET</span><span class="sxs-lookup"><span data-stu-id="e235f-127">.NET API</span></span>
    - <span data-ttu-id="e235f-128">API REST</span><span class="sxs-lookup"><span data-stu-id="e235f-128">REST API</span></span>

     <span data-ttu-id="e235f-129">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="e235f-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e235f-130">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="e235f-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="e235f-131">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="e235f-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="e235f-132">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="e235f-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="e235f-133">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="e235f-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e235f-134">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="e235f-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e235f-135">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e235f-136">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados PostgreSQL local, consulte [exemplo JSON: copiar dados de PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="e235f-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="e235f-137">Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de PostgreSQL toodefine usado Data Factory entidades tooa específico:</span><span class="sxs-lookup"><span data-stu-id="e235f-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e235f-138">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="e235f-138">Linked service properties</span></span>
<span data-ttu-id="e235f-139">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooPostgreSQL vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="e235f-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="e235f-140">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e235f-140">Property</span></span> | <span data-ttu-id="e235f-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="e235f-141">Description</span></span> | <span data-ttu-id="e235f-142">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e235f-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e235f-143">type</span><span class="sxs-lookup"><span data-stu-id="e235f-143">type</span></span> |<span data-ttu-id="e235f-144">propriedade de tipo Hello deve ser definida como: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="e235f-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="e235f-145">Sim</span><span class="sxs-lookup"><span data-stu-id="e235f-145">Yes</span></span> |
| <span data-ttu-id="e235f-146">server</span><span class="sxs-lookup"><span data-stu-id="e235f-146">server</span></span> |<span data-ttu-id="e235f-147">Nome do servidor do hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e235f-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="e235f-148">Sim</span><span class="sxs-lookup"><span data-stu-id="e235f-148">Yes</span></span> |
| <span data-ttu-id="e235f-149">database</span><span class="sxs-lookup"><span data-stu-id="e235f-149">database</span></span> |<span data-ttu-id="e235f-150">Nome do banco de dados PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="e235f-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="e235f-151">Sim</span><span class="sxs-lookup"><span data-stu-id="e235f-151">Yes</span></span> |
| <span data-ttu-id="e235f-152">schema</span><span class="sxs-lookup"><span data-stu-id="e235f-152">schema</span></span> |<span data-ttu-id="e235f-153">Nome do esquema de saudação no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="e235f-154">nome do esquema Olá diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e235f-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="e235f-155">Não</span><span class="sxs-lookup"><span data-stu-id="e235f-155">No</span></span> |
| <span data-ttu-id="e235f-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="e235f-156">authenticationType</span></span> |<span data-ttu-id="e235f-157">Tipo de autenticação usado o banco de dados PostgreSQL toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e235f-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="e235f-158">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="e235f-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="e235f-159">Sim</span><span class="sxs-lookup"><span data-stu-id="e235f-159">Yes</span></span> |
| <span data-ttu-id="e235f-160">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="e235f-160">username</span></span> |<span data-ttu-id="e235f-161">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="e235f-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="e235f-162">Não</span><span class="sxs-lookup"><span data-stu-id="e235f-162">No</span></span> |
| <span data-ttu-id="e235f-163">Senha</span><span class="sxs-lookup"><span data-stu-id="e235f-163">password</span></span> |<span data-ttu-id="e235f-164">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="e235f-165">Não</span><span class="sxs-lookup"><span data-stu-id="e235f-165">No</span></span> |
| <span data-ttu-id="e235f-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e235f-166">gatewayName</span></span> |<span data-ttu-id="e235f-167">Nome do gateway Olá Olá serviço da fábrica de dados deve usar tooconnect toohello local banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e235f-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="e235f-168">Sim</span><span class="sxs-lookup"><span data-stu-id="e235f-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="e235f-169">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="e235f-169">Dataset properties</span></span>
<span data-ttu-id="e235f-170">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="e235f-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e235f-171">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="e235f-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="e235f-172">seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e235f-173">Olá typeProperties seção de conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados PostgreSQL) tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="e235f-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="e235f-174">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e235f-174">Property</span></span> | <span data-ttu-id="e235f-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="e235f-175">Description</span></span> | <span data-ttu-id="e235f-176">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e235f-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e235f-177">tableName</span><span class="sxs-lookup"><span data-stu-id="e235f-177">tableName</span></span> |<span data-ttu-id="e235f-178">Nome da tabela de saudação em Olá instância de banco de dados PostgreSQL serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="e235f-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="e235f-179">Olá tableName diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e235f-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="e235f-180">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="e235f-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="e235f-181">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="e235f-181">Copy activity properties</span></span>
<span data-ttu-id="e235f-182">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="e235f-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e235f-183">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="e235f-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="e235f-184">Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="e235f-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="e235f-185">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="e235f-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="e235f-186">Quando a fonte é do tipo **RelationalSource** (que inclui PostgreSQL), Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="e235f-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="e235f-187">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e235f-187">Property</span></span> | <span data-ttu-id="e235f-188">Descrição</span><span class="sxs-lookup"><span data-stu-id="e235f-188">Description</span></span> | <span data-ttu-id="e235f-189">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="e235f-189">Allowed values</span></span> | <span data-ttu-id="e235f-190">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e235f-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e235f-191">query</span><span class="sxs-lookup"><span data-stu-id="e235f-191">query</span></span> |<span data-ttu-id="e235f-192">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="e235f-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e235f-193">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="e235f-193">SQL query string.</span></span> <span data-ttu-id="e235f-194">Por exemplo: "query": "select * from \"MySchema\".\"MyTable\"".</span><span class="sxs-lookup"><span data-stu-id="e235f-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="e235f-195">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="e235f-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="e235f-196">Os nomes de esquema e tabela diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e235f-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="e235f-197">Coloque-as no `""` (aspas duplas) na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="e235f-198">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="e235f-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="e235f-199">Exemplo JSON: copiar dados de PostgreSQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="e235f-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="e235f-200">Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e235f-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e235f-201">Eles mostram como banco de dados PostgreSQL toocopy dados tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="e235f-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="e235f-202">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="e235f-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="e235f-203">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="e235f-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="e235f-204">Ele não inclui instruções passo a passo para criar a fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="e235f-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="e235f-205">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="e235f-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="e235f-206">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="e235f-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="e235f-207">Um serviço vinculado do tipo [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e235f-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="e235f-208">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e235f-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e235f-209">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e235f-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e235f-210">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e235f-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e235f-211">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e235f-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e235f-212">exemplo Hello copia dados de um resultado de consulta no blob de tooa do banco de dados PostgreSQL a cada hora.</span><span class="sxs-lookup"><span data-stu-id="e235f-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="e235f-213">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e235f-214">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="e235f-215">Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="e235f-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="e235f-216">**Serviço vinculado do PostgreSQL:**</span><span class="sxs-lookup"><span data-stu-id="e235f-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="e235f-217">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="e235f-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="e235f-218">**Conjunto de dados de entrada do PostgreSQL:**</span><span class="sxs-lookup"><span data-stu-id="e235f-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="e235f-219">exemplo Hello supõe que você criou uma tabela "MyTable" na PostgreSQL e contém uma coluna chamada "timestamp" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="e235f-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="e235f-220">Configuração `"external": true` informa o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="e235f-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
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

<span data-ttu-id="e235f-221">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="e235f-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e235f-222">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="e235f-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e235f-223">Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="e235f-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e235f-224">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="e235f-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="e235f-225">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="e235f-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="e235f-226">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é agendado toorun por hora.</span><span class="sxs-lookup"><span data-stu-id="e235f-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="e235f-227">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e235f-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="e235f-228">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá public.usstates tabela no banco de dados PostgreSQL hello.</span><span class="sxs-lookup"><span data-stu-id="e235f-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="e235f-229">Mapeamento de tipo para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e235f-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="e235f-230">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e235f-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="e235f-231">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="e235f-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="e235f-232">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="e235f-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="e235f-233">Ao mover dados tooPostgreSQL, hello mapeamentos a seguir são usados de PostgreSQL tipo too.NET tipo.</span><span class="sxs-lookup"><span data-stu-id="e235f-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="e235f-234">Tipo de banco de dados PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="e235f-234">PostgreSQL Database type</span></span> | <span data-ttu-id="e235f-235">Aliases de PostgresSQL</span><span class="sxs-lookup"><span data-stu-id="e235f-235">PostgresSQL aliases</span></span> | <span data-ttu-id="e235f-236">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e235f-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e235f-237">abstime</span><span class="sxs-lookup"><span data-stu-id="e235f-237">abstime</span></span> | |<span data-ttu-id="e235f-238">Datetime</span><span class="sxs-lookup"><span data-stu-id="e235f-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="e235f-239">bigint</span><span class="sxs-lookup"><span data-stu-id="e235f-239">bigint</span></span> |<span data-ttu-id="e235f-240">int8</span><span class="sxs-lookup"><span data-stu-id="e235f-240">int8</span></span> |<span data-ttu-id="e235f-241">Int64</span><span class="sxs-lookup"><span data-stu-id="e235f-241">Int64</span></span> |
| <span data-ttu-id="e235f-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="e235f-242">bigserial</span></span> |<span data-ttu-id="e235f-243">serial8</span><span class="sxs-lookup"><span data-stu-id="e235f-243">serial8</span></span> |<span data-ttu-id="e235f-244">Int64</span><span class="sxs-lookup"><span data-stu-id="e235f-244">Int64</span></span> |
| <span data-ttu-id="e235f-245">bit [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="e235f-245">bit [ (n) ]</span></span> | |<span data-ttu-id="e235f-246">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="e235f-247">bit varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="e235f-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="e235f-248">varbit</span><span class="sxs-lookup"><span data-stu-id="e235f-248">varbit</span></span> |<span data-ttu-id="e235f-249">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-249">Byte[], String</span></span> |
| <span data-ttu-id="e235f-250">booleano</span><span class="sxs-lookup"><span data-stu-id="e235f-250">boolean</span></span> |<span data-ttu-id="e235f-251">bool</span><span class="sxs-lookup"><span data-stu-id="e235f-251">bool</span></span> |<span data-ttu-id="e235f-252">Booliano</span><span class="sxs-lookup"><span data-stu-id="e235f-252">Boolean</span></span> |
| <span data-ttu-id="e235f-253">box</span><span class="sxs-lookup"><span data-stu-id="e235f-253">box</span></span> | |<span data-ttu-id="e235f-254">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-255">bytea</span><span class="sxs-lookup"><span data-stu-id="e235f-255">bytea</span></span> | |<span data-ttu-id="e235f-256">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-257">character [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="e235f-257">character [ (n) ]</span></span> |<span data-ttu-id="e235f-258">char [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="e235f-258">char [ (n) ]</span></span> |<span data-ttu-id="e235f-259">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-259">String</span></span> |
| <span data-ttu-id="e235f-260">character varying [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="e235f-260">character varying [ (n) ]</span></span> |<span data-ttu-id="e235f-261">varchar [ (n) ]</span><span class="sxs-lookup"><span data-stu-id="e235f-261">varchar [ (n) ]</span></span> |<span data-ttu-id="e235f-262">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-262">String</span></span> |
| <span data-ttu-id="e235f-263">cid</span><span class="sxs-lookup"><span data-stu-id="e235f-263">cid</span></span> | |<span data-ttu-id="e235f-264">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-264">String</span></span> |&nbsp;
| <span data-ttu-id="e235f-265">cidr</span><span class="sxs-lookup"><span data-stu-id="e235f-265">cidr</span></span> | |<span data-ttu-id="e235f-266">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-266">String</span></span> |&nbsp;
| <span data-ttu-id="e235f-267">circle</span><span class="sxs-lookup"><span data-stu-id="e235f-267">circle</span></span> | |<span data-ttu-id="e235f-268">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-269">data</span><span class="sxs-lookup"><span data-stu-id="e235f-269">date</span></span> | |<span data-ttu-id="e235f-270">Datetime</span><span class="sxs-lookup"><span data-stu-id="e235f-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="e235f-271">daterange</span><span class="sxs-lookup"><span data-stu-id="e235f-271">daterange</span></span> | |<span data-ttu-id="e235f-272">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-272">String</span></span> |&nbsp;
| <span data-ttu-id="e235f-273">double precision</span><span class="sxs-lookup"><span data-stu-id="e235f-273">double precision</span></span> |<span data-ttu-id="e235f-274">float8</span><span class="sxs-lookup"><span data-stu-id="e235f-274">float8</span></span> |<span data-ttu-id="e235f-275">Duplo</span><span class="sxs-lookup"><span data-stu-id="e235f-275">Double</span></span> |
| <span data-ttu-id="e235f-276">inet</span><span class="sxs-lookup"><span data-stu-id="e235f-276">inet</span></span> | |<span data-ttu-id="e235f-277">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-278">intarry</span><span class="sxs-lookup"><span data-stu-id="e235f-278">intarry</span></span> | |<span data-ttu-id="e235f-279">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-279">String</span></span> |&nbsp;
| <span data-ttu-id="e235f-280">int4range</span><span class="sxs-lookup"><span data-stu-id="e235f-280">int4range</span></span> | |<span data-ttu-id="e235f-281">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-281">String</span></span> |&nbsp;
| <span data-ttu-id="e235f-282">int8range</span><span class="sxs-lookup"><span data-stu-id="e235f-282">int8range</span></span> | |<span data-ttu-id="e235f-283">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-283">String</span></span> |&nbsp;
| <span data-ttu-id="e235f-284">inteiro</span><span class="sxs-lookup"><span data-stu-id="e235f-284">integer</span></span> |<span data-ttu-id="e235f-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="e235f-285">int, int4</span></span> |<span data-ttu-id="e235f-286">Int32</span><span class="sxs-lookup"><span data-stu-id="e235f-286">Int32</span></span> |
| <span data-ttu-id="e235f-287">interval [ fields ] [ (p) ]</span><span class="sxs-lookup"><span data-stu-id="e235f-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="e235f-288">Timespan</span><span class="sxs-lookup"><span data-stu-id="e235f-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="e235f-289">json</span><span class="sxs-lookup"><span data-stu-id="e235f-289">json</span></span> | |<span data-ttu-id="e235f-290">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-290">String</span></span> |&nbsp;
| <span data-ttu-id="e235f-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="e235f-291">jsonb</span></span> | |<span data-ttu-id="e235f-292">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e235f-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="e235f-293">line</span><span class="sxs-lookup"><span data-stu-id="e235f-293">line</span></span> | |<span data-ttu-id="e235f-294">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-295">lseg</span><span class="sxs-lookup"><span data-stu-id="e235f-295">lseg</span></span> | |<span data-ttu-id="e235f-296">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="e235f-297">macaddr</span></span> | |<span data-ttu-id="e235f-298">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-299">money</span><span class="sxs-lookup"><span data-stu-id="e235f-299">money</span></span> | |<span data-ttu-id="e235f-300">Decimal</span><span class="sxs-lookup"><span data-stu-id="e235f-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="e235f-301">numeric [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="e235f-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="e235f-302">decimal [ (p, s) ]</span><span class="sxs-lookup"><span data-stu-id="e235f-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="e235f-303">Decimal</span><span class="sxs-lookup"><span data-stu-id="e235f-303">Decimal</span></span> |
| <span data-ttu-id="e235f-304">numrange</span><span class="sxs-lookup"><span data-stu-id="e235f-304">numrange</span></span> | |<span data-ttu-id="e235f-305">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-305">String</span></span> |&nbsp;
| <span data-ttu-id="e235f-306">oid</span><span class="sxs-lookup"><span data-stu-id="e235f-306">oid</span></span> | |<span data-ttu-id="e235f-307">Int32</span><span class="sxs-lookup"><span data-stu-id="e235f-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="e235f-308">path</span><span class="sxs-lookup"><span data-stu-id="e235f-308">path</span></span> | |<span data-ttu-id="e235f-309">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="e235f-310">pg_lsn</span></span> | |<span data-ttu-id="e235f-311">Int64</span><span class="sxs-lookup"><span data-stu-id="e235f-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="e235f-312">point</span><span class="sxs-lookup"><span data-stu-id="e235f-312">point</span></span> | |<span data-ttu-id="e235f-313">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-314">polygon</span><span class="sxs-lookup"><span data-stu-id="e235f-314">polygon</span></span> | |<span data-ttu-id="e235f-315">Byte[], String</span><span class="sxs-lookup"><span data-stu-id="e235f-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="e235f-316">real</span><span class="sxs-lookup"><span data-stu-id="e235f-316">real</span></span> |<span data-ttu-id="e235f-317">float4</span><span class="sxs-lookup"><span data-stu-id="e235f-317">float4</span></span> |<span data-ttu-id="e235f-318">Single</span><span class="sxs-lookup"><span data-stu-id="e235f-318">Single</span></span> |
| <span data-ttu-id="e235f-319">smallint</span><span class="sxs-lookup"><span data-stu-id="e235f-319">smallint</span></span> |<span data-ttu-id="e235f-320">int2</span><span class="sxs-lookup"><span data-stu-id="e235f-320">int2</span></span> |<span data-ttu-id="e235f-321">Int16</span><span class="sxs-lookup"><span data-stu-id="e235f-321">Int16</span></span> |
| <span data-ttu-id="e235f-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="e235f-322">smallserial</span></span> |<span data-ttu-id="e235f-323">serial2</span><span class="sxs-lookup"><span data-stu-id="e235f-323">serial2</span></span> |<span data-ttu-id="e235f-324">Int16</span><span class="sxs-lookup"><span data-stu-id="e235f-324">Int16</span></span> |
| <span data-ttu-id="e235f-325">serial</span><span class="sxs-lookup"><span data-stu-id="e235f-325">serial</span></span> |<span data-ttu-id="e235f-326">serial4</span><span class="sxs-lookup"><span data-stu-id="e235f-326">serial4</span></span> |<span data-ttu-id="e235f-327">Int32</span><span class="sxs-lookup"><span data-stu-id="e235f-327">Int32</span></span> |
| <span data-ttu-id="e235f-328">texto</span><span class="sxs-lookup"><span data-stu-id="e235f-328">text</span></span> | |<span data-ttu-id="e235f-329">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e235f-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="e235f-330">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="e235f-330">Map source toosink columns</span></span>
<span data-ttu-id="e235f-331">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e235f-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e235f-332">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="e235f-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="e235f-333">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="e235f-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="e235f-334">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="e235f-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e235f-335">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="e235f-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e235f-336">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="e235f-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e235f-337">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="e235f-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e235f-338">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="e235f-338">Performance and Tuning</span></span>
<span data-ttu-id="e235f-339">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="e235f-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
