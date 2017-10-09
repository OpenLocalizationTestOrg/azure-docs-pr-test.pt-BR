---
title: dados de aaaMove do SAP Business Warehouse usando o Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre como toomove dados do SAP Business Warehouse utilizando a fábrica de dados do Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="0af58-103">Mover dados do SAP Business Warehouse usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0af58-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="0af58-104">Este artigo explica como toouse hello atividade de cópia de dados do Azure Data Factory toomove de um local SAP Business Warehouse (BW).</span><span class="sxs-lookup"><span data-stu-id="0af58-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="0af58-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af58-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="0af58-106">Você pode copiar dados de um repositório de dados local do SAP Business Warehouse dados repositório tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="0af58-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="0af58-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="0af58-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0af58-108">Fábrica de dados atualmente oferece suporte somente a movimentação de dados de um tooother de dados do SAP Business Warehouse armazena, mas não para mover dados de outros dados armazena tooan SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0af58-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="0af58-109">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="0af58-109">Supported versions and installation</span></span>
<span data-ttu-id="0af58-110">Este conector dá suporte ao SAP Business Warehouse versão 7.x.</span><span class="sxs-lookup"><span data-stu-id="0af58-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="0af58-111">Ele oferece suporte à cópia de dados do InfoCubes e QueryCubes (incluindo consultas BEx) usando consultas MDX.</span><span class="sxs-lookup"><span data-stu-id="0af58-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="0af58-112">tooenable Olá conectividade toohello instância SAP BW, instale Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af58-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="0af58-113">**Gateway de gerenciamento de dados**: Data Factory serviço oferece suporte à conexão de dados locais tooon repositórios (incluindo SAP Business Warehouse) usando um componente denominado Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="0af58-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="0af58-114">toolearn sobre o Gateway de gerenciamento de dados e instruções passo a passo para configurar o gateway hello, consulte [toocloud repositório de dados de repositório de dados movendo entre dados locais](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0af58-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="0af58-115">Gateway é necessário mesmo se Olá SAP Business Warehouse estiver hospedado em uma máquina virtual de IaaS do Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="0af58-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="0af58-116">Você pode instalar o gateway de saudação em Olá mesma VM como dados Olá armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0af58-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="0af58-117">**Biblioteca do SAP NetWeaver** no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="0af58-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="0af58-118">Você pode obter a biblioteca do SAP Netweaver saudação do administrador do SAP ou diretamente do hello [Centro de Download de Software SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="0af58-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="0af58-119">Pesquise Olá **SAP Observação #1025361** local de download de saudação tooget para a versão mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="0af58-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="0af58-120">Certifique-se de que a arquitetura Olá para a biblioteca do SAP NetWeaver hello (32 bits ou 64 bits) corresponde à sua instalação de gateway.</span><span class="sxs-lookup"><span data-stu-id="0af58-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="0af58-121">Instale todos os arquivos incluídos no toohello acordo do SAP NetWeaver RFC SDK de saudação nota da SAP.</span><span class="sxs-lookup"><span data-stu-id="0af58-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="0af58-122">biblioteca do SAP NetWeaver Olá também está incluída no hello instalação das ferramentas de cliente do SAP.</span><span class="sxs-lookup"><span data-stu-id="0af58-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="0af58-123">Coloque dlls Olá extraídos da saudação SDK de RFC NetWeaver na pasta system32.</span><span class="sxs-lookup"><span data-stu-id="0af58-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0af58-124">Introdução</span><span class="sxs-lookup"><span data-stu-id="0af58-124">Getting started</span></span>
<span data-ttu-id="0af58-125">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="0af58-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="0af58-126">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="0af58-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="0af58-127">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="0af58-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="0af58-128">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="0af58-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0af58-129">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0af58-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0af58-130">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af58-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="0af58-131">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="0af58-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="0af58-132">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="0af58-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="0af58-133">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="0af58-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0af58-134">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="0af58-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="0af58-135">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af58-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="0af58-136">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um local SAP Business Warehouse, consulte [exemplo JSON: copiar dados do SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="0af58-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="0af58-137">Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de SAP BW toodefine usado Data Factory entidades tooan específico:</span><span class="sxs-lookup"><span data-stu-id="0af58-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0af58-138">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="0af58-138">Linked service properties</span></span>
<span data-ttu-id="0af58-139">Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooSAP Business Warehouse (BW) vinculado de serviço.</span><span class="sxs-lookup"><span data-stu-id="0af58-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="0af58-140">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0af58-140">Property</span></span> | <span data-ttu-id="0af58-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="0af58-141">Description</span></span> | <span data-ttu-id="0af58-142">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0af58-142">Allowed values</span></span> | <span data-ttu-id="0af58-143">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0af58-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="0af58-144">server</span><span class="sxs-lookup"><span data-stu-id="0af58-144">server</span></span> | <span data-ttu-id="0af58-145">Nome do servidor de saudação no qual Olá SAP BW instância reside.</span><span class="sxs-lookup"><span data-stu-id="0af58-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="0af58-146">string</span><span class="sxs-lookup"><span data-stu-id="0af58-146">string</span></span> | <span data-ttu-id="0af58-147">Sim</span><span class="sxs-lookup"><span data-stu-id="0af58-147">Yes</span></span>
<span data-ttu-id="0af58-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="0af58-148">systemNumber</span></span> | <span data-ttu-id="0af58-149">Número de sistema de saudação sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0af58-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="0af58-150">Número decimal de dois dígitos representado como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0af58-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="0af58-151">Sim</span><span class="sxs-lookup"><span data-stu-id="0af58-151">Yes</span></span>
<span data-ttu-id="0af58-152">clientId</span><span class="sxs-lookup"><span data-stu-id="0af58-152">clientId</span></span> | <span data-ttu-id="0af58-153">ID do cliente do cliente Olá Olá sistema SAP W.</span><span class="sxs-lookup"><span data-stu-id="0af58-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="0af58-154">Número decimal de três dígitos representado como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0af58-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="0af58-155">Sim</span><span class="sxs-lookup"><span data-stu-id="0af58-155">Yes</span></span>
<span data-ttu-id="0af58-156">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="0af58-156">username</span></span> | <span data-ttu-id="0af58-157">Nome de usuário de saudação que tem acesso toohello SAP server</span><span class="sxs-lookup"><span data-stu-id="0af58-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="0af58-158">string</span><span class="sxs-lookup"><span data-stu-id="0af58-158">string</span></span> | <span data-ttu-id="0af58-159">Sim</span><span class="sxs-lookup"><span data-stu-id="0af58-159">Yes</span></span>
<span data-ttu-id="0af58-160">Senha</span><span class="sxs-lookup"><span data-stu-id="0af58-160">password</span></span> | <span data-ttu-id="0af58-161">Senha do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="0af58-161">Password for hello user.</span></span> | <span data-ttu-id="0af58-162">string</span><span class="sxs-lookup"><span data-stu-id="0af58-162">string</span></span> | <span data-ttu-id="0af58-163">Sim</span><span class="sxs-lookup"><span data-stu-id="0af58-163">Yes</span></span>
<span data-ttu-id="0af58-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0af58-164">gatewayName</span></span> | <span data-ttu-id="0af58-165">Nome do gateway Olá Olá serviço da fábrica de dados deve usar a instância de SAP BW tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="0af58-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="0af58-166">string</span><span class="sxs-lookup"><span data-stu-id="0af58-166">string</span></span> | <span data-ttu-id="0af58-167">Sim</span><span class="sxs-lookup"><span data-stu-id="0af58-167">Yes</span></span>
<span data-ttu-id="0af58-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="0af58-168">encryptedCredential</span></span> | <span data-ttu-id="0af58-169">cadeia de caracteres de credencial Olá criptografado.</span><span class="sxs-lookup"><span data-stu-id="0af58-169">hello encrypted credential string.</span></span> | <span data-ttu-id="0af58-170">string</span><span class="sxs-lookup"><span data-stu-id="0af58-170">string</span></span> | <span data-ttu-id="0af58-171">Não</span><span class="sxs-lookup"><span data-stu-id="0af58-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="0af58-172">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="0af58-172">Dataset properties</span></span>
<span data-ttu-id="0af58-173">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0af58-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0af58-174">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="0af58-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0af58-175">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af58-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="0af58-176">Não existem propriedades específicas do tipo de suporte para o conjunto de dados de SAP BW de saudação do tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0af58-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="0af58-177">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0af58-177">Copy activity properties</span></span>
<span data-ttu-id="0af58-178">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0af58-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0af58-179">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="0af58-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="0af58-180">Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="0af58-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="0af58-181">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="0af58-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="0af58-182">Quando a fonte na atividade de cópia é do tipo **RelationalSource** (que inclui o SAP BW), Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="0af58-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="0af58-183">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0af58-183">Property</span></span> | <span data-ttu-id="0af58-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="0af58-184">Description</span></span> | <span data-ttu-id="0af58-185">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0af58-185">Allowed values</span></span> | <span data-ttu-id="0af58-186">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0af58-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0af58-187">query</span><span class="sxs-lookup"><span data-stu-id="0af58-187">query</span></span> | <span data-ttu-id="0af58-188">Especifica Olá MDX consulta tooread dados da instância do SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="0af58-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="0af58-189">Consulta MDX.</span><span class="sxs-lookup"><span data-stu-id="0af58-189">MDX query.</span></span> | <span data-ttu-id="0af58-190">Sim</span><span class="sxs-lookup"><span data-stu-id="0af58-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="0af58-191">Exemplo JSON: copiar dados do SAP Business Warehouse tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="0af58-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="0af58-192">Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0af58-193">Este exemplo mostra como toocopy dados de um tooan do SAP Business Warehouse local armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0af58-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="0af58-194">No entanto, os dados podem ser copiados **diretamente** tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="0af58-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0af58-195">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="0af58-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="0af58-196">Ele não inclui instruções passo a passo para criar a fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="0af58-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="0af58-197">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0af58-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="0af58-198">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af58-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="0af58-199">Um serviço vinculado do tipo [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0af58-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="0af58-200">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0af58-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0af58-201">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0af58-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="0af58-202">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0af58-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0af58-203">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0af58-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0af58-204">exemplo Hello copia dados de uma instância de SAP Business Warehouse tooan BLOBs do Azure por hora.</span><span class="sxs-lookup"><span data-stu-id="0af58-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="0af58-205">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af58-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="0af58-206">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af58-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="0af58-207">Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="0af58-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="0af58-208">Serviço vinculado do SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="0af58-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="0af58-209">Isso vinculado links serviço sua fábrica de dados do SAP BW instância toohello.</span><span class="sxs-lookup"><span data-stu-id="0af58-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="0af58-210">propriedade do tipo Hello está definida muito**SapBw**.</span><span class="sxs-lookup"><span data-stu-id="0af58-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="0af58-211">seção de typeProperties Olá fornece informações de conexão para a instância do SAP BW hello.</span><span class="sxs-lookup"><span data-stu-id="0af58-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="0af58-212">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0af58-212">Azure Storage linked service</span></span>
<span data-ttu-id="0af58-213">Isso vinculado links serviço sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0af58-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="0af58-214">propriedade do tipo Hello está definida muito**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="0af58-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="0af58-215">seção de typeProperties Olá fornece informações de conexão para Olá conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0af58-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="0af58-216">Conjunto de dados de entrada do SAP BW</span><span class="sxs-lookup"><span data-stu-id="0af58-216">SAP BW input dataset</span></span>
<span data-ttu-id="0af58-217">Este conjunto de dados define o conjunto de dados do hello SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0af58-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="0af58-218">Defina o tipo de saudação do conjunto de dados de Data Factory Olá muito**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0af58-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="0af58-219">No momento, você não especifica quaisquer propriedades específicas ao tipo para um conjunto de dados do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0af58-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="0af58-220">consulta de saudação na definição de atividade de cópia de saudação especifica quais tooread dados da instância do SAP BW Olá.</span><span class="sxs-lookup"><span data-stu-id="0af58-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="0af58-221">Definindo a propriedade externa tootrue informa o serviço de fábrica de dados de saudação tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="0af58-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="0af58-222">Propriedades de frequência e intervalo define a agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="0af58-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="0af58-223">Nesse caso, dados saudação é lido da instância do SAP BW Olá por hora.</span><span class="sxs-lookup"><span data-stu-id="0af58-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="0af58-224">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="0af58-224">Azure Blob output dataset</span></span>
<span data-ttu-id="0af58-225">Este conjunto de dados define o conjunto de dados de Blob do Azure de saída hello.</span><span class="sxs-lookup"><span data-stu-id="0af58-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="0af58-226">propriedade de tipo de saudação é definida tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="0af58-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="0af58-227">seção de typeProperties Olá fornece onde Olá dados copiados da instância do SAP BW Olá são armazenados.</span><span class="sxs-lookup"><span data-stu-id="0af58-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="0af58-228">Olá os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="0af58-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0af58-229">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="0af58-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="0af58-230">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="0af58-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="0af58-231">Pipeline com Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0af58-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="0af58-232">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0af58-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="0af58-233">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** (de origem SAP BW) e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0af58-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="0af58-234">consulta de saudação especificada para hello **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="0af58-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="0af58-235">Mapeamento de tipo para SAP BW</span><span class="sxs-lookup"><span data-stu-id="0af58-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="0af58-236">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0af58-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="0af58-237">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="0af58-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="0af58-238">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="0af58-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="0af58-239">Ao mover dados do SAP BW, Olá mapeamentos a seguir é usado de tipos de too.NET de tipos do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0af58-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="0af58-240">Tipo de dados no hello ABAP dicionário</span><span class="sxs-lookup"><span data-stu-id="0af58-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="0af58-241">Tipo de Dados do .NET</span><span class="sxs-lookup"><span data-stu-id="0af58-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="0af58-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="0af58-242">ACCP</span></span> |  <span data-ttu-id="0af58-243">int</span><span class="sxs-lookup"><span data-stu-id="0af58-243">Int</span></span>
<span data-ttu-id="0af58-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="0af58-244">CHAR</span></span> | <span data-ttu-id="0af58-245">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0af58-245">String</span></span>
<span data-ttu-id="0af58-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="0af58-246">CLNT</span></span> | <span data-ttu-id="0af58-247">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0af58-247">String</span></span>
<span data-ttu-id="0af58-248">CURR</span><span class="sxs-lookup"><span data-stu-id="0af58-248">CURR</span></span> | <span data-ttu-id="0af58-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="0af58-249">Decimal</span></span>
<span data-ttu-id="0af58-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="0af58-250">CUKY</span></span> | <span data-ttu-id="0af58-251">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0af58-251">String</span></span>
<span data-ttu-id="0af58-252">DEC</span><span class="sxs-lookup"><span data-stu-id="0af58-252">DEC</span></span> | <span data-ttu-id="0af58-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="0af58-253">Decimal</span></span>
<span data-ttu-id="0af58-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="0af58-254">FLTP</span></span> | <span data-ttu-id="0af58-255">Duplo</span><span class="sxs-lookup"><span data-stu-id="0af58-255">Double</span></span>
<span data-ttu-id="0af58-256">INT1</span><span class="sxs-lookup"><span data-stu-id="0af58-256">INT1</span></span> | <span data-ttu-id="0af58-257">Byte</span><span class="sxs-lookup"><span data-stu-id="0af58-257">Byte</span></span>
<span data-ttu-id="0af58-258">INT2</span><span class="sxs-lookup"><span data-stu-id="0af58-258">INT2</span></span> | <span data-ttu-id="0af58-259">Int16</span><span class="sxs-lookup"><span data-stu-id="0af58-259">Int16</span></span>
<span data-ttu-id="0af58-260">INT4</span><span class="sxs-lookup"><span data-stu-id="0af58-260">INT4</span></span> | <span data-ttu-id="0af58-261">int</span><span class="sxs-lookup"><span data-stu-id="0af58-261">Int</span></span>
<span data-ttu-id="0af58-262">LANG</span><span class="sxs-lookup"><span data-stu-id="0af58-262">LANG</span></span> | <span data-ttu-id="0af58-263">string</span><span class="sxs-lookup"><span data-stu-id="0af58-263">String</span></span>
<span data-ttu-id="0af58-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="0af58-264">LCHR</span></span> | <span data-ttu-id="0af58-265">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0af58-265">String</span></span>
<span data-ttu-id="0af58-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="0af58-266">LRAW</span></span> | <span data-ttu-id="0af58-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0af58-267">Byte[]</span></span>
<span data-ttu-id="0af58-268">PREC</span><span class="sxs-lookup"><span data-stu-id="0af58-268">PREC</span></span> | <span data-ttu-id="0af58-269">Int16</span><span class="sxs-lookup"><span data-stu-id="0af58-269">Int16</span></span>
<span data-ttu-id="0af58-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="0af58-270">QUAN</span></span> | <span data-ttu-id="0af58-271">Decimal</span><span class="sxs-lookup"><span data-stu-id="0af58-271">Decimal</span></span>
<span data-ttu-id="0af58-272">RAW</span><span class="sxs-lookup"><span data-stu-id="0af58-272">RAW</span></span> | <span data-ttu-id="0af58-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0af58-273">Byte[]</span></span>
<span data-ttu-id="0af58-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="0af58-274">RAWSTRING</span></span> | <span data-ttu-id="0af58-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0af58-275">Byte[]</span></span>
<span data-ttu-id="0af58-276">STRING</span><span class="sxs-lookup"><span data-stu-id="0af58-276">STRING</span></span> | <span data-ttu-id="0af58-277">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0af58-277">String</span></span>
<span data-ttu-id="0af58-278">UNIDADE</span><span class="sxs-lookup"><span data-stu-id="0af58-278">UNIT</span></span> | <span data-ttu-id="0af58-279">string</span><span class="sxs-lookup"><span data-stu-id="0af58-279">String</span></span>
<span data-ttu-id="0af58-280">DATS</span><span class="sxs-lookup"><span data-stu-id="0af58-280">DATS</span></span> | <span data-ttu-id="0af58-281">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0af58-281">String</span></span>
<span data-ttu-id="0af58-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="0af58-282">NUMC</span></span> | <span data-ttu-id="0af58-283">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0af58-283">String</span></span>
<span data-ttu-id="0af58-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="0af58-284">TIMS</span></span> | <span data-ttu-id="0af58-285">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0af58-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="0af58-286">colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="0af58-287">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="0af58-287">Map source toosink columns</span></span>
<span data-ttu-id="0af58-288">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="0af58-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="0af58-289">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="0af58-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="0af58-290">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="0af58-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="0af58-291">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="0af58-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="0af58-292">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="0af58-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="0af58-293">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="0af58-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="0af58-294">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="0af58-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0af58-295">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="0af58-295">Performance and Tuning</span></span>
<span data-ttu-id="0af58-296">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="0af58-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
