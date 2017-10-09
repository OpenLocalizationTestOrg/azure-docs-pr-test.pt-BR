---
title: dados de aaaMove do MySQL usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como toomove dados do MySQL do banco de dados usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="38031-103">Mover dados do MySQL usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="38031-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="38031-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de banco de dados MySQL local.</span><span class="sxs-lookup"><span data-stu-id="38031-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="38031-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="38031-106">Você pode copiar dados de um repositório de dados local MySQL dados repositório tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="38031-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="38031-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="38031-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="38031-108">Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de um de dados MySQL, mas não para mover dados de outro armazenamento de dados dados repositórios tooan MySQL.</span><span class="sxs-lookup"><span data-stu-id="38031-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="38031-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="38031-109">Prerequisites</span></span>
<span data-ttu-id="38031-110">Serviço da fábrica de dados oferece suporte a fontes de MySQL local tooon conexão usando Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="38031-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="38031-111">Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="38031-112">Gateway é necessário mesmo que o banco de dados do hello MySQL é hospedado em uma máquina virtual de IaaS do Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="38031-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="38031-113">Você pode instalar o gateway de saudação em Olá mesma VM como dados Olá armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="38031-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="38031-114">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="38031-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="38031-115">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="38031-115">Supported versions and installation</span></span>
<span data-ttu-id="38031-116">Para Gateway de gerenciamento de dados tooconnect toohello banco de dados MySQL, você precisa tooinstall Olá [MySQL Connector/Net para o Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versão 6.6.5 ou superior) Olá no mesmo sistema como Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="38031-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="38031-117">Há suporte para o MySQL versão 5.1 e superior.</span><span class="sxs-lookup"><span data-stu-id="38031-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="38031-118">Se você atingir o erro "Falha de autenticação porque o participante remoto Olá fechou fluxo de transporte hello.", considere Olá tooupgrade versão do MySQL Connector/Net toohigher.</span><span class="sxs-lookup"><span data-stu-id="38031-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="38031-119">Introdução</span><span class="sxs-lookup"><span data-stu-id="38031-119">Getting started</span></span>
<span data-ttu-id="38031-120">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="38031-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="38031-121">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="38031-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="38031-122">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="38031-123">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="38031-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="38031-124">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="38031-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="38031-125">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="38031-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="38031-126">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="38031-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="38031-127">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="38031-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="38031-128">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="38031-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="38031-129">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="38031-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="38031-130">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="38031-131">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados MySQL local, consulte [exemplo JSON: copiar dados do MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="38031-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="38031-132">Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de MySQL toodefine usado Data Factory entidades tooa específico:</span><span class="sxs-lookup"><span data-stu-id="38031-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="38031-133">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="38031-133">Linked service properties</span></span>
<span data-ttu-id="38031-134">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooMySQL vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="38031-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="38031-135">Propriedade</span><span class="sxs-lookup"><span data-stu-id="38031-135">Property</span></span> | <span data-ttu-id="38031-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="38031-136">Description</span></span> | <span data-ttu-id="38031-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="38031-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38031-138">type</span><span class="sxs-lookup"><span data-stu-id="38031-138">type</span></span> |<span data-ttu-id="38031-139">propriedade de tipo Hello deve ser definida como: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="38031-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="38031-140">Sim</span><span class="sxs-lookup"><span data-stu-id="38031-140">Yes</span></span> |
| <span data-ttu-id="38031-141">server</span><span class="sxs-lookup"><span data-stu-id="38031-141">server</span></span> |<span data-ttu-id="38031-142">Nome do servidor MySQL de saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="38031-143">Sim</span><span class="sxs-lookup"><span data-stu-id="38031-143">Yes</span></span> |
| <span data-ttu-id="38031-144">database</span><span class="sxs-lookup"><span data-stu-id="38031-144">database</span></span> |<span data-ttu-id="38031-145">Nome do banco de dados do hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="38031-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="38031-146">Sim</span><span class="sxs-lookup"><span data-stu-id="38031-146">Yes</span></span> |
| <span data-ttu-id="38031-147">schema</span><span class="sxs-lookup"><span data-stu-id="38031-147">schema</span></span> |<span data-ttu-id="38031-148">Nome do esquema de saudação no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="38031-149">Não</span><span class="sxs-lookup"><span data-stu-id="38031-149">No</span></span> |
| <span data-ttu-id="38031-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="38031-150">authenticationType</span></span> |<span data-ttu-id="38031-151">Tipo de autenticação usado o banco de dados do tooconnect toohello MySQL.</span><span class="sxs-lookup"><span data-stu-id="38031-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="38031-152">Os valores possíveis são: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="38031-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="38031-153">Sim</span><span class="sxs-lookup"><span data-stu-id="38031-153">Yes</span></span> |
| <span data-ttu-id="38031-154">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="38031-154">username</span></span> |<span data-ttu-id="38031-155">Especifique o banco de dados do usuário nome tooconnect toohello MySQL.</span><span class="sxs-lookup"><span data-stu-id="38031-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="38031-156">Sim</span><span class="sxs-lookup"><span data-stu-id="38031-156">Yes</span></span> |
| <span data-ttu-id="38031-157">Senha</span><span class="sxs-lookup"><span data-stu-id="38031-157">password</span></span> |<span data-ttu-id="38031-158">Especifique a senha da conta de usuário de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="38031-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="38031-159">Sim</span><span class="sxs-lookup"><span data-stu-id="38031-159">Yes</span></span> |
| <span data-ttu-id="38031-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="38031-160">gatewayName</span></span> |<span data-ttu-id="38031-161">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local MySQL.</span><span class="sxs-lookup"><span data-stu-id="38031-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="38031-162">Sim</span><span class="sxs-lookup"><span data-stu-id="38031-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="38031-163">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="38031-163">Dataset properties</span></span>
<span data-ttu-id="38031-164">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="38031-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="38031-165">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="38031-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="38031-166">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="38031-167">Olá typeProperties seção de conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados MySQL) tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="38031-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="38031-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="38031-168">Property</span></span> | <span data-ttu-id="38031-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="38031-169">Description</span></span> | <span data-ttu-id="38031-170">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="38031-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="38031-171">tableName</span><span class="sxs-lookup"><span data-stu-id="38031-171">tableName</span></span> |<span data-ttu-id="38031-172">Nome da tabela de saudação em Olá instância de banco de dados MySQL serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="38031-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="38031-173">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="38031-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="38031-174">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="38031-174">Copy activity properties</span></span>
<span data-ttu-id="38031-175">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="38031-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="38031-176">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="38031-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="38031-177">Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="38031-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="38031-178">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="38031-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="38031-179">Quando a fonte na atividade de cópia é do tipo **RelationalSource** (que inclui o MySQL), Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="38031-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="38031-180">Propriedade</span><span class="sxs-lookup"><span data-stu-id="38031-180">Property</span></span> | <span data-ttu-id="38031-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="38031-181">Description</span></span> | <span data-ttu-id="38031-182">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="38031-182">Allowed values</span></span> | <span data-ttu-id="38031-183">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="38031-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="38031-184">query</span><span class="sxs-lookup"><span data-stu-id="38031-184">query</span></span> |<span data-ttu-id="38031-185">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="38031-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="38031-186">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="38031-186">SQL query string.</span></span> <span data-ttu-id="38031-187">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="38031-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="38031-188">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="38031-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="38031-189">Exemplo JSON: copiar dados do MySQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="38031-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="38031-190">Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="38031-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="38031-191">Ele mostra como toocopy dados do MySQL local de banco de dados tooan armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="38031-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="38031-192">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="38031-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38031-193">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="38031-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="38031-194">Ele não inclui instruções passo a passo para criar a fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="38031-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="38031-195">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="38031-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="38031-196">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="38031-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="38031-197">Um serviço vinculado do tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="38031-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="38031-198">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="38031-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="38031-199">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="38031-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="38031-200">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="38031-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="38031-201">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="38031-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="38031-202">exemplo Hello copia dados de um resultado de consulta no blob de tooa do banco de dados MySQL por hora.</span><span class="sxs-lookup"><span data-stu-id="38031-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="38031-203">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="38031-204">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="38031-205">Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="38031-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="38031-206">**Serviço vinculado do MySQL:**</span><span class="sxs-lookup"><span data-stu-id="38031-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="38031-207">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="38031-207">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="38031-208">**Conjunto de dados de entrada do MySQL:**</span><span class="sxs-lookup"><span data-stu-id="38031-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="38031-209">exemplo Hello supõe que você criou uma tabela "MyTable" no MySQL e contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="38031-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="38031-210">Definindo "externo": "verdadeiro" informa Olá serviço de fábrica de dados tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="38031-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
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

