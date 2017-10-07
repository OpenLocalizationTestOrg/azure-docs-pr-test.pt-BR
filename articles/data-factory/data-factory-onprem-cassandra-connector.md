---
title: "dados de aaaMove de Cassandra utilizando a fábrica de dados | Microsoft Docs"
description: Saiba mais sobre como dados toomove Cassandra um local de banco de dados usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="5a0f2-103">Mover dados de um banco de dados Cassandra local usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5a0f2-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="5a0f2-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de um banco de dados de Cassandra local.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="5a0f2-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="5a0f2-106">Você pode copiar dados de um repositório de dados local Cassandra dados repositório tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="5a0f2-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="5a0f2-108">Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de um dados Cassandra, mas não para mover dados de outro armazenamento de dados dados repositórios tooa Cassandra.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="5a0f2-109">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="5a0f2-109">Supported versions</span></span>
<span data-ttu-id="5a0f2-110">Olá Cassandra conector dá suporte a saudação seguintes versões do Cassandra: 2. x.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a0f2-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5a0f2-111">Prerequisites</span></span>
<span data-ttu-id="5a0f2-112">Saudação do Azure Data Factory serviço toobe tooconnect capaz de tooyour local Cassandra banco de dados, você deve instalar um Gateway de gerenciamento de dados em Olá mesmo esse banco de dados de saudação de hosts de máquina ou em um tooavoid máquina separada competição por recursos com hello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="5a0f2-113">Gateway de gerenciamento de dados é um componente que se conecta a serviços de toocloud de fontes de dados no local de forma segura e gerenciada.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="5a0f2-114">Confira o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter todos os detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="5a0f2-115">Consulte [mover dados de local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções passo a passo sobre como configurar o gateway de saudação um toomove do pipeline de dados.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="5a0f2-116">Você deve usar o banco de dados do hello gateway tooconnect tooa Cassandra mesmo se o banco de dados de saudação é hospedado na nuvem hello, por exemplo, em uma VM de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="5a0f2-117">Y, você pode ter um gateway de saudação em Olá VM mesmo banco de dados Olá hosts ou em uma máquina virtual separada, contanto que o gateway de saudação pode se conectar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="5a0f2-118">Quando você instalar o gateway de Olá, ele instala automaticamente um banco de dados do Microsoft Cassandra ODBC driver usado tooconnect tooCassandra.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="5a0f2-119">Portanto, você não precisa toomanually instalar qualquer driver no computador do gateway Olá ao copiar dados do banco de dados de Cassandra hello.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="5a0f2-120">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5a0f2-121">Introdução</span><span class="sxs-lookup"><span data-stu-id="5a0f2-121">Getting started</span></span>
<span data-ttu-id="5a0f2-122">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="5a0f2-123">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="5a0f2-124">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="5a0f2-125">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5a0f2-126">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="5a0f2-127">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a0f2-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="5a0f2-128">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="5a0f2-129">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="5a0f2-130">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="5a0f2-131">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="5a0f2-132">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="5a0f2-133">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados local Cassandra, consulte [exemplo JSON: copiar dados de Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="5a0f2-134">Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de Cassandra toodefine usado Data Factory entidades tooa específico:</span><span class="sxs-lookup"><span data-stu-id="5a0f2-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="5a0f2-135">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="5a0f2-135">Linked service properties</span></span>
<span data-ttu-id="5a0f2-136">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooCassandra vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="5a0f2-137">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5a0f2-137">Property</span></span> | <span data-ttu-id="5a0f2-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a0f2-138">Description</span></span> | <span data-ttu-id="5a0f2-139">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a0f2-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a0f2-140">type</span><span class="sxs-lookup"><span data-stu-id="5a0f2-140">type</span></span> |<span data-ttu-id="5a0f2-141">propriedade de tipo Hello deve ser definida como: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="5a0f2-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="5a0f2-142">Sim</span><span class="sxs-lookup"><span data-stu-id="5a0f2-142">Yes</span></span> |
| <span data-ttu-id="5a0f2-143">host</span><span class="sxs-lookup"><span data-stu-id="5a0f2-143">host</span></span> |<span data-ttu-id="5a0f2-144">Um ou mais endereços IP ou nomes de host dos servidores Cassandra.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="5a0f2-145">Especifique uma lista separada por vírgulas de endereços IP ou host nomes tooconnect tooall servidores simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="5a0f2-146">Sim</span><span class="sxs-lookup"><span data-stu-id="5a0f2-146">Yes</span></span> |
| <span data-ttu-id="5a0f2-147">porta</span><span class="sxs-lookup"><span data-stu-id="5a0f2-147">port</span></span> |<span data-ttu-id="5a0f2-148">Olá porta TCP que Olá servidor Cassandra usa toolisten para conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="5a0f2-149">Não, valor padrão: 9042</span><span class="sxs-lookup"><span data-stu-id="5a0f2-149">No, default value: 9042</span></span> |
| <span data-ttu-id="5a0f2-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="5a0f2-150">authenticationType</span></span> |<span data-ttu-id="5a0f2-151">Básica, ou Anônima</span><span class="sxs-lookup"><span data-stu-id="5a0f2-151">Basic, or Anonymous</span></span> |<span data-ttu-id="5a0f2-152">Sim</span><span class="sxs-lookup"><span data-stu-id="5a0f2-152">Yes</span></span> |
| <span data-ttu-id="5a0f2-153">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="5a0f2-153">username</span></span> |<span data-ttu-id="5a0f2-154">Especifique o nome de usuário para a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="5a0f2-155">Sim, se authenticationType é definido tooBasic.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="5a0f2-156">Senha</span><span class="sxs-lookup"><span data-stu-id="5a0f2-156">password</span></span> |<span data-ttu-id="5a0f2-157">Especifique a senha da conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-157">Specify password for hello user account.</span></span> |<span data-ttu-id="5a0f2-158">Sim, se authenticationType é definido tooBasic.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="5a0f2-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="5a0f2-159">gatewayName</span></span> |<span data-ttu-id="5a0f2-160">nome de saudação do gateway de saudação que é usado tooconnect toohello Cassandra banco de dados no local.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="5a0f2-161">Sim</span><span class="sxs-lookup"><span data-stu-id="5a0f2-161">Yes</span></span> |
| <span data-ttu-id="5a0f2-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="5a0f2-162">encryptedCredential</span></span> |<span data-ttu-id="5a0f2-163">Credencial criptografada pelo gateway hello.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="5a0f2-164">Não</span><span class="sxs-lookup"><span data-stu-id="5a0f2-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="5a0f2-165">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="5a0f2-165">Dataset properties</span></span>
<span data-ttu-id="5a0f2-166">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5a0f2-167">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="5a0f2-168">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="5a0f2-169">Olá typeProperties seção de conjunto de dados do tipo **CassandraTable** tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="5a0f2-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="5a0f2-170">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5a0f2-170">Property</span></span> | <span data-ttu-id="5a0f2-171">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a0f2-171">Description</span></span> | <span data-ttu-id="5a0f2-172">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a0f2-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a0f2-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="5a0f2-173">keyspace</span></span> |<span data-ttu-id="5a0f2-174">Nome da saudação keyspace ou esquema Cassandra banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="5a0f2-175">Sim (se a **consulta** para **CassandraSource** não estiver definida).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="5a0f2-176">tableName</span><span class="sxs-lookup"><span data-stu-id="5a0f2-176">tableName</span></span> |<span data-ttu-id="5a0f2-177">Nome da tabela de saudação no banco de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="5a0f2-178">Sim (se a **consulta** para **CassandraSource** não estiver definida).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="5a0f2-179">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="5a0f2-179">Copy activity properties</span></span>
<span data-ttu-id="5a0f2-180">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5a0f2-181">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="5a0f2-182">Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="5a0f2-183">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="5a0f2-184">Quando a fonte é do tipo **CassandraSource**, Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="5a0f2-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="5a0f2-185">Propriedade</span><span class="sxs-lookup"><span data-stu-id="5a0f2-185">Property</span></span> | <span data-ttu-id="5a0f2-186">Descrição</span><span class="sxs-lookup"><span data-stu-id="5a0f2-186">Description</span></span> | <span data-ttu-id="5a0f2-187">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="5a0f2-187">Allowed values</span></span> | <span data-ttu-id="5a0f2-188">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5a0f2-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5a0f2-189">query</span><span class="sxs-lookup"><span data-stu-id="5a0f2-189">query</span></span> |<span data-ttu-id="5a0f2-190">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="5a0f2-191">Consulta SQL-92 ou consulta CQL.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="5a0f2-192">Veja [Referência ao CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="5a0f2-193">Ao usar a consulta SQL, especifique **keyspace name.table nome** toorepresent Olá tabela tooquery.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="5a0f2-194">Não (se tableName e keyspace no conjunto de dados estiverem definidos).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="5a0f2-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="5a0f2-195">consistencyLevel</span></span> |<span data-ttu-id="5a0f2-196">nível de consistência de saudação especifica quantas réplicas deve responder a solicitação de leitura de tooa antes de retornar o aplicativo de cliente de toohello de dados.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="5a0f2-197">Verificações de Cassandra Olá número especificado de réplicas para a solicitação de leitura de saudação do toosatisfy de dados.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="5a0f2-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="5a0f2-199">Confira [Configuring data consistency (Configurando a consistência de dados)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="5a0f2-200">Não.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-200">No.</span></span> <span data-ttu-id="5a0f2-201">O valor padrão é ONE.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="5a0f2-202">Exemplo JSON: copiar dados de Cassandra tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="5a0f2-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="5a0f2-203">Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5a0f2-204">Ele mostra como dados toocopy Cassandra um local de banco de dados tooan armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="5a0f2-205">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a0f2-206">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="5a0f2-207">Ele não inclui instruções passo a passo para criar a fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="5a0f2-208">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="5a0f2-209">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a0f2-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="5a0f2-210">Um serviço vinculado do tipo [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="5a0f2-211">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="5a0f2-212">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="5a0f2-213">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="5a0f2-214">O [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [CassandraSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="5a0f2-215">**Serviço vinculado Cassandra:**</span><span class="sxs-lookup"><span data-stu-id="5a0f2-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="5a0f2-216">Este exemplo usa Olá **Cassandra** serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="5a0f2-217">Consulte [serviço vinculado de Cassandra](#linked-service-properties) seção de propriedades de saudação suportados por esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="5a0f2-218">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="5a0f2-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="5a0f2-219">**Conjunto de dados de entrada do Cassandra:**</span><span class="sxs-lookup"><span data-stu-id="5a0f2-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

<span data-ttu-id="5a0f2-220">Configuração **externo** muito**true** informa o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="5a0f2-221">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="5a0f2-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="5a0f2-222">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="5a0f2-223">**Atividade de cópia em um pipeline com origem Cassandra e coletor de Blob:**</span><span class="sxs-lookup"><span data-stu-id="5a0f2-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="5a0f2-224">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="5a0f2-225">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**CassandraSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="5a0f2-226">Consulte [propriedades de tipo RelationalSource](#copy-activity-properties) para lista de saudação de propriedades com suporte pelo Olá RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="5a0f2-227">Mapeamento de tipo para Cassandra</span><span class="sxs-lookup"><span data-stu-id="5a0f2-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="5a0f2-228">Tipo Cassandra</span><span class="sxs-lookup"><span data-stu-id="5a0f2-228">Cassandra Type</span></span> | <span data-ttu-id="5a0f2-229">Tipo baseado no .Net</span><span class="sxs-lookup"><span data-stu-id="5a0f2-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="5a0f2-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="5a0f2-230">ASCII</span></span> |<span data-ttu-id="5a0f2-231">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a0f2-231">String</span></span> |
| <span data-ttu-id="5a0f2-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="5a0f2-232">BIGINT</span></span> |<span data-ttu-id="5a0f2-233">Int64</span><span class="sxs-lookup"><span data-stu-id="5a0f2-233">Int64</span></span> |
| <span data-ttu-id="5a0f2-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="5a0f2-234">BLOB</span></span> |<span data-ttu-id="5a0f2-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="5a0f2-235">Byte[]</span></span> |
| <span data-ttu-id="5a0f2-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="5a0f2-236">BOOLEAN</span></span> |<span data-ttu-id="5a0f2-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="5a0f2-237">Boolean</span></span> |
| <span data-ttu-id="5a0f2-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="5a0f2-238">DECIMAL</span></span> |<span data-ttu-id="5a0f2-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="5a0f2-239">Decimal</span></span> |
| <span data-ttu-id="5a0f2-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="5a0f2-240">DOUBLE</span></span> |<span data-ttu-id="5a0f2-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="5a0f2-241">Double</span></span> |
| <span data-ttu-id="5a0f2-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="5a0f2-242">FLOAT</span></span> |<span data-ttu-id="5a0f2-243">Single</span><span class="sxs-lookup"><span data-stu-id="5a0f2-243">Single</span></span> |
| <span data-ttu-id="5a0f2-244">INET</span><span class="sxs-lookup"><span data-stu-id="5a0f2-244">INET</span></span> |<span data-ttu-id="5a0f2-245">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a0f2-245">String</span></span> |
| <span data-ttu-id="5a0f2-246">INT</span><span class="sxs-lookup"><span data-stu-id="5a0f2-246">INT</span></span> |<span data-ttu-id="5a0f2-247">Int32</span><span class="sxs-lookup"><span data-stu-id="5a0f2-247">Int32</span></span> |
| <span data-ttu-id="5a0f2-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="5a0f2-248">TEXT</span></span> |<span data-ttu-id="5a0f2-249">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a0f2-249">String</span></span> |
| <span data-ttu-id="5a0f2-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="5a0f2-250">TIMESTAMP</span></span> |<span data-ttu-id="5a0f2-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="5a0f2-251">DateTime</span></span> |
| <span data-ttu-id="5a0f2-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="5a0f2-252">TIMEUUID</span></span> |<span data-ttu-id="5a0f2-253">Guid</span><span class="sxs-lookup"><span data-stu-id="5a0f2-253">Guid</span></span> |
| <span data-ttu-id="5a0f2-254">UUID</span><span class="sxs-lookup"><span data-stu-id="5a0f2-254">UUID</span></span> |<span data-ttu-id="5a0f2-255">Guid</span><span class="sxs-lookup"><span data-stu-id="5a0f2-255">Guid</span></span> |
| <span data-ttu-id="5a0f2-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="5a0f2-256">VARCHAR</span></span> |<span data-ttu-id="5a0f2-257">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a0f2-257">String</span></span> |
| <span data-ttu-id="5a0f2-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="5a0f2-258">VARINT</span></span> |<span data-ttu-id="5a0f2-259">Decimal</span><span class="sxs-lookup"><span data-stu-id="5a0f2-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="5a0f2-260">Para a coleção de tipos (mapa, conjunto, lista, etc.), consulte muito[trabalhar com tipos de coleção Cassandra usando a tabela virtual](#work-with-collections-using-virtual-table) seção.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="5a0f2-261">Não há suporte para tipos definidos pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="5a0f2-262">comprimento de saudação de comprimentos de coluna binária e de colunas de cadeia de caracteres não pode ser maior que 4000.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="5a0f2-263">Trabalhar com coleções usando tabela virtual</span><span class="sxs-lookup"><span data-stu-id="5a0f2-263">Work with collections using virtual table</span></span>
<span data-ttu-id="5a0f2-264">A fábrica de dados do Azure usa um interna tooconnect tooand copiar dados do driver ODBC do banco de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="5a0f2-265">Para tipos de coleção, incluindo o mapa, conjunto e lista, o driver Olá renormalizes dados saudação em tabelas virtuais correspondentes.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="5a0f2-266">Especificamente, se uma tabela contiver colunas coleção, o driver hello gera Olá tabelas virtuais a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a0f2-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="5a0f2-267">Um **tabela base**, que contém Olá os mesmos dados que a tabela real Olá com exceção das colunas da coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="5a0f2-268">tabela base Olá usa Olá mesmo nome como tabela de saudação real que ele representa.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="5a0f2-269">Um **tabela virtual** para cada coluna de coleção, que expande dados saudação aninhado.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="5a0f2-270">tabelas virtuais de saudação que representam coleções são nomeadas usando Olá nome de tabela real hello, um separador de "*vt*" e o nome de saudação da coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="5a0f2-271">Tabelas virtuais Consulte toohello dados na tabela real hello, habilitando tooaccess de driver Olá Olá dados desnormalizados.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="5a0f2-272">Confira a seção Exemplo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-272">See Example section for details.</span></span> <span data-ttu-id="5a0f2-273">Você pode acessar o conteúdo de Olá de coleções de Cassandra ao consultar e unir tabelas virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="5a0f2-274">Você pode usar o hello [Assistente para cópia de](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively exibição Olá a lista de tabelas no banco de dados de Cassandra incluindo tabelas virtuais hello e visualizar dados hello dentro.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="5a0f2-275">Também pode criar uma consulta no Assistente para cópia de saudação e validar os resultados de saudação toosee.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="5a0f2-276">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5a0f2-276">Example</span></span>
<span data-ttu-id="5a0f2-277">Por exemplo, hello seguir "ExampleTable" é uma tabela de banco de dados de Cassandra que contém uma coluna de chave primária da inteiro chamado "pk_int", uma coluna de texto denominado valor, uma coluna de lista, uma coluna de mapa e uma coluna de conjunto (chamado de "StringSet").</span><span class="sxs-lookup"><span data-stu-id="5a0f2-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="5a0f2-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="5a0f2-278">pk_int</span></span> | <span data-ttu-id="5a0f2-279">Valor</span><span class="sxs-lookup"><span data-stu-id="5a0f2-279">Value</span></span> | <span data-ttu-id="5a0f2-280">Listar</span><span class="sxs-lookup"><span data-stu-id="5a0f2-280">List</span></span> | <span data-ttu-id="5a0f2-281">Mapa</span><span class="sxs-lookup"><span data-stu-id="5a0f2-281">Map</span></span> | <span data-ttu-id="5a0f2-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="5a0f2-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5a0f2-283">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-283">1</span></span> |<span data-ttu-id="5a0f2-284">"valor de exemplo 1"</span><span class="sxs-lookup"><span data-stu-id="5a0f2-284">"sample value 1"</span></span> |<span data-ttu-id="5a0f2-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="5a0f2-285">["1", "2", "3"]</span></span> |<span data-ttu-id="5a0f2-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="5a0f2-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="5a0f2-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="5a0f2-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="5a0f2-288">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-288">3</span></span> |<span data-ttu-id="5a0f2-289">"valor de exemplo 3"</span><span class="sxs-lookup"><span data-stu-id="5a0f2-289">"sample value 3"</span></span> |<span data-ttu-id="5a0f2-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="5a0f2-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="5a0f2-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="5a0f2-291">{"S1": "t"}</span></span> |<span data-ttu-id="5a0f2-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="5a0f2-292">{"A", "E"}</span></span> |

<span data-ttu-id="5a0f2-293">driver de saudação poderia gerar vários toorepresent de tabelas virtuais nessa única tabela.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="5a0f2-294">Olá colunas de chave estrangeira em tabelas virtuais Olá fazer referência a colunas de chave primária Olá na tabela real hello e indicar qual real linha da tabela linha hello tabela virtual corresponde à.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="5a0f2-295">primeira tabela virtual que Olá é a tabela base hello, denominada "ExampleTable" é mostrada no Olá a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="5a0f2-296">tabela base Olá contém Olá mesmo dados da tabela de banco de dados original hello, exceto as coleções de saudação, que são omitidos dessa tabela e expandidas em outras tabelas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="5a0f2-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="5a0f2-297">pk_int</span></span> | <span data-ttu-id="5a0f2-298">Valor</span><span class="sxs-lookup"><span data-stu-id="5a0f2-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="5a0f2-299">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-299">1</span></span> |<span data-ttu-id="5a0f2-300">"valor de exemplo 1"</span><span class="sxs-lookup"><span data-stu-id="5a0f2-300">"sample value 1"</span></span> |
| <span data-ttu-id="5a0f2-301">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-301">3</span></span> |<span data-ttu-id="5a0f2-302">"valor de exemplo 3"</span><span class="sxs-lookup"><span data-stu-id="5a0f2-302">"sample value 3"</span></span> |

<span data-ttu-id="5a0f2-303">Olá, tabelas a seguir mostram tabelas Olá virtual renormalize dados saudação de colunas de lista e mapa StringSet hello.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="5a0f2-304">Olá colunas com nomes que terminam com index"ou"c_have"para indicar posição Olá dos dados hello dentro da lista original hello ou um mapa.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="5a0f2-305">colunas de saudação com nomes que terminam com Value"contêm dados de saudação expandido da coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="5a0f2-306">Tabela "ExampleTable_vt_List":</span><span class="sxs-lookup"><span data-stu-id="5a0f2-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="5a0f2-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="5a0f2-307">pk_int</span></span> | <span data-ttu-id="5a0f2-308">List_index</span><span class="sxs-lookup"><span data-stu-id="5a0f2-308">List_index</span></span> | <span data-ttu-id="5a0f2-309">List_value</span><span class="sxs-lookup"><span data-stu-id="5a0f2-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a0f2-310">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-310">1</span></span> |<span data-ttu-id="5a0f2-311">0</span><span class="sxs-lookup"><span data-stu-id="5a0f2-311">0</span></span> |<span data-ttu-id="5a0f2-312">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-312">1</span></span> |
| <span data-ttu-id="5a0f2-313">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-313">1</span></span> |<span data-ttu-id="5a0f2-314">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-314">1</span></span> |<span data-ttu-id="5a0f2-315">2</span><span class="sxs-lookup"><span data-stu-id="5a0f2-315">2</span></span> |
| <span data-ttu-id="5a0f2-316">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-316">1</span></span> |<span data-ttu-id="5a0f2-317">2</span><span class="sxs-lookup"><span data-stu-id="5a0f2-317">2</span></span> |<span data-ttu-id="5a0f2-318">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-318">3</span></span> |
| <span data-ttu-id="5a0f2-319">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-319">3</span></span> |<span data-ttu-id="5a0f2-320">0</span><span class="sxs-lookup"><span data-stu-id="5a0f2-320">0</span></span> |<span data-ttu-id="5a0f2-321">100</span><span class="sxs-lookup"><span data-stu-id="5a0f2-321">100</span></span> |
| <span data-ttu-id="5a0f2-322">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-322">3</span></span> |<span data-ttu-id="5a0f2-323">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-323">1</span></span> |<span data-ttu-id="5a0f2-324">101</span><span class="sxs-lookup"><span data-stu-id="5a0f2-324">101</span></span> |
| <span data-ttu-id="5a0f2-325">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-325">3</span></span> |<span data-ttu-id="5a0f2-326">2</span><span class="sxs-lookup"><span data-stu-id="5a0f2-326">2</span></span> |<span data-ttu-id="5a0f2-327">102</span><span class="sxs-lookup"><span data-stu-id="5a0f2-327">102</span></span> |
| <span data-ttu-id="5a0f2-328">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-328">3</span></span> |<span data-ttu-id="5a0f2-329">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-329">3</span></span> |<span data-ttu-id="5a0f2-330">103</span><span class="sxs-lookup"><span data-stu-id="5a0f2-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="5a0f2-331">Tabela "ExampleTable_vt_Map":</span><span class="sxs-lookup"><span data-stu-id="5a0f2-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="5a0f2-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="5a0f2-332">pk_int</span></span> | <span data-ttu-id="5a0f2-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="5a0f2-333">Map_key</span></span> | <span data-ttu-id="5a0f2-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="5a0f2-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a0f2-335">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-335">1</span></span> |<span data-ttu-id="5a0f2-336">S1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-336">S1</span></span> |<span data-ttu-id="5a0f2-337">O </span><span class="sxs-lookup"><span data-stu-id="5a0f2-337">A</span></span> |
| <span data-ttu-id="5a0f2-338">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-338">1</span></span> |<span data-ttu-id="5a0f2-339">S2</span><span class="sxs-lookup"><span data-stu-id="5a0f2-339">S2</span></span> |<span data-ttu-id="5a0f2-340">b</span><span class="sxs-lookup"><span data-stu-id="5a0f2-340">b</span></span> |
| <span data-ttu-id="5a0f2-341">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-341">3</span></span> |<span data-ttu-id="5a0f2-342">S1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-342">S1</span></span> |<span data-ttu-id="5a0f2-343">t</span><span class="sxs-lookup"><span data-stu-id="5a0f2-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="5a0f2-344">Tabela "ExampleTable_vt_StringSet":</span><span class="sxs-lookup"><span data-stu-id="5a0f2-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="5a0f2-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="5a0f2-345">pk_int</span></span> | <span data-ttu-id="5a0f2-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="5a0f2-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="5a0f2-347">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-347">1</span></span> |<span data-ttu-id="5a0f2-348">O </span><span class="sxs-lookup"><span data-stu-id="5a0f2-348">A</span></span> |
| <span data-ttu-id="5a0f2-349">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-349">1</span></span> |<span data-ttu-id="5a0f2-350">b</span><span class="sxs-lookup"><span data-stu-id="5a0f2-350">B</span></span> |
| <span data-ttu-id="5a0f2-351">1</span><span class="sxs-lookup"><span data-stu-id="5a0f2-351">1</span></span> |<span data-ttu-id="5a0f2-352">C</span><span class="sxs-lookup"><span data-stu-id="5a0f2-352">C</span></span> |
| <span data-ttu-id="5a0f2-353">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-353">3</span></span> |<span data-ttu-id="5a0f2-354">O </span><span class="sxs-lookup"><span data-stu-id="5a0f2-354">A</span></span> |
| <span data-ttu-id="5a0f2-355">3</span><span class="sxs-lookup"><span data-stu-id="5a0f2-355">3</span></span> |<span data-ttu-id="5a0f2-356">E</span><span class="sxs-lookup"><span data-stu-id="5a0f2-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="5a0f2-357">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="5a0f2-357">Map source toosink columns</span></span>
<span data-ttu-id="5a0f2-358">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="5a0f2-359">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="5a0f2-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="5a0f2-360">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="5a0f2-361">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="5a0f2-362">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="5a0f2-363">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="5a0f2-364">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="5a0f2-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="5a0f2-365">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="5a0f2-365">Performance and Tuning</span></span>
<span data-ttu-id="5a0f2-366">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="5a0f2-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
