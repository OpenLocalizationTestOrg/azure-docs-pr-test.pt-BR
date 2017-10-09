---
title: "dados de aaaMove do MongoDB usando a fábrica de dados | Microsoft Docs"
description: Saiba mais sobre como os dados de toomove do MongoDB banco de dados usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="8f2d1-103">Mover dados do MongoDB usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8f2d1-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="8f2d1-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de um banco de dados do MongoDB no local.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="8f2d1-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="8f2d1-106">Você pode copiar dados de um repositório de dados local MongoDB dados repositório tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="8f2d1-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="8f2d1-108">Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de um dados MongoDB, mas não para mover dados de outro repositório de dados dados repositórios tooan MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8f2d1-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f2d1-109">Prerequisites</span></span>
<span data-ttu-id="8f2d1-110">Saudação do Azure Data Factory serviço toobe tooconnect capaz de tooyour local MongoDB banco de dados, você deve instalar Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f2d1-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="8f2d1-111">As versões com suporte do MongoDB são: 2.4, 2.6, 3.0 e 3.2.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="8f2d1-112">Gateway de gerenciamento de dados em Olá mesma máquina desse banco de dados de saudação de hosts ou em um tooavoid máquina separada competição por recursos com o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="8f2d1-113">Gateway de gerenciamento de dados é um software que se conecta a serviços de toocloud de fontes de dados no local de forma segura e gerenciada.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="8f2d1-114">Confira o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter todos os detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="8f2d1-115">Consulte [mover dados de local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções passo a passo sobre como configurar o gateway de saudação um toomove do pipeline de dados.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="8f2d1-116">Quando você instalar o gateway de hello, instala automaticamente um tooMongoDB de tooconnect do MongoDB do Microsoft ODBC driver usado.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8f2d1-117">É necessário toouse Olá gateway tooconnect tooMongoDB mesmo se ele estiver hospedado em VMs de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="8f2d1-118">Se você estiver tentando tooconnect tooan instância do MongoDB hospedado na nuvem, você também pode instalar instância de gateway Olá no hello IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8f2d1-119">Introdução</span><span class="sxs-lookup"><span data-stu-id="8f2d1-119">Getting started</span></span>
<span data-ttu-id="8f2d1-120">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local MongoDB usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="8f2d1-121">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="8f2d1-122">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="8f2d1-123">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8f2d1-124">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8f2d1-125">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f2d1-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="8f2d1-126">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="8f2d1-127">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="8f2d1-128">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8f2d1-129">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="8f2d1-130">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="8f2d1-131">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados do MongoDB no local, consulte [exemplo JSON: copiar dados do MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="8f2d1-132">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específicas tooMongoDB origem:</span><span class="sxs-lookup"><span data-stu-id="8f2d1-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8f2d1-133">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="8f2d1-133">Linked service properties</span></span>
<span data-ttu-id="8f2d1-134">Olá tabela a seguir fornece descrição para elementos JSON específicos muito**OnPremisesMongoDB** serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="8f2d1-135">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8f2d1-135">Property</span></span> | <span data-ttu-id="8f2d1-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f2d1-136">Description</span></span> | <span data-ttu-id="8f2d1-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8f2d1-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f2d1-138">type</span><span class="sxs-lookup"><span data-stu-id="8f2d1-138">type</span></span> |<span data-ttu-id="8f2d1-139">propriedade de tipo Hello deve ser definida como: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="8f2d1-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="8f2d1-140">Sim</span><span class="sxs-lookup"><span data-stu-id="8f2d1-140">Yes</span></span> |
| <span data-ttu-id="8f2d1-141">server</span><span class="sxs-lookup"><span data-stu-id="8f2d1-141">server</span></span> |<span data-ttu-id="8f2d1-142">IP endereço ou nome de host do servidor do MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="8f2d1-143">Sim</span><span class="sxs-lookup"><span data-stu-id="8f2d1-143">Yes</span></span> |
| <span data-ttu-id="8f2d1-144">porta</span><span class="sxs-lookup"><span data-stu-id="8f2d1-144">port</span></span> |<span data-ttu-id="8f2d1-145">Porta TCP que Olá MongoDB server usa toolisten para conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="8f2d1-146">Opcional, valor padrão: 27017</span><span class="sxs-lookup"><span data-stu-id="8f2d1-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="8f2d1-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="8f2d1-147">authenticationType</span></span> |<span data-ttu-id="8f2d1-148">Básica ou Anônima.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="8f2d1-149">Sim</span><span class="sxs-lookup"><span data-stu-id="8f2d1-149">Yes</span></span> |
| <span data-ttu-id="8f2d1-150">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="8f2d1-150">username</span></span> |<span data-ttu-id="8f2d1-151">Conta de usuário tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="8f2d1-152">Sim (se a autenticação básica for usada).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="8f2d1-153">Senha</span><span class="sxs-lookup"><span data-stu-id="8f2d1-153">password</span></span> |<span data-ttu-id="8f2d1-154">Senha do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-154">Password for hello user.</span></span> |<span data-ttu-id="8f2d1-155">Sim (se a autenticação básica for usada).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="8f2d1-156">authSource</span><span class="sxs-lookup"><span data-stu-id="8f2d1-156">authSource</span></span> |<span data-ttu-id="8f2d1-157">Nome do banco de dados do MongoDB Olá que você deseja toouse toocheck suas credenciais para autenticação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="8f2d1-158">Opcional (se a autenticação básica for usada).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="8f2d1-159">padrão: usa a conta de administrador hello e banco de dados de saudação especificado usando a propriedade databaseName.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="8f2d1-160">databaseName</span><span class="sxs-lookup"><span data-stu-id="8f2d1-160">databaseName</span></span> |<span data-ttu-id="8f2d1-161">Nome do banco de dados do MongoDB Olá que você deseja tooaccess.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="8f2d1-162">Sim</span><span class="sxs-lookup"><span data-stu-id="8f2d1-162">Yes</span></span> |
| <span data-ttu-id="8f2d1-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="8f2d1-163">gatewayName</span></span> |<span data-ttu-id="8f2d1-164">Nome do gateway de saudação que acessa o repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="8f2d1-165">Sim</span><span class="sxs-lookup"><span data-stu-id="8f2d1-165">Yes</span></span> |
| <span data-ttu-id="8f2d1-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="8f2d1-166">encryptedCredential</span></span> |<span data-ttu-id="8f2d1-167">Credencial criptografada pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="8f2d1-168">Opcional</span><span class="sxs-lookup"><span data-stu-id="8f2d1-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="8f2d1-169">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8f2d1-169">Dataset properties</span></span>
<span data-ttu-id="8f2d1-170">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8f2d1-171">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8f2d1-172">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="8f2d1-173">Olá typeProperties seção de conjunto de dados do tipo **MongoDbCollection** tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f2d1-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="8f2d1-174">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8f2d1-174">Property</span></span> | <span data-ttu-id="8f2d1-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f2d1-175">Description</span></span> | <span data-ttu-id="8f2d1-176">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8f2d1-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f2d1-177">collectionName</span><span class="sxs-lookup"><span data-stu-id="8f2d1-177">collectionName</span></span> |<span data-ttu-id="8f2d1-178">Nome da coleção de saudação no banco de dados do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="8f2d1-179">Sim</span><span class="sxs-lookup"><span data-stu-id="8f2d1-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="8f2d1-180">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="8f2d1-180">Copy activity properties</span></span>
<span data-ttu-id="8f2d1-181">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8f2d1-182">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="8f2d1-183">As propriedades disponíveis no hello **typeProperties** seção de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="8f2d1-184">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="8f2d1-185">Quando a fonte de saudação é do tipo **MongoDbSource** Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="8f2d1-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="8f2d1-186">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8f2d1-186">Property</span></span> | <span data-ttu-id="8f2d1-187">Descrição</span><span class="sxs-lookup"><span data-stu-id="8f2d1-187">Description</span></span> | <span data-ttu-id="8f2d1-188">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8f2d1-188">Allowed values</span></span> | <span data-ttu-id="8f2d1-189">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8f2d1-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8f2d1-190">query</span><span class="sxs-lookup"><span data-stu-id="8f2d1-190">query</span></span> |<span data-ttu-id="8f2d1-191">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="8f2d1-192">Cadeia de consulta SQL-92.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-192">SQL-92 query string.</span></span> <span data-ttu-id="8f2d1-193">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="8f2d1-194">Não (se **collectionName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="8f2d1-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="8f2d1-195">Exemplo JSON: copiar dados do MongoDB tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="8f2d1-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="8f2d1-196">Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8f2d1-197">Ele mostra como toocopy dados de um tooan do MongoDB local armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="8f2d1-198">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="8f2d1-199">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f2d1-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="8f2d1-200">Um serviço vinculado do tipo [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="8f2d1-201">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8f2d1-202">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="8f2d1-203">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8f2d1-204">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [MongoDbSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8f2d1-205">exemplo Hello copia dados de um resultado de consulta no blob de tooa de banco de dados do MongoDB a cada hora.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="8f2d1-206">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="8f2d1-207">Como uma primeira etapa, configurar o gateway de gerenciamento de dados de saudação de acordo com as instruções de Olá Olá [Data Management Gateway](data-factory-data-management-gateway.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="8f2d1-208">**Serviço vinculado ao MongoDB:**</span><span class="sxs-lookup"><span data-stu-id="8f2d1-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="8f2d1-209">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="8f2d1-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="8f2d1-210">**Conjunto de dados de entrada do MongoDB:** configuração "externo": "verdadeiro" informa Olá serviço de fábrica de dados tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="8f2d1-211">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="8f2d1-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8f2d1-212">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="8f2d1-213">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="8f2d1-214">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="8f2d1-215">**Uma atividade de cópia em um pipeline com origem no MongoDB e coletor Blob:**</span><span class="sxs-lookup"><span data-stu-id="8f2d1-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="8f2d1-216">pipeline de saudação contém uma atividade de cópia que é configurado toouse hello acima conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="8f2d1-217">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**MongoDbSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="8f2d1-218">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="8f2d1-219">Esquema do Data Factory</span><span class="sxs-lookup"><span data-stu-id="8f2d1-219">Schema by Data Factory</span></span>
<span data-ttu-id="8f2d1-220">Serviço de fábrica de dados do Azure infere o esquema de uma coleção do MongoDB usando documentos Olá 100 mais recente na coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="8f2d1-221">Se esses 100 documentos não contêm o esquema completo, algumas colunas podem ser ignoradas durante a operação de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="8f2d1-222">Mapeamento de tipo para o MongoDB</span><span class="sxs-lookup"><span data-stu-id="8f2d1-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="8f2d1-223">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f2d1-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="8f2d1-224">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="8f2d1-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="8f2d1-225">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="8f2d1-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="8f2d1-226">Ao mover Olá tooMongoDB de dados a seguir os mapeamentos são usados de tipos de too.NET de tipos do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="8f2d1-227">Tipo do MongoDB</span><span class="sxs-lookup"><span data-stu-id="8f2d1-227">MongoDB type</span></span> | <span data-ttu-id="8f2d1-228">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8f2d1-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="8f2d1-229">Binário</span><span class="sxs-lookup"><span data-stu-id="8f2d1-229">Binary</span></span> |<span data-ttu-id="8f2d1-230">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8f2d1-230">Byte[]</span></span> |
| <span data-ttu-id="8f2d1-231">Booliano</span><span class="sxs-lookup"><span data-stu-id="8f2d1-231">Boolean</span></span> |<span data-ttu-id="8f2d1-232">Booliano</span><span class="sxs-lookup"><span data-stu-id="8f2d1-232">Boolean</span></span> |
| <span data-ttu-id="8f2d1-233">Data</span><span class="sxs-lookup"><span data-stu-id="8f2d1-233">Date</span></span> |<span data-ttu-id="8f2d1-234">DateTime</span><span class="sxs-lookup"><span data-stu-id="8f2d1-234">DateTime</span></span> |
| <span data-ttu-id="8f2d1-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="8f2d1-235">NumberDouble</span></span> |<span data-ttu-id="8f2d1-236">Duplo</span><span class="sxs-lookup"><span data-stu-id="8f2d1-236">Double</span></span> |
| <span data-ttu-id="8f2d1-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="8f2d1-237">NumberInt</span></span> |<span data-ttu-id="8f2d1-238">Int32</span><span class="sxs-lookup"><span data-stu-id="8f2d1-238">Int32</span></span> |
| <span data-ttu-id="8f2d1-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="8f2d1-239">NumberLong</span></span> |<span data-ttu-id="8f2d1-240">Int64</span><span class="sxs-lookup"><span data-stu-id="8f2d1-240">Int64</span></span> |
| <span data-ttu-id="8f2d1-241">ObjectID</span><span class="sxs-lookup"><span data-stu-id="8f2d1-241">ObjectID</span></span> |<span data-ttu-id="8f2d1-242">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8f2d1-242">String</span></span> |
| <span data-ttu-id="8f2d1-243">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8f2d1-243">String</span></span> |<span data-ttu-id="8f2d1-244">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8f2d1-244">String</span></span> |
| <span data-ttu-id="8f2d1-245">UUID</span><span class="sxs-lookup"><span data-stu-id="8f2d1-245">UUID</span></span> |<span data-ttu-id="8f2d1-246">Guid</span><span class="sxs-lookup"><span data-stu-id="8f2d1-246">Guid</span></span> |
| <span data-ttu-id="8f2d1-247">Objeto</span><span class="sxs-lookup"><span data-stu-id="8f2d1-247">Object</span></span> |<span data-ttu-id="8f2d1-248">Renormalizado para colunas simples com “_” como separador aninhado</span><span class="sxs-lookup"><span data-stu-id="8f2d1-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="8f2d1-249">toolearn sobre o suporte para matrizes usando tabelas virtuais, consulte muito[suporte para tipos complexos usando tabelas virtuais](#support-for-complex-types-using-virtual-tables) seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="8f2d1-250">No momento, não há suporte para Olá seguintes tipos de dados do MongoDB: DBPointer, JavaScript, Max/Min chave, Expressão Regular, o símbolo, o carimbo de hora, indefinido</span><span class="sxs-lookup"><span data-stu-id="8f2d1-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="8f2d1-251">Suporte para tipos complexos usando tabelas virtuais</span><span class="sxs-lookup"><span data-stu-id="8f2d1-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="8f2d1-252">A fábrica de dados do Azure usa um internos ODBC driver tooconnect tooand copiar dados de seu banco de dados do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="8f2d1-253">Para tipos complexos, como objetos ou matrizes com tipos diferentes em documentos Olá, o driver Olá novamente normaliza dados em tabelas virtuais correspondentes.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="8f2d1-254">Especificamente, se uma tabela contiver essas colunas, o driver hello gera Olá tabelas virtuais a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f2d1-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="8f2d1-255">Um **tabela base**, que contém Olá os mesmos dados que a tabela real Olá com exceção das colunas de tipo complexo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="8f2d1-256">tabela base Olá usa Olá mesmo nome como tabela de saudação real que ele representa.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="8f2d1-257">Um **tabela virtual** para cada coluna de tipo complexo, que expande dados saudação aninhado.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="8f2d1-258">tabelas virtuais Olá são nomeadas usando nome hello da tabela real Olá, um separador "_" e o nome de saudação do objeto ou matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="8f2d1-259">Tabelas virtuais Consulte toohello dados na tabela real hello, habilitando tooaccess de driver Olá Olá dados desnormalizados.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="8f2d1-260">Veja a seção Exemplo abaixo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-260">See Example section below details.</span></span> <span data-ttu-id="8f2d1-261">Você pode acessar conteúdo de saudação do MongoDB matrizes ao consultar e unir tabelas virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="8f2d1-262">Você pode usar o hello [Assistente para cópia de](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively exibição Olá a lista de tabelas no banco de dados do MongoDB incluindo tabelas virtuais hello e visualizar dados hello dentro.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="8f2d1-263">Também pode criar uma consulta no Assistente para cópia de saudação e validar os resultados de saudação toosee.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="8f2d1-264">Exemplo</span><span class="sxs-lookup"><span data-stu-id="8f2d1-264">Example</span></span>
<span data-ttu-id="8f2d1-265">Por exemplo, "TabelaDeExemplo" abaixo é uma tabela do MongoDB com uma coluna com uma matriz de Objetos em cada célula – Faturas, e uma coluna com uma matriz de tipos escalares – Classificações.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="8f2d1-266">_id</span><span class="sxs-lookup"><span data-stu-id="8f2d1-266">_id</span></span> | <span data-ttu-id="8f2d1-267">Nome do Cliente</span><span class="sxs-lookup"><span data-stu-id="8f2d1-267">Customer Name</span></span> | <span data-ttu-id="8f2d1-268">Faturas</span><span class="sxs-lookup"><span data-stu-id="8f2d1-268">Invoices</span></span> | <span data-ttu-id="8f2d1-269">Nível de Serviço</span><span class="sxs-lookup"><span data-stu-id="8f2d1-269">Service Level</span></span> | <span data-ttu-id="8f2d1-270">Classificações</span><span class="sxs-lookup"><span data-stu-id="8f2d1-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="8f2d1-271">1111</span><span class="sxs-lookup"><span data-stu-id="8f2d1-271">1111</span></span> |<span data-ttu-id="8f2d1-272">ABC</span><span class="sxs-lookup"><span data-stu-id="8f2d1-272">ABC</span></span> |<span data-ttu-id="8f2d1-273">[{invoice_id:”123”, item:”torradeira”, price:”456”, discount:”0,2”}, {invoice_id:”124”, item:”forno”,price: ”1235”,discount: ”0,2”}]</span><span class="sxs-lookup"><span data-stu-id="8f2d1-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="8f2d1-274">Silver</span><span class="sxs-lookup"><span data-stu-id="8f2d1-274">Silver</span></span> |<span data-ttu-id="8f2d1-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="8f2d1-275">[5,6]</span></span> |
| <span data-ttu-id="8f2d1-276">2222</span><span class="sxs-lookup"><span data-stu-id="8f2d1-276">2222</span></span> |<span data-ttu-id="8f2d1-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="8f2d1-277">XYZ</span></span> |<span data-ttu-id="8f2d1-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span><span class="sxs-lookup"><span data-stu-id="8f2d1-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="8f2d1-279">Gold</span><span class="sxs-lookup"><span data-stu-id="8f2d1-279">Gold</span></span> |<span data-ttu-id="8f2d1-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="8f2d1-280">[1,2]</span></span> |

<span data-ttu-id="8f2d1-281">driver de saudação poderia gerar vários toorepresent de tabelas virtuais nessa única tabela.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="8f2d1-282">Olá primeiro virtual tabela é Olá base chamado "ExampleTable", mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="8f2d1-283">tabela base Olá contém todos os dados de saudação da tabela original hello, mas dados saudação de matrizes de saudação foi omitidos e são expandidos em tabelas virtuais hello.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="8f2d1-284">_id</span><span class="sxs-lookup"><span data-stu-id="8f2d1-284">_id</span></span> | <span data-ttu-id="8f2d1-285">Nome do Cliente</span><span class="sxs-lookup"><span data-stu-id="8f2d1-285">Customer Name</span></span> | <span data-ttu-id="8f2d1-286">Nível de Serviço</span><span class="sxs-lookup"><span data-stu-id="8f2d1-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f2d1-287">1111</span><span class="sxs-lookup"><span data-stu-id="8f2d1-287">1111</span></span> |<span data-ttu-id="8f2d1-288">ABC</span><span class="sxs-lookup"><span data-stu-id="8f2d1-288">ABC</span></span> |<span data-ttu-id="8f2d1-289">Silver</span><span class="sxs-lookup"><span data-stu-id="8f2d1-289">Silver</span></span> |
| <span data-ttu-id="8f2d1-290">2222</span><span class="sxs-lookup"><span data-stu-id="8f2d1-290">2222</span></span> |<span data-ttu-id="8f2d1-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="8f2d1-291">XYZ</span></span> |<span data-ttu-id="8f2d1-292">Gold</span><span class="sxs-lookup"><span data-stu-id="8f2d1-292">Gold</span></span> |

<span data-ttu-id="8f2d1-293">Olá tabelas a seguir mostram Olá tabelas virtuais que representam matrizes de saudação original no exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="8f2d1-294">Essas tabelas contêm seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="8f2d1-294">These tables contain hello following:</span></span>

* <span data-ttu-id="8f2d1-295">Uma referência de volta toohello coluna de chave primária correspondente toohello linha original da matriz original da saudação (por meio da coluna de ID Olá)</span><span class="sxs-lookup"><span data-stu-id="8f2d1-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="8f2d1-296">Uma indicação da posição de saudação do dados hello dentro da matriz original Olá</span><span class="sxs-lookup"><span data-stu-id="8f2d1-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="8f2d1-297">Olá expandido dados para cada elemento na matriz de saudação</span><span class="sxs-lookup"><span data-stu-id="8f2d1-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="8f2d1-298">Tabela "TabelaDeExemplo_Faturas":</span><span class="sxs-lookup"><span data-stu-id="8f2d1-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="8f2d1-299">_id</span><span class="sxs-lookup"><span data-stu-id="8f2d1-299">_id</span></span> | <span data-ttu-id="8f2d1-300">TabelaDeExemplo_Faturas_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="8f2d1-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="8f2d1-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="8f2d1-301">invoice_id</span></span> | <span data-ttu-id="8f2d1-302">item</span><span class="sxs-lookup"><span data-stu-id="8f2d1-302">item</span></span> | <span data-ttu-id="8f2d1-303">preço</span><span class="sxs-lookup"><span data-stu-id="8f2d1-303">price</span></span> | <span data-ttu-id="8f2d1-304">Desconto</span><span class="sxs-lookup"><span data-stu-id="8f2d1-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8f2d1-305">1111</span><span class="sxs-lookup"><span data-stu-id="8f2d1-305">1111</span></span> |<span data-ttu-id="8f2d1-306">0</span><span class="sxs-lookup"><span data-stu-id="8f2d1-306">0</span></span> |<span data-ttu-id="8f2d1-307">123</span><span class="sxs-lookup"><span data-stu-id="8f2d1-307">123</span></span> |<span data-ttu-id="8f2d1-308">torradeira</span><span class="sxs-lookup"><span data-stu-id="8f2d1-308">toaster</span></span> |<span data-ttu-id="8f2d1-309">456</span><span class="sxs-lookup"><span data-stu-id="8f2d1-309">456</span></span> |<span data-ttu-id="8f2d1-310">0,2</span><span class="sxs-lookup"><span data-stu-id="8f2d1-310">0.2</span></span> |
| <span data-ttu-id="8f2d1-311">1111</span><span class="sxs-lookup"><span data-stu-id="8f2d1-311">1111</span></span> |<span data-ttu-id="8f2d1-312">1</span><span class="sxs-lookup"><span data-stu-id="8f2d1-312">1</span></span> |<span data-ttu-id="8f2d1-313">124</span><span class="sxs-lookup"><span data-stu-id="8f2d1-313">124</span></span> |<span data-ttu-id="8f2d1-314">forno</span><span class="sxs-lookup"><span data-stu-id="8f2d1-314">oven</span></span> |<span data-ttu-id="8f2d1-315">1235</span><span class="sxs-lookup"><span data-stu-id="8f2d1-315">1235</span></span> |<span data-ttu-id="8f2d1-316">0,2</span><span class="sxs-lookup"><span data-stu-id="8f2d1-316">0.2</span></span> |
| <span data-ttu-id="8f2d1-317">2222</span><span class="sxs-lookup"><span data-stu-id="8f2d1-317">2222</span></span> |<span data-ttu-id="8f2d1-318">0</span><span class="sxs-lookup"><span data-stu-id="8f2d1-318">0</span></span> |<span data-ttu-id="8f2d1-319">135</span><span class="sxs-lookup"><span data-stu-id="8f2d1-319">135</span></span> |<span data-ttu-id="8f2d1-320">geladeira</span><span class="sxs-lookup"><span data-stu-id="8f2d1-320">fridge</span></span> |<span data-ttu-id="8f2d1-321">12543</span><span class="sxs-lookup"><span data-stu-id="8f2d1-321">12543</span></span> |<span data-ttu-id="8f2d1-322">0,0</span><span class="sxs-lookup"><span data-stu-id="8f2d1-322">0.0</span></span> |

<span data-ttu-id="8f2d1-323">Tabela "TabelaDeExemplo_Classificações":</span><span class="sxs-lookup"><span data-stu-id="8f2d1-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="8f2d1-324">_id</span><span class="sxs-lookup"><span data-stu-id="8f2d1-324">_id</span></span> | <span data-ttu-id="8f2d1-325">TabelaDeExemplo_Classificações_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="8f2d1-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="8f2d1-326">TabelaDeExemplo_Classificações</span><span class="sxs-lookup"><span data-stu-id="8f2d1-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8f2d1-327">1111</span><span class="sxs-lookup"><span data-stu-id="8f2d1-327">1111</span></span> |<span data-ttu-id="8f2d1-328">0</span><span class="sxs-lookup"><span data-stu-id="8f2d1-328">0</span></span> |<span data-ttu-id="8f2d1-329">5</span><span class="sxs-lookup"><span data-stu-id="8f2d1-329">5</span></span> |
| <span data-ttu-id="8f2d1-330">1111</span><span class="sxs-lookup"><span data-stu-id="8f2d1-330">1111</span></span> |<span data-ttu-id="8f2d1-331">1</span><span class="sxs-lookup"><span data-stu-id="8f2d1-331">1</span></span> |<span data-ttu-id="8f2d1-332">6</span><span class="sxs-lookup"><span data-stu-id="8f2d1-332">6</span></span> |
| <span data-ttu-id="8f2d1-333">2222</span><span class="sxs-lookup"><span data-stu-id="8f2d1-333">2222</span></span> |<span data-ttu-id="8f2d1-334">0</span><span class="sxs-lookup"><span data-stu-id="8f2d1-334">0</span></span> |<span data-ttu-id="8f2d1-335">1</span><span class="sxs-lookup"><span data-stu-id="8f2d1-335">1</span></span> |
| <span data-ttu-id="8f2d1-336">2222</span><span class="sxs-lookup"><span data-stu-id="8f2d1-336">2222</span></span> |<span data-ttu-id="8f2d1-337">1</span><span class="sxs-lookup"><span data-stu-id="8f2d1-337">1</span></span> |<span data-ttu-id="8f2d1-338">2</span><span class="sxs-lookup"><span data-stu-id="8f2d1-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="8f2d1-339">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="8f2d1-339">Map source toosink columns</span></span>
<span data-ttu-id="8f2d1-340">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="8f2d1-341">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="8f2d1-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="8f2d1-342">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="8f2d1-343">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="8f2d1-344">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="8f2d1-345">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="8f2d1-346">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="8f2d1-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8f2d1-347">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="8f2d1-347">Performance and Tuning</span></span>
<span data-ttu-id="8f2d1-348">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f2d1-349">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f2d1-349">Next Steps</span></span>
<span data-ttu-id="8f2d1-350">Consulte [mover dados entre locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) do artigo para obter instruções passo a passo para criar um pipeline de dados que move dados de um local de dados armazenam tooan repositório de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f2d1-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