<span data-ttu-id="38031-211">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="38031-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="38031-212">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="38031-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="38031-213">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="38031-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="38031-214">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="38031-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="38031-215">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="38031-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="38031-216">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="38031-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="38031-217">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="38031-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="38031-218">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="38031-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
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
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="38031-219">Mapeamento de tipo para MySQL</span><span class="sxs-lookup"><span data-stu-id="38031-219">Type mapping for MySQL</span></span>
<span data-ttu-id="38031-220">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="38031-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="38031-221">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="38031-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="38031-222">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="38031-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="38031-223">Ao mover dados tooMySQL, hello mapeamentos a seguir são usados de tipos de too.NET de tipos do MySQL.</span><span class="sxs-lookup"><span data-stu-id="38031-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="38031-224">Tipo do Banco de Dados MySQL</span><span class="sxs-lookup"><span data-stu-id="38031-224">MySQL Database type</span></span> | <span data-ttu-id="38031-225">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="38031-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="38031-226">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="38031-226">bigint unsigned</span></span> |<span data-ttu-id="38031-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="38031-227">Decimal</span></span> |
| <span data-ttu-id="38031-228">bigint</span><span class="sxs-lookup"><span data-stu-id="38031-228">bigint</span></span> |<span data-ttu-id="38031-229">Int64</span><span class="sxs-lookup"><span data-stu-id="38031-229">Int64</span></span> |
| <span data-ttu-id="38031-230">bit</span><span class="sxs-lookup"><span data-stu-id="38031-230">bit</span></span> |<span data-ttu-id="38031-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="38031-231">Decimal</span></span> |
| <span data-ttu-id="38031-232">blob</span><span class="sxs-lookup"><span data-stu-id="38031-232">blob</span></span> |<span data-ttu-id="38031-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="38031-233">Byte[]</span></span> |
| <span data-ttu-id="38031-234">bool</span><span class="sxs-lookup"><span data-stu-id="38031-234">bool</span></span> |<span data-ttu-id="38031-235">Booliano</span><span class="sxs-lookup"><span data-stu-id="38031-235">Boolean</span></span> |
| <span data-ttu-id="38031-236">char</span><span class="sxs-lookup"><span data-stu-id="38031-236">char</span></span> |<span data-ttu-id="38031-237">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="38031-237">String</span></span> |
| <span data-ttu-id="38031-238">data</span><span class="sxs-lookup"><span data-stu-id="38031-238">date</span></span> |<span data-ttu-id="38031-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="38031-239">Datetime</span></span> |
| <span data-ttu-id="38031-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="38031-240">datetime</span></span> |<span data-ttu-id="38031-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="38031-241">Datetime</span></span> |
| <span data-ttu-id="38031-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="38031-242">decimal</span></span> |<span data-ttu-id="38031-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="38031-243">Decimal</span></span> |
| <span data-ttu-id="38031-244">double precision</span><span class="sxs-lookup"><span data-stu-id="38031-244">double precision</span></span> |<span data-ttu-id="38031-245">Duplo</span><span class="sxs-lookup"><span data-stu-id="38031-245">Double</span></span> |
| <span data-ttu-id="38031-246">Duplo</span><span class="sxs-lookup"><span data-stu-id="38031-246">double</span></span> |<span data-ttu-id="38031-247">Duplo</span><span class="sxs-lookup"><span data-stu-id="38031-247">Double</span></span> |
| <span data-ttu-id="38031-248">enum</span><span class="sxs-lookup"><span data-stu-id="38031-248">enum</span></span> |<span data-ttu-id="38031-249">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="38031-249">String</span></span> |
| <span data-ttu-id="38031-250">flutuante</span><span class="sxs-lookup"><span data-stu-id="38031-250">float</span></span> |<span data-ttu-id="38031-251">Single</span><span class="sxs-lookup"><span data-stu-id="38031-251">Single</span></span> |
| <span data-ttu-id="38031-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="38031-252">int unsigned</span></span> |<span data-ttu-id="38031-253">Int64</span><span class="sxs-lookup"><span data-stu-id="38031-253">Int64</span></span> |
| <span data-ttu-id="38031-254">int</span><span class="sxs-lookup"><span data-stu-id="38031-254">int</span></span> |<span data-ttu-id="38031-255">Int32</span><span class="sxs-lookup"><span data-stu-id="38031-255">Int32</span></span> |
| <span data-ttu-id="38031-256">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="38031-256">integer unsigned</span></span> |<span data-ttu-id="38031-257">Int64</span><span class="sxs-lookup"><span data-stu-id="38031-257">Int64</span></span> |
| <span data-ttu-id="38031-258">inteiro</span><span class="sxs-lookup"><span data-stu-id="38031-258">integer</span></span> |<span data-ttu-id="38031-259">Int32</span><span class="sxs-lookup"><span data-stu-id="38031-259">Int32</span></span> |
| <span data-ttu-id="38031-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="38031-260">long varbinary</span></span> |<span data-ttu-id="38031-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="38031-261">Byte[]</span></span> |
| <span data-ttu-id="38031-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="38031-262">long varchar</span></span> |<span data-ttu-id="38031-263">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="38031-263">String</span></span> |
| <span data-ttu-id="38031-264">longblob</span><span class="sxs-lookup"><span data-stu-id="38031-264">longblob</span></span> |<span data-ttu-id="38031-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="38031-265">Byte[]</span></span> |
| <span data-ttu-id="38031-266">longtext</span><span class="sxs-lookup"><span data-stu-id="38031-266">longtext</span></span> |<span data-ttu-id="38031-267">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="38031-267">String</span></span> |
| <span data-ttu-id="38031-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="38031-268">mediumblob</span></span> |<span data-ttu-id="38031-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="38031-269">Byte[]</span></span> |
| <span data-ttu-id="38031-270">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="38031-270">mediumint unsigned</span></span> |<span data-ttu-id="38031-271">Int64</span><span class="sxs-lookup"><span data-stu-id="38031-271">Int64</span></span> |
| <span data-ttu-id="38031-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="38031-272">mediumint</span></span> |<span data-ttu-id="38031-273">Int32</span><span class="sxs-lookup"><span data-stu-id="38031-273">Int32</span></span> |
| <span data-ttu-id="38031-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="38031-274">mediumtext</span></span> |<span data-ttu-id="38031-275">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="38031-275">String</span></span> |
| <span data-ttu-id="38031-276">numérico</span><span class="sxs-lookup"><span data-stu-id="38031-276">numeric</span></span> |<span data-ttu-id="38031-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="38031-277">Decimal</span></span> |
| <span data-ttu-id="38031-278">real</span><span class="sxs-lookup"><span data-stu-id="38031-278">real</span></span> |<span data-ttu-id="38031-279">Duplo</span><span class="sxs-lookup"><span data-stu-id="38031-279">Double</span></span> |
| <span data-ttu-id="38031-280">set</span><span class="sxs-lookup"><span data-stu-id="38031-280">set</span></span> |<span data-ttu-id="38031-281">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="38031-281">String</span></span> |
| <span data-ttu-id="38031-282">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="38031-282">smallint unsigned</span></span> |<span data-ttu-id="38031-283">Int32</span><span class="sxs-lookup"><span data-stu-id="38031-283">Int32</span></span> |
| <span data-ttu-id="38031-284">smallint</span><span class="sxs-lookup"><span data-stu-id="38031-284">smallint</span></span> |<span data-ttu-id="38031-285">Int16</span><span class="sxs-lookup"><span data-stu-id="38031-285">Int16</span></span> |
| <span data-ttu-id="38031-286">texto</span><span class="sxs-lookup"><span data-stu-id="38031-286">text</span></span> |<span data-ttu-id="38031-287">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="38031-287">String</span></span> |
| <span data-ttu-id="38031-288">tempo real</span><span class="sxs-lookup"><span data-stu-id="38031-288">time</span></span> |<span data-ttu-id="38031-289">timespan</span><span class="sxs-lookup"><span data-stu-id="38031-289">TimeSpan</span></span> |
| <span data-ttu-id="38031-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="38031-290">timestamp</span></span> |<span data-ttu-id="38031-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="38031-291">Datetime</span></span> |
| <span data-ttu-id="38031-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="38031-292">tinyblob</span></span> |<span data-ttu-id="38031-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="38031-293">Byte[]</span></span> |
| <span data-ttu-id="38031-294">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="38031-294">tinyint unsigned</span></span> |<span data-ttu-id="38031-295">Int16</span><span class="sxs-lookup"><span data-stu-id="38031-295">Int16</span></span> |
| <span data-ttu-id="38031-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="38031-296">tinyint</span></span> |<span data-ttu-id="38031-297">Int16</span><span class="sxs-lookup"><span data-stu-id="38031-297">Int16</span></span> |
| <span data-ttu-id="38031-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="38031-298">tinytext</span></span> |<span data-ttu-id="38031-299">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="38031-299">String</span></span> |
| <span data-ttu-id="38031-300">varchar</span><span class="sxs-lookup"><span data-stu-id="38031-300">varchar</span></span> |<span data-ttu-id="38031-301">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="38031-301">String</span></span> |
| <span data-ttu-id="38031-302">year</span><span class="sxs-lookup"><span data-stu-id="38031-302">year</span></span> |<span data-ttu-id="38031-303">int</span><span class="sxs-lookup"><span data-stu-id="38031-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="38031-304">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="38031-304">Map source toosink columns</span></span>
<span data-ttu-id="38031-305">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="38031-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="38031-306">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="38031-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="38031-307">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="38031-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="38031-308">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="38031-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="38031-309">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="38031-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="38031-310">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="38031-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="38031-311">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="38031-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="38031-312">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="38031-312">Performance and Tuning</span></span>
<span data-ttu-id="38031-313">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="38031-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
