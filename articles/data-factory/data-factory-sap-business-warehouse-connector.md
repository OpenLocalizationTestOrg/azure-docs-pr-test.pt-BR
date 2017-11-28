---
title: Mover dados do SAP Business Warehouse usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como mover dados do SAP Business Warehouse usando o Azure Data Factory.
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
ms.openlocfilehash: 220ccc8b94797880d335385046001c5f3b17c862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="0d174-103">Mover dados do SAP Business Warehouse usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0d174-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="0d174-104">Este artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de um SAP BW (Business Warehouse) local.</span><span class="sxs-lookup"><span data-stu-id="0d174-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="0d174-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0d174-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="0d174-106">Você pode copiar dados de um repositório de dados local do SAP Business Warehouse para qualquer repositório de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="0d174-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="0d174-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0d174-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0d174-108">Atualmente, a data factory dá suporte apenas à movimentação de dados de um SAP Business Warehouse para outros repositórios de dados, mas não para a movimentação de dados de outros repositórios de dados para o SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0d174-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="0d174-109">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="0d174-109">Supported versions and installation</span></span>
<span data-ttu-id="0d174-110">Este conector dá suporte ao SAP Business Warehouse versão 7.x.</span><span class="sxs-lookup"><span data-stu-id="0d174-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="0d174-111">Ele oferece suporte à cópia de dados do InfoCubes e QueryCubes (incluindo consultas BEx) usando consultas MDX.</span><span class="sxs-lookup"><span data-stu-id="0d174-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="0d174-112">Para habilitar a conectividade com a instância do SAP BW, instale os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="0d174-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="0d174-113">**Gateway de Gerenciamento de Dados**: o serviço Data Factory oferece suporte à conexão com armazenamentos de dados locais (incluindo SAP Business Warehouse) usando um componente denominado Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="0d174-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="0d174-114">Para saber mais sobre o Gateway de Gerenciamento de Dados e obter instruções passo a passo de como configurar o gateway, veja o artigo [Mover dados entre armazenamentos de dados locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="0d174-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="0d174-115">O gateway é exigido mesmo que o SAP Business Warehouse esteja hospedado em uma VM (máquina virtual) IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d174-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="0d174-116">Você pode instalar o gateway na mesma VM do armazenamento de dados ou em uma VM diferente, desde que o gateway possa conectar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0d174-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="0d174-117">**Biblioteca do SAP NetWeaver** no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="0d174-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="0d174-118">Você pode obter a biblioteca do SAP Netweaver com seu administrador do SAP, ou diretamente do [Centro de Download de Software SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="0d174-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="0d174-119">Pesquise pela **Nota SAP Nº 1025361** para obter o local de download da versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="0d174-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="0d174-120">Certifique-se de que a arquitetura para a biblioteca do SAP NetWeaver (32 bits ou 64 bits) corresponda à sua instalação do gateway.</span><span class="sxs-lookup"><span data-stu-id="0d174-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="0d174-121">Em seguida, instale todos os arquivos incluídos no SDK RFC do SAP NetWeaver, de acordo com a Nota SAP.</span><span class="sxs-lookup"><span data-stu-id="0d174-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="0d174-122">A biblioteca do SAP NetWeaver também está incluída na instalação das Ferramentas de Cliente SAP.</span><span class="sxs-lookup"><span data-stu-id="0d174-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="0d174-123">Coloque as dlls extraídas do SDK do RFC do NetWeaver na pasta system32.</span><span class="sxs-lookup"><span data-stu-id="0d174-123">Put the dlls extracted from the NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0d174-124">Introdução</span><span class="sxs-lookup"><span data-stu-id="0d174-124">Getting started</span></span>
<span data-ttu-id="0d174-125">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="0d174-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="0d174-126">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="0d174-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="0d174-127">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="0d174-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="0d174-128">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="0d174-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0d174-129">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0d174-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0d174-130">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="0d174-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="0d174-131">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="0d174-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="0d174-132">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="0d174-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="0d174-133">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="0d174-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0d174-134">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="0d174-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="0d174-135">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0d174-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="0d174-136">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um SAP Business Warehouse local, confira a seção [Exemplo de JSON: Copiar dados do SAP Business Warehouse para o Blob do Azure](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="0d174-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="0d174-137">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas para um repositório de dados do SAP BW:</span><span class="sxs-lookup"><span data-stu-id="0d174-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0d174-138">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="0d174-138">Linked service properties</span></span>
<span data-ttu-id="0d174-139">A tabela a seguir fornece a descrição para elementos JSON específicas para o serviço vinculado do SAP Business Warehouse (BW).</span><span class="sxs-lookup"><span data-stu-id="0d174-139">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="0d174-140">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0d174-140">Property</span></span> | <span data-ttu-id="0d174-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="0d174-141">Description</span></span> | <span data-ttu-id="0d174-142">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0d174-142">Allowed values</span></span> | <span data-ttu-id="0d174-143">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0d174-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="0d174-144">server</span><span class="sxs-lookup"><span data-stu-id="0d174-144">server</span></span> | <span data-ttu-id="0d174-145">Nome do servidor no qual reside a instância do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0d174-145">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="0d174-146">string</span><span class="sxs-lookup"><span data-stu-id="0d174-146">string</span></span> | <span data-ttu-id="0d174-147">Sim</span><span class="sxs-lookup"><span data-stu-id="0d174-147">Yes</span></span>
<span data-ttu-id="0d174-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="0d174-148">systemNumber</span></span> | <span data-ttu-id="0d174-149">Número de sistema do sistema SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0d174-149">System number of the SAP BW system.</span></span> | <span data-ttu-id="0d174-150">Número decimal de dois dígitos representado como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0d174-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="0d174-151">Sim</span><span class="sxs-lookup"><span data-stu-id="0d174-151">Yes</span></span>
<span data-ttu-id="0d174-152">clientId</span><span class="sxs-lookup"><span data-stu-id="0d174-152">clientId</span></span> | <span data-ttu-id="0d174-153">ID de Cliente do cliente no sistema SAP W.</span><span class="sxs-lookup"><span data-stu-id="0d174-153">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="0d174-154">Número decimal de três dígitos representado como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0d174-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="0d174-155">Sim</span><span class="sxs-lookup"><span data-stu-id="0d174-155">Yes</span></span>
<span data-ttu-id="0d174-156">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="0d174-156">username</span></span> | <span data-ttu-id="0d174-157">Nome do usuário que tem acesso ao servidor SAP</span><span class="sxs-lookup"><span data-stu-id="0d174-157">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="0d174-158">string</span><span class="sxs-lookup"><span data-stu-id="0d174-158">string</span></span> | <span data-ttu-id="0d174-159">Sim</span><span class="sxs-lookup"><span data-stu-id="0d174-159">Yes</span></span>
<span data-ttu-id="0d174-160">Senha</span><span class="sxs-lookup"><span data-stu-id="0d174-160">password</span></span> | <span data-ttu-id="0d174-161">Senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="0d174-161">Password for the user.</span></span> | <span data-ttu-id="0d174-162">string</span><span class="sxs-lookup"><span data-stu-id="0d174-162">string</span></span> | <span data-ttu-id="0d174-163">Sim</span><span class="sxs-lookup"><span data-stu-id="0d174-163">Yes</span></span>
<span data-ttu-id="0d174-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0d174-164">gatewayName</span></span> | <span data-ttu-id="0d174-165">O nome do gateway que o serviço Data Factory deve usar para se conectar à instância local do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0d174-165">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="0d174-166">string</span><span class="sxs-lookup"><span data-stu-id="0d174-166">string</span></span> | <span data-ttu-id="0d174-167">Sim</span><span class="sxs-lookup"><span data-stu-id="0d174-167">Yes</span></span>
<span data-ttu-id="0d174-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="0d174-168">encryptedCredential</span></span> | <span data-ttu-id="0d174-169">A cadeia de caracteres de credencial criptografada.</span><span class="sxs-lookup"><span data-stu-id="0d174-169">The encrypted credential string.</span></span> | <span data-ttu-id="0d174-170">string</span><span class="sxs-lookup"><span data-stu-id="0d174-170">string</span></span> | <span data-ttu-id="0d174-171">Não</span><span class="sxs-lookup"><span data-stu-id="0d174-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="0d174-172">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="0d174-172">Dataset properties</span></span>
<span data-ttu-id="0d174-173">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0d174-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0d174-174">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="0d174-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0d174-175">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="0d174-175">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="0d174-176">Não há propriedades específicas ao tipo com suporte para o conjunto de dados do SAP BW do tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0d174-176">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="0d174-177">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0d174-177">Copy activity properties</span></span>
<span data-ttu-id="0d174-178">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0d174-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0d174-179">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="0d174-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="0d174-180">Por outro lado, as propriedades disponíveis na seção **typeProperties** da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="0d174-180">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="0d174-181">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="0d174-181">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="0d174-182">Quando a fonte na atividade de cópia for do tipo **RelationalSource** (que inclui o SAP BW), as seguintes propriedades estão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="0d174-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="0d174-183">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0d174-183">Property</span></span> | <span data-ttu-id="0d174-184">Descrição</span><span class="sxs-lookup"><span data-stu-id="0d174-184">Description</span></span> | <span data-ttu-id="0d174-185">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0d174-185">Allowed values</span></span> | <span data-ttu-id="0d174-186">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0d174-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d174-187">query</span><span class="sxs-lookup"><span data-stu-id="0d174-187">query</span></span> | <span data-ttu-id="0d174-188">Especifica a consulta MDX para ler dados da instância do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0d174-188">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="0d174-189">Consulta MDX.</span><span class="sxs-lookup"><span data-stu-id="0d174-189">MDX query.</span></span> | <span data-ttu-id="0d174-190">Sim</span><span class="sxs-lookup"><span data-stu-id="0d174-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="0d174-191">Exemplo de JSON: Copiar dados do SAP Business Warehouse para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="0d174-191">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="0d174-192">O exemplo a seguir fornece as definições de JSON de exemplo que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0d174-192">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0d174-193">Este exemplo mostra como copiar dados de um SAP Business Warehouse local para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d174-193">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="0d174-194">No entanto, os dados podem ser copiados **diretamente** para qualquer uma das fontes declaradas [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0d174-194">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0d174-195">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="0d174-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="0d174-196">Ele não inclui instruções passo a passo para criar o data factory.</span><span class="sxs-lookup"><span data-stu-id="0d174-196">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="0d174-197">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0d174-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="0d174-198">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="0d174-198">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="0d174-199">Um serviço vinculado do tipo [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0d174-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="0d174-200">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0d174-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0d174-201">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0d174-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="0d174-202">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0d174-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0d174-203">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0d174-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0d174-204">O exemplo copia dados de uma instância do SAP Business Warehouse para um Blob do Azure por hora.</span><span class="sxs-lookup"><span data-stu-id="0d174-204">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="0d174-205">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="0d174-205">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="0d174-206">Como uma primeira etapa, configure o gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="0d174-206">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="0d174-207">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="0d174-207">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="0d174-208">Serviço vinculado do SAP Business Warehouse</span><span class="sxs-lookup"><span data-stu-id="0d174-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="0d174-209">Esse serviço vinculado vincula sua instância do SAP BW à data factory.</span><span class="sxs-lookup"><span data-stu-id="0d174-209">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="0d174-210">A propriedade type é definida como **SapBw**.</span><span class="sxs-lookup"><span data-stu-id="0d174-210">The type property is set to **SapBw**.</span></span> <span data-ttu-id="0d174-211">A seção typeProperties fornece informações de conexão para a instância do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0d174-211">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="0d174-212">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0d174-212">Azure Storage linked service</span></span>
<span data-ttu-id="0d174-213">O serviço vinculado vincula sua conta de Armazenamento do Azure à data factory.</span><span class="sxs-lookup"><span data-stu-id="0d174-213">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="0d174-214">A propriedade type é definida como **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="0d174-214">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="0d174-215">A seção typeProperties fornece informações de conexão para a conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d174-215">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="0d174-216">Conjunto de dados de entrada do SAP BW</span><span class="sxs-lookup"><span data-stu-id="0d174-216">SAP BW input dataset</span></span>
<span data-ttu-id="0d174-217">Esse conjunto de dados define o conjunto de dados do SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0d174-217">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="0d174-218">Defina o tipo do conjunto de dados do Data Factory como **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0d174-218">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="0d174-219">No momento, você não especifica quaisquer propriedades específicas ao tipo para um conjunto de dados do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0d174-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="0d174-220">A consulta na definição da Atividade de Cópia especifica quais dados serão lidos da instância do SAP BW.</span><span class="sxs-lookup"><span data-stu-id="0d174-220">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="0d174-221">Configurar a propriedade external como true informa ao serviço Data Factory que a tabela é externa ao Data Factory e não é produzida por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0d174-221">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="0d174-222">As propriedades de frequência e intervalo definem a agenda.</span><span class="sxs-lookup"><span data-stu-id="0d174-222">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="0d174-223">Nesse caso, os dados são lidos da instância do SAP BW por hora.</span><span class="sxs-lookup"><span data-stu-id="0d174-223">In this case, the data is read from the SAP BW instance hourly.</span></span> 

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



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="0d174-224">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="0d174-224">Azure Blob output dataset</span></span>
<span data-ttu-id="0d174-225">Esse conjunto de dados define o conjunto de dados de saída do Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d174-225">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="0d174-226">A propriedade type é definida como AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="0d174-226">The type property is set to AzureBlob.</span></span> <span data-ttu-id="0d174-227">A seção typeProperties fornece o local onde os dados copiados da instância do SAP BW serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="0d174-227">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="0d174-228">Os dados são gravados em um novo blob a cada hora (frequency: hora, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="0d174-228">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0d174-229">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="0d174-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="0d174-230">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="0d174-230">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="0d174-231">Pipeline com Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0d174-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="0d174-232">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0d174-232">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="0d174-233">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** (para a fonte do SAP BW) e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0d174-233">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="0d174-234">A consulta especificada para a propriedade **query** seleciona os dados na última hora para copiar.</span><span class="sxs-lookup"><span data-stu-id="0d174-234">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

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



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="0d174-235">Mapeamento de tipo para SAP BW</span><span class="sxs-lookup"><span data-stu-id="0d174-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="0d174-236">Conforme mencionado no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) , a Atividade de cópia executa conversões automáticas de tipo de fonte para tipos de coletor, com a abordagem em duas etapas descritas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d174-236">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="0d174-237">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="0d174-237">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="0d174-238">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="0d174-238">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="0d174-239">Ao mover dados do SAP BW, os seguintes mapeamentos serão usados dos tipos do SAP BW para os tipos do .NET.</span><span class="sxs-lookup"><span data-stu-id="0d174-239">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="0d174-240">Tipo de dados no Dicionário ABAP</span><span class="sxs-lookup"><span data-stu-id="0d174-240">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="0d174-241">Tipo de Dados do .NET</span><span class="sxs-lookup"><span data-stu-id="0d174-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="0d174-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="0d174-242">ACCP</span></span> |  <span data-ttu-id="0d174-243">int</span><span class="sxs-lookup"><span data-stu-id="0d174-243">Int</span></span>
<span data-ttu-id="0d174-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="0d174-244">CHAR</span></span> | <span data-ttu-id="0d174-245">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d174-245">String</span></span>
<span data-ttu-id="0d174-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="0d174-246">CLNT</span></span> | <span data-ttu-id="0d174-247">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d174-247">String</span></span>
<span data-ttu-id="0d174-248">CURR</span><span class="sxs-lookup"><span data-stu-id="0d174-248">CURR</span></span> | <span data-ttu-id="0d174-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="0d174-249">Decimal</span></span>
<span data-ttu-id="0d174-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="0d174-250">CUKY</span></span> | <span data-ttu-id="0d174-251">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d174-251">String</span></span>
<span data-ttu-id="0d174-252">DEC</span><span class="sxs-lookup"><span data-stu-id="0d174-252">DEC</span></span> | <span data-ttu-id="0d174-253">Decimal</span><span class="sxs-lookup"><span data-stu-id="0d174-253">Decimal</span></span>
<span data-ttu-id="0d174-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="0d174-254">FLTP</span></span> | <span data-ttu-id="0d174-255">Duplo</span><span class="sxs-lookup"><span data-stu-id="0d174-255">Double</span></span>
<span data-ttu-id="0d174-256">INT1</span><span class="sxs-lookup"><span data-stu-id="0d174-256">INT1</span></span> | <span data-ttu-id="0d174-257">Byte</span><span class="sxs-lookup"><span data-stu-id="0d174-257">Byte</span></span>
<span data-ttu-id="0d174-258">INT2</span><span class="sxs-lookup"><span data-stu-id="0d174-258">INT2</span></span> | <span data-ttu-id="0d174-259">Int16</span><span class="sxs-lookup"><span data-stu-id="0d174-259">Int16</span></span>
<span data-ttu-id="0d174-260">INT4</span><span class="sxs-lookup"><span data-stu-id="0d174-260">INT4</span></span> | <span data-ttu-id="0d174-261">int</span><span class="sxs-lookup"><span data-stu-id="0d174-261">Int</span></span>
<span data-ttu-id="0d174-262">LANG</span><span class="sxs-lookup"><span data-stu-id="0d174-262">LANG</span></span> | <span data-ttu-id="0d174-263">string</span><span class="sxs-lookup"><span data-stu-id="0d174-263">String</span></span>
<span data-ttu-id="0d174-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="0d174-264">LCHR</span></span> | <span data-ttu-id="0d174-265">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d174-265">String</span></span>
<span data-ttu-id="0d174-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="0d174-266">LRAW</span></span> | <span data-ttu-id="0d174-267">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0d174-267">Byte[]</span></span>
<span data-ttu-id="0d174-268">PREC</span><span class="sxs-lookup"><span data-stu-id="0d174-268">PREC</span></span> | <span data-ttu-id="0d174-269">Int16</span><span class="sxs-lookup"><span data-stu-id="0d174-269">Int16</span></span>
<span data-ttu-id="0d174-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="0d174-270">QUAN</span></span> | <span data-ttu-id="0d174-271">Decimal</span><span class="sxs-lookup"><span data-stu-id="0d174-271">Decimal</span></span>
<span data-ttu-id="0d174-272">RAW</span><span class="sxs-lookup"><span data-stu-id="0d174-272">RAW</span></span> | <span data-ttu-id="0d174-273">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0d174-273">Byte[]</span></span>
<span data-ttu-id="0d174-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="0d174-274">RAWSTRING</span></span> | <span data-ttu-id="0d174-275">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0d174-275">Byte[]</span></span>
<span data-ttu-id="0d174-276">STRING</span><span class="sxs-lookup"><span data-stu-id="0d174-276">STRING</span></span> | <span data-ttu-id="0d174-277">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d174-277">String</span></span>
<span data-ttu-id="0d174-278">UNIDADE</span><span class="sxs-lookup"><span data-stu-id="0d174-278">UNIT</span></span> | <span data-ttu-id="0d174-279">string</span><span class="sxs-lookup"><span data-stu-id="0d174-279">String</span></span>
<span data-ttu-id="0d174-280">DATS</span><span class="sxs-lookup"><span data-stu-id="0d174-280">DATS</span></span> | <span data-ttu-id="0d174-281">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d174-281">String</span></span>
<span data-ttu-id="0d174-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="0d174-282">NUMC</span></span> | <span data-ttu-id="0d174-283">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d174-283">String</span></span>
<span data-ttu-id="0d174-284">TIMS</span><span class="sxs-lookup"><span data-stu-id="0d174-284">TIMS</span></span> | <span data-ttu-id="0d174-285">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d174-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="0d174-286">Para mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="0d174-286">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="0d174-287">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="0d174-287">Map source to sink columns</span></span>
<span data-ttu-id="0d174-288">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="0d174-288">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="0d174-289">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="0d174-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="0d174-290">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="0d174-290">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="0d174-291">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="0d174-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="0d174-292">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="0d174-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="0d174-293">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="0d174-293">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="0d174-294">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="0d174-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0d174-295">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="0d174-295">Performance and Tuning</span></span>
<span data-ttu-id="0d174-296">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="0d174-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
