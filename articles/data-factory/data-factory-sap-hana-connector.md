---
title: aaaMove dados de uso do Azure Data Factory do SAP HANA | Microsoft Docs
description: "Saiba mais sobre como toomove dados do SAP HANA utilizando a fábrica de dados do Azure."
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="2b7d9-103">Mover dados do SAP HANA usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2b7d9-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="2b7d9-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de um local SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="2b7d9-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="2b7d9-106">Você pode copiar dados de um repositório de dados local SAP HANA dados repositório tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="2b7d9-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2b7d9-108">Fábrica de dados atualmente oferece suporte somente a movimentação de dados de um tooother de dados do SAP HANA armazena, mas não para mover dados de outros dados armazena tooan SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="2b7d9-109">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="2b7d9-109">Supported versions and installation</span></span>
<span data-ttu-id="2b7d9-110">Esse conector oferece suporte a qualquer versão do banco de dados SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="2b7d9-111">Ele oferece suporte à cópia de dados dos modelos de informações do HANA (como os modos de exibição de Análise e de Cálculo) e às tabelas Linha/Coluna usando consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="2b7d9-112">tooenable Olá conectividade toohello instância SAP HANA, instale Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b7d9-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="2b7d9-113">**Gateway de gerenciamento de dados**: Data Factory serviço oferece suporte à conexão de dados locais tooon repositórios (incluindo SAP HANA) usando um componente denominado Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="2b7d9-114">toolearn sobre o Gateway de gerenciamento de dados e instruções passo a passo para configurar o gateway hello, consulte [toocloud repositório de dados de repositório de dados movendo entre dados locais](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="2b7d9-115">Gateway é necessário mesmo se Olá SAP HANA estiver hospedado em uma máquina virtual de IaaS do Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="2b7d9-116">Você pode instalar o gateway de saudação em Olá mesma VM como dados Olá armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="2b7d9-117">**Driver ODBC do SAP HANA** no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="2b7d9-118">Você pode baixar o driver de ODBC do SAP HANA saudação do hello [Centro de Download de Software SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="2b7d9-119">Pesquisa de palavra-chave de saudação **SAP HANA CLIENT para Windows**.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="2b7d9-120">Introdução</span><span class="sxs-lookup"><span data-stu-id="2b7d9-120">Getting started</span></span>
<span data-ttu-id="2b7d9-121">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="2b7d9-122">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="2b7d9-123">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="2b7d9-124">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2b7d9-125">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2b7d9-126">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b7d9-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="2b7d9-127">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="2b7d9-128">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="2b7d9-129">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2b7d9-130">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="2b7d9-131">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="2b7d9-132">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um local SAP HANA, consulte [exemplo JSON: copiar dados do SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2b7d9-133">Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de SAP HANA toodefine usado Data Factory entidades tooan específico:</span><span class="sxs-lookup"><span data-stu-id="2b7d9-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2b7d9-134">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="2b7d9-134">Linked service properties</span></span>
<span data-ttu-id="2b7d9-135">Olá, a tabela a seguir fornece o serviço vinculado de descrição de JSON de elementos específico tooSAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="2b7d9-136">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2b7d9-136">Property</span></span> | <span data-ttu-id="2b7d9-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b7d9-137">Description</span></span> | <span data-ttu-id="2b7d9-138">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="2b7d9-138">Allowed values</span></span> | <span data-ttu-id="2b7d9-139">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2b7d9-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="2b7d9-140">server</span><span class="sxs-lookup"><span data-stu-id="2b7d9-140">server</span></span> | <span data-ttu-id="2b7d9-141">Nome do servidor de saudação no qual Olá SAP HANA instância reside.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="2b7d9-142">Se o servidor estiver usando uma porta personalizada, especifique `server:port`.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="2b7d9-143">string</span><span class="sxs-lookup"><span data-stu-id="2b7d9-143">string</span></span> | <span data-ttu-id="2b7d9-144">Sim</span><span class="sxs-lookup"><span data-stu-id="2b7d9-144">Yes</span></span>
<span data-ttu-id="2b7d9-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2b7d9-145">authenticationType</span></span> | <span data-ttu-id="2b7d9-146">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-146">Type of authentication.</span></span> | <span data-ttu-id="2b7d9-147">cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-147">string.</span></span> <span data-ttu-id="2b7d9-148">"Básico" ou "Windows"</span><span class="sxs-lookup"><span data-stu-id="2b7d9-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="2b7d9-149">Sim</span><span class="sxs-lookup"><span data-stu-id="2b7d9-149">Yes</span></span> 
<span data-ttu-id="2b7d9-150">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="2b7d9-150">username</span></span> | <span data-ttu-id="2b7d9-151">Nome de usuário de saudação que tem acesso toohello SAP server</span><span class="sxs-lookup"><span data-stu-id="2b7d9-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="2b7d9-152">string</span><span class="sxs-lookup"><span data-stu-id="2b7d9-152">string</span></span> | <span data-ttu-id="2b7d9-153">Sim</span><span class="sxs-lookup"><span data-stu-id="2b7d9-153">Yes</span></span>
<span data-ttu-id="2b7d9-154">Senha</span><span class="sxs-lookup"><span data-stu-id="2b7d9-154">password</span></span> | <span data-ttu-id="2b7d9-155">Senha do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-155">Password for hello user.</span></span> | <span data-ttu-id="2b7d9-156">string</span><span class="sxs-lookup"><span data-stu-id="2b7d9-156">string</span></span> | <span data-ttu-id="2b7d9-157">Sim</span><span class="sxs-lookup"><span data-stu-id="2b7d9-157">Yes</span></span>
<span data-ttu-id="2b7d9-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2b7d9-158">gatewayName</span></span> | <span data-ttu-id="2b7d9-159">Nome do gateway Olá Olá serviço da fábrica de dados deve usar a instância de SAP HANA tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="2b7d9-160">string</span><span class="sxs-lookup"><span data-stu-id="2b7d9-160">string</span></span> | <span data-ttu-id="2b7d9-161">Sim</span><span class="sxs-lookup"><span data-stu-id="2b7d9-161">Yes</span></span>
<span data-ttu-id="2b7d9-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="2b7d9-162">encryptedCredential</span></span> | <span data-ttu-id="2b7d9-163">cadeia de caracteres de credencial Olá criptografado.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-163">hello encrypted credential string.</span></span> | <span data-ttu-id="2b7d9-164">string</span><span class="sxs-lookup"><span data-stu-id="2b7d9-164">string</span></span> | <span data-ttu-id="2b7d9-165">Não</span><span class="sxs-lookup"><span data-stu-id="2b7d9-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="2b7d9-166">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="2b7d9-166">Dataset properties</span></span>
<span data-ttu-id="2b7d9-167">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2b7d9-168">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2b7d9-169">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="2b7d9-170">Não existem propriedades específicas do tipo de suporte para o dataset do SAP HANA saudação do tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="2b7d9-171">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="2b7d9-171">Copy activity properties</span></span>
<span data-ttu-id="2b7d9-172">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2b7d9-173">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="2b7d9-174">Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="2b7d9-175">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="2b7d9-176">Quando a fonte na atividade de cópia é do tipo **RelationalSource** (que inclui o SAP HANA), Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="2b7d9-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="2b7d9-177">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2b7d9-177">Property</span></span> | <span data-ttu-id="2b7d9-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="2b7d9-178">Description</span></span> | <span data-ttu-id="2b7d9-179">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="2b7d9-179">Allowed values</span></span> | <span data-ttu-id="2b7d9-180">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2b7d9-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2b7d9-181">query</span><span class="sxs-lookup"><span data-stu-id="2b7d9-181">query</span></span> | <span data-ttu-id="2b7d9-182">Especifica Olá SQL consulta tooread dados da instância do SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="2b7d9-183">Consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-183">SQL query.</span></span> | <span data-ttu-id="2b7d9-184">Sim</span><span class="sxs-lookup"><span data-stu-id="2b7d9-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="2b7d9-185">Exemplo JSON: copiar dados do SAP HANA tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="2b7d9-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="2b7d9-186">Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2b7d9-187">Este exemplo mostra como toocopy dados de um tooan do SAP HANA local armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="2b7d9-188">No entanto, os dados podem ser copiados **diretamente** tooany de Coletores Olá listados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="2b7d9-189">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="2b7d9-190">Ele não inclui instruções passo a passo para criar a fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="2b7d9-191">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="2b7d9-192">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b7d9-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="2b7d9-193">Um serviço vinculado do tipo [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="2b7d9-194">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2b7d9-195">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="2b7d9-196">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2b7d9-197">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2b7d9-198">exemplo Hello copia dados de uma instância de SAP HANA tooan BLOBs do Azure por hora.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="2b7d9-199">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="2b7d9-200">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="2b7d9-201">Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="2b7d9-202">Serviço vinculado SAP HANA</span><span class="sxs-lookup"><span data-stu-id="2b7d9-202">SAP HANA linked service</span></span>
<span data-ttu-id="2b7d9-203">Isso vinculado links serviço sua fábrica de dados SAP HANA toohello de instância.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="2b7d9-204">propriedade do tipo Hello está definida muito**SapHana**.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="2b7d9-205">seção de typeProperties Olá fornece informações de conexão para a instância do SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="2b7d9-206">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2b7d9-206">Azure Storage linked service</span></span>
<span data-ttu-id="2b7d9-207">Isso vinculado links serviço sua fábrica de dados de toohello de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="2b7d9-208">propriedade do tipo Hello está definida muito**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="2b7d9-209">seção de typeProperties Olá fornece informações de conexão para Olá conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="2b7d9-210">Conjunto de dados de entrada do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="2b7d9-210">SAP HANA input dataset</span></span>

<span data-ttu-id="2b7d9-211">Este conjunto de dados define o conjunto de dados do hello SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="2b7d9-212">Defina o tipo de saudação do conjunto de dados de Data Factory Olá muito**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="2b7d9-213">No momento, você não especifica quaisquer propriedades específicas ao tipo para um conjunto de dados do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="2b7d9-214">consulta de saudação na definição de atividade de cópia de saudação especifica quais tooread dados da instância do SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="2b7d9-215">Definindo a propriedade externa tootrue informa o serviço de fábrica de dados de saudação tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="2b7d9-216">Propriedades de frequência e intervalo define a agenda de saudação.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="2b7d9-217">Nesse caso, dados saudação é lido da instância do SAP HANA Olá por hora.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="2b7d9-218">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="2b7d9-218">Azure Blob output dataset</span></span>
<span data-ttu-id="2b7d9-219">Este conjunto de dados define o conjunto de dados de Blob do Azure de saída hello.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="2b7d9-220">propriedade de tipo de saudação é definida tooAzureBlob.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="2b7d9-221">seção de typeProperties Olá fornece onde Olá dados copiados da instância do SAP HANA Olá são armazenados.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="2b7d9-222">Olá os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2b7d9-223">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="2b7d9-224">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="2b7d9-225">Pipeline com Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="2b7d9-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="2b7d9-226">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="2b7d9-227">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** (de origem do SAP HANA) e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="2b7d9-228">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="2b7d9-229">Mapeamento de tipo para SAP HANA</span><span class="sxs-lookup"><span data-stu-id="2b7d9-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="2b7d9-230">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="2b7d9-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="2b7d9-231">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="2b7d9-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="2b7d9-232">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="2b7d9-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="2b7d9-233">Ao mover dados do SAP HANA, Olá mapeamentos a seguir é usado de tipos de too.NET de tipos do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="2b7d9-234">Tipo SAP HANA</span><span class="sxs-lookup"><span data-stu-id="2b7d9-234">SAP HANA Type</span></span> | <span data-ttu-id="2b7d9-235">Tipo baseado no .NET</span><span class="sxs-lookup"><span data-stu-id="2b7d9-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="2b7d9-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="2b7d9-236">TINYINT</span></span> | <span data-ttu-id="2b7d9-237">Byte</span><span class="sxs-lookup"><span data-stu-id="2b7d9-237">Byte</span></span>
<span data-ttu-id="2b7d9-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="2b7d9-238">SMALLINT</span></span> | <span data-ttu-id="2b7d9-239">Int16</span><span class="sxs-lookup"><span data-stu-id="2b7d9-239">Int16</span></span>
<span data-ttu-id="2b7d9-240">INT</span><span class="sxs-lookup"><span data-stu-id="2b7d9-240">INT</span></span> | <span data-ttu-id="2b7d9-241">Int32</span><span class="sxs-lookup"><span data-stu-id="2b7d9-241">Int32</span></span>
<span data-ttu-id="2b7d9-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="2b7d9-242">BIGINT</span></span> | <span data-ttu-id="2b7d9-243">Int64</span><span class="sxs-lookup"><span data-stu-id="2b7d9-243">Int64</span></span>
<span data-ttu-id="2b7d9-244">REAL</span><span class="sxs-lookup"><span data-stu-id="2b7d9-244">REAL</span></span> | <span data-ttu-id="2b7d9-245">Single</span><span class="sxs-lookup"><span data-stu-id="2b7d9-245">Single</span></span>
<span data-ttu-id="2b7d9-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="2b7d9-246">DOUBLE</span></span> | <span data-ttu-id="2b7d9-247">Single</span><span class="sxs-lookup"><span data-stu-id="2b7d9-247">Single</span></span>
<span data-ttu-id="2b7d9-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="2b7d9-248">DECIMAL</span></span> | <span data-ttu-id="2b7d9-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="2b7d9-249">Decimal</span></span>
<span data-ttu-id="2b7d9-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="2b7d9-250">BOOLEAN</span></span> | <span data-ttu-id="2b7d9-251">Byte</span><span class="sxs-lookup"><span data-stu-id="2b7d9-251">Byte</span></span>
<span data-ttu-id="2b7d9-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="2b7d9-252">VARCHAR</span></span> | <span data-ttu-id="2b7d9-253">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2b7d9-253">String</span></span>
<span data-ttu-id="2b7d9-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="2b7d9-254">NVARCHAR</span></span> | <span data-ttu-id="2b7d9-255">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2b7d9-255">String</span></span>
<span data-ttu-id="2b7d9-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="2b7d9-256">CLOB</span></span> | <span data-ttu-id="2b7d9-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2b7d9-257">Byte[]</span></span>
<span data-ttu-id="2b7d9-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="2b7d9-258">ALPHANUM</span></span> | <span data-ttu-id="2b7d9-259">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="2b7d9-259">String</span></span>
<span data-ttu-id="2b7d9-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="2b7d9-260">BLOB</span></span> | <span data-ttu-id="2b7d9-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="2b7d9-261">Byte[]</span></span>
<span data-ttu-id="2b7d9-262">DATE</span><span class="sxs-lookup"><span data-stu-id="2b7d9-262">DATE</span></span> | <span data-ttu-id="2b7d9-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="2b7d9-263">DateTime</span></span>
<span data-ttu-id="2b7d9-264">TIME</span><span class="sxs-lookup"><span data-stu-id="2b7d9-264">TIME</span></span> | <span data-ttu-id="2b7d9-265">timespan</span><span class="sxs-lookup"><span data-stu-id="2b7d9-265">TimeSpan</span></span>
<span data-ttu-id="2b7d9-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="2b7d9-266">TIMESTAMP</span></span> | <span data-ttu-id="2b7d9-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="2b7d9-267">DateTime</span></span>
<span data-ttu-id="2b7d9-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="2b7d9-268">SECONDDATE</span></span> | <span data-ttu-id="2b7d9-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="2b7d9-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="2b7d9-270">Limitações conhecidas</span><span class="sxs-lookup"><span data-stu-id="2b7d9-270">Known limitations</span></span>
<span data-ttu-id="2b7d9-271">Há algumas limitações conhecidas ao copiar dados do SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="2b7d9-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="2b7d9-272">Cadeias de caracteres NVARCHAR são truncados toomaximum comprimento de 4000 caracteres Unicode</span><span class="sxs-lookup"><span data-stu-id="2b7d9-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="2b7d9-273">Não há suporte para SMALLDECIMAL</span><span class="sxs-lookup"><span data-stu-id="2b7d9-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="2b7d9-274">Não há suporte para VARBINARY</span><span class="sxs-lookup"><span data-stu-id="2b7d9-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="2b7d9-275">As datas válidas são entre 30/12/1899 e 31/12/9999</span><span class="sxs-lookup"><span data-stu-id="2b7d9-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="2b7d9-276">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="2b7d9-276">Map source toosink columns</span></span>
<span data-ttu-id="2b7d9-277">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="2b7d9-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2b7d9-278">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="2b7d9-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="2b7d9-279">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="2b7d9-280">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2b7d9-281">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2b7d9-282">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2b7d9-283">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="2b7d9-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2b7d9-284">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="2b7d9-284">Performance and Tuning</span></span>
<span data-ttu-id="2b7d9-285">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="2b7d9-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
