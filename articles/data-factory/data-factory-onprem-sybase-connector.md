---
title: dados de aaaMove do Sybase usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como toomove dados do banco de dados Sybase usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="2f5b7-103">Mover dados do Sybase usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2f5b7-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="2f5b7-104">Este artigo explica como toouse hello atividade de cópia de dados do Azure Data Factory toomove de banco de dados Sybase local.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="2f5b7-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="2f5b7-106">Você pode copiar dados de um repositório de dados local Sybase dados repositório tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="2f5b7-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2f5b7-108">Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de um de dados Sybase, mas não para mover dados de outro armazenamento de dados dados repositórios tooa Sybase.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2f5b7-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2f5b7-109">Prerequisites</span></span>
<span data-ttu-id="2f5b7-110">Serviço da fábrica de dados oferece suporte a fontes de Sybase local tooon conexão usando Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="2f5b7-111">Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="2f5b7-112">Gateway é necessário mesmo que o banco de dados do Sybase Olá é hospedado em uma VM de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="2f5b7-113">Você pode instalar o gateway de saudação em Olá mesmo IaaS VM como Olá dados armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="2f5b7-114">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="2f5b7-115">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="2f5b7-115">Supported versions and installation</span></span>
<span data-ttu-id="2f5b7-116">Para Gateway de gerenciamento de dados tooconnect toohello banco de dados Sybase, você precisa Olá tooinstall [provedor de dados do Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 ou acima em Olá mesmo sistema como Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="2f5b7-117">Há suporte para o Sybase versão 16 e superior.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2f5b7-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="2f5b7-118">Getting started</span></span>
<span data-ttu-id="2f5b7-119">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="2f5b7-120">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2f5b7-121">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="2f5b7-122">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2f5b7-123">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2f5b7-124">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f5b7-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="2f5b7-125">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2f5b7-126">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="2f5b7-127">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2f5b7-128">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2f5b7-129">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2f5b7-130">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados Sybase local, consulte [exemplo JSON: copiar dados do Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2f5b7-131">Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de Sybase toodefine usado Data Factory entidades tooa específico:</span><span class="sxs-lookup"><span data-stu-id="2f5b7-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2f5b7-132">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="2f5b7-132">Linked service properties</span></span>
<span data-ttu-id="2f5b7-133">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooSybase vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="2f5b7-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2f5b7-134">Property</span></span> | <span data-ttu-id="2f5b7-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="2f5b7-135">Description</span></span> | <span data-ttu-id="2f5b7-136">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2f5b7-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f5b7-137">type</span><span class="sxs-lookup"><span data-stu-id="2f5b7-137">type</span></span> |<span data-ttu-id="2f5b7-138">propriedade de tipo Hello deve ser definida como: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="2f5b7-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="2f5b7-139">Sim</span><span class="sxs-lookup"><span data-stu-id="2f5b7-139">Yes</span></span> |
| <span data-ttu-id="2f5b7-140">server</span><span class="sxs-lookup"><span data-stu-id="2f5b7-140">server</span></span> |<span data-ttu-id="2f5b7-141">Nome do servidor do Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="2f5b7-142">Sim</span><span class="sxs-lookup"><span data-stu-id="2f5b7-142">Yes</span></span> |
| <span data-ttu-id="2f5b7-143">database</span><span class="sxs-lookup"><span data-stu-id="2f5b7-143">database</span></span> |<span data-ttu-id="2f5b7-144">Nome do banco de dados do Sybase hello.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="2f5b7-145">Sim</span><span class="sxs-lookup"><span data-stu-id="2f5b7-145">Yes</span></span> |
| <span data-ttu-id="2f5b7-146">schema</span><span class="sxs-lookup"><span data-stu-id="2f5b7-146">schema</span></span> |<span data-ttu-id="2f5b7-147">Nome do esquema de saudação no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="2f5b7-148">Não</span><span class="sxs-lookup"><span data-stu-id="2f5b7-148">No</span></span> |
| <span data-ttu-id="2f5b7-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2f5b7-149">authenticationType</span></span> |<span data-ttu-id="2f5b7-150">Tipo de autenticação usado o banco de dados do Sybase tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="2f5b7-151">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="2f5b7-152">Sim</span><span class="sxs-lookup"><span data-stu-id="2f5b7-152">Yes</span></span> |
| <span data-ttu-id="2f5b7-153">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="2f5b7-153">username</span></span> |<span data-ttu-id="2f5b7-154">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="2f5b7-155">Não</span><span class="sxs-lookup"><span data-stu-id="2f5b7-155">No</span></span> |
| <span data-ttu-id="2f5b7-156">Senha</span><span class="sxs-lookup"><span data-stu-id="2f5b7-156">password</span></span> |<span data-ttu-id="2f5b7-157">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="2f5b7-158">Não</span><span class="sxs-lookup"><span data-stu-id="2f5b7-158">No</span></span> |
| <span data-ttu-id="2f5b7-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2f5b7-159">gatewayName</span></span> |<span data-ttu-id="2f5b7-160">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados Sybase local de toohello de tooconnect.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="2f5b7-161">Sim</span><span class="sxs-lookup"><span data-stu-id="2f5b7-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2f5b7-162">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="2f5b7-162">Dataset properties</span></span>
<span data-ttu-id="2f5b7-163">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2f5b7-164">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2f5b7-165">seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2f5b7-166">Olá **typeProperties** seção de conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados Sybase) tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f5b7-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="2f5b7-167">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2f5b7-167">Property</span></span> | <span data-ttu-id="2f5b7-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="2f5b7-168">Description</span></span> | <span data-ttu-id="2f5b7-169">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2f5b7-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f5b7-170">tableName</span><span class="sxs-lookup"><span data-stu-id="2f5b7-170">tableName</span></span> |<span data-ttu-id="2f5b7-171">Nome da tabela de saudação em Olá instância de banco de dados Sybase serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="2f5b7-172">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="2f5b7-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2f5b7-173">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="2f5b7-173">Copy activity properties</span></span>
<span data-ttu-id="2f5b7-174">Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, consulte o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2f5b7-175">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="2f5b7-176">Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="2f5b7-177">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2f5b7-178">Quando a fonte de saudação é do tipo **RelationalSource** (que inclui Sybase), Olá propriedades a seguir está disponível em **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="2f5b7-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="2f5b7-179">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2f5b7-179">Property</span></span> | <span data-ttu-id="2f5b7-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="2f5b7-180">Description</span></span> | <span data-ttu-id="2f5b7-181">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="2f5b7-181">Allowed values</span></span> | <span data-ttu-id="2f5b7-182">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2f5b7-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2f5b7-183">query</span><span class="sxs-lookup"><span data-stu-id="2f5b7-183">query</span></span> |<span data-ttu-id="2f5b7-184">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="2f5b7-185">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-185">SQL query string.</span></span> <span data-ttu-id="2f5b7-186">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="2f5b7-187">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="2f5b7-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="2f5b7-188">Exemplo JSON: copiar dados do Sybase tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="2f5b7-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="2f5b7-189">Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2f5b7-190">Eles mostram como banco de dados toocopy do Sybase dados tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="2f5b7-191">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="2f5b7-192">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f5b7-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="2f5b7-193">Um serviço vinculado do tipo [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="2f5b7-194">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2f5b7-195">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="2f5b7-196">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2f5b7-197">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2f5b7-198">exemplo Hello copia dados de um resultado de consulta no blob de tooa do banco de dados Sybase a cada hora.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="2f5b7-199">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="2f5b7-200">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="2f5b7-201">Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2f5b7-202">**Serviço vinculado Sybase:**</span><span class="sxs-lookup"><span data-stu-id="2f5b7-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

<span data-ttu-id="2f5b7-203">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="2f5b7-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="2f5b7-204">**Conjunto de dados de entrada do Sybase:**</span><span class="sxs-lookup"><span data-stu-id="2f5b7-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="2f5b7-205">exemplo Hello supõe que você criou uma tabela "MyTable" na Sybase e contém uma coluna chamada "timestamp" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="2f5b7-206">Definindo "externo": true informa o serviço de fábrica de dados de saudação que este conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="2f5b7-207">Observe que Olá **tipo** Olá serviço vinculado está definido como: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

<span data-ttu-id="2f5b7-208">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="2f5b7-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2f5b7-209">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2f5b7-210">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="2f5b7-211">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="2f5b7-212">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="2f5b7-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="2f5b7-213">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é agendado toorun por hora.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="2f5b7-214">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="2f5b7-215">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados saudação da saudação DBA. Tabela de pedidos no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="2f5b7-216">Mapeamento de tipo para Sybase</span><span class="sxs-lookup"><span data-stu-id="2f5b7-216">Type mapping for Sybase</span></span>
<span data-ttu-id="2f5b7-217">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, hello atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2f5b7-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="2f5b7-218">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="2f5b7-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="2f5b7-219">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="2f5b7-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="2f5b7-220">Sybase dá suporte a T-SQL e tipos T-SQL.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="2f5b7-221">Para uma tabela de mapeamento de tipo de too.NET de tipos de sql, consulte [conector do SQL Azure](data-factory-azure-sql-connector.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="2f5b7-222">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="2f5b7-222">Map source toosink columns</span></span>
<span data-ttu-id="2f5b7-223">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2f5b7-224">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="2f5b7-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="2f5b7-225">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="2f5b7-226">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2f5b7-227">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2f5b7-228">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2f5b7-229">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2f5b7-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2f5b7-230">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="2f5b7-230">Performance and Tuning</span></span>
<span data-ttu-id="2f5b7-231">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="2f5b7-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
