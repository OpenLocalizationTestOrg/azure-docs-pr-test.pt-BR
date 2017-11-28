---
title: Mover dados do SAP HANA usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como mover dados do SAP HANA usando o Azure Data Factory.
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
ms.openlocfilehash: 2ab488d82d24999a6231e40cb719715463c51d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="0e32e-103">Mover dados do SAP HANA usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0e32e-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="0e32e-104">Esse artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de um SAP HANA local.</span><span class="sxs-lookup"><span data-stu-id="0e32e-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="0e32e-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0e32e-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="0e32e-106">Você pode copiar dados de um armazenamento de dados local do SAP HANA para qualquer armazenamento de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="0e32e-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="0e32e-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0e32e-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0e32e-108">Atualmente, o Data Factory dá suporte apenas à movimentação de dados de um SAP HANA para outros armazenamentos de dados, mas não à movimentação de dados de outros armazenamentos de dados para um SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="0e32e-109">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="0e32e-109">Supported versions and installation</span></span>
<span data-ttu-id="0e32e-110">Esse conector oferece suporte a qualquer versão do banco de dados SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="0e32e-111">Ele oferece suporte à cópia de dados dos modelos de informações do HANA (como os modos de exibição de Análise e de Cálculo) e às tabelas Linha/Coluna usando consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="0e32e-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="0e32e-112">Para habilitar a conectividade com a instância do SAP HANA, instale os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="0e32e-112">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="0e32e-113">**Gateway de Gerenciamento de Dados**: o serviço Data Factory oferece suporte à conexão com armazenamentos de dados locais (incluindo SAP HANA) usando um componente denominado Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="0e32e-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="0e32e-114">Para saber mais sobre o Gateway de Gerenciamento de Dados e obter instruções passo a passo de como configurar o gateway, veja o artigo [Mover dados entre armazenamentos de dados locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="0e32e-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="0e32e-115">O gateway é requerido mesmo que o SAP HANA esteja hospedado em uma máquina virtual (VM) IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e32e-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="0e32e-116">Você pode instalar o gateway na mesma VM do armazenamento de dados ou em uma VM diferente, desde que o gateway possa conectar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0e32e-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="0e32e-117">**Driver ODBC do SAP HANA** no computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="0e32e-117">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="0e32e-118">Baixe o driver ODBC do SAP HANA do [Centro de Download de Software SAP](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="0e32e-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="0e32e-119">Pesquisa com a palavra-chave **CLIENTE SAP HANA para Windows**.</span><span class="sxs-lookup"><span data-stu-id="0e32e-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="0e32e-120">Introdução</span><span class="sxs-lookup"><span data-stu-id="0e32e-120">Getting started</span></span>
<span data-ttu-id="0e32e-121">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="0e32e-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="0e32e-122">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="0e32e-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="0e32e-123">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="0e32e-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="0e32e-124">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="0e32e-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0e32e-125">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0e32e-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0e32e-126">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="0e32e-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="0e32e-127">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="0e32e-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="0e32e-128">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="0e32e-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="0e32e-129">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="0e32e-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0e32e-130">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="0e32e-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="0e32e-131">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0e32e-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="0e32e-132">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um SAP HANA local, confira a seção [Exemplo de JSON: Copiar dados do SAP HANA para o Blob do Azure](#json-example-copy-data-from-sap-hana-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="0e32e-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="0e32e-133">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas para um repositório de dados do SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="0e32e-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0e32e-134">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="0e32e-134">Linked service properties</span></span>
<span data-ttu-id="0e32e-135">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="0e32e-136">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0e32e-136">Property</span></span> | <span data-ttu-id="0e32e-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="0e32e-137">Description</span></span> | <span data-ttu-id="0e32e-138">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0e32e-138">Allowed values</span></span> | <span data-ttu-id="0e32e-139">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0e32e-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="0e32e-140">server</span><span class="sxs-lookup"><span data-stu-id="0e32e-140">server</span></span> | <span data-ttu-id="0e32e-141">Nome do servidor no qual reside a instância do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-141">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="0e32e-142">Se o servidor estiver usando uma porta personalizada, especifique `server:port`.</span><span class="sxs-lookup"><span data-stu-id="0e32e-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="0e32e-143">string</span><span class="sxs-lookup"><span data-stu-id="0e32e-143">string</span></span> | <span data-ttu-id="0e32e-144">Sim</span><span class="sxs-lookup"><span data-stu-id="0e32e-144">Yes</span></span>
<span data-ttu-id="0e32e-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0e32e-145">authenticationType</span></span> | <span data-ttu-id="0e32e-146">Tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="0e32e-146">Type of authentication.</span></span> | <span data-ttu-id="0e32e-147">cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0e32e-147">string.</span></span> <span data-ttu-id="0e32e-148">"Básico" ou "Windows"</span><span class="sxs-lookup"><span data-stu-id="0e32e-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="0e32e-149">Sim</span><span class="sxs-lookup"><span data-stu-id="0e32e-149">Yes</span></span> 
<span data-ttu-id="0e32e-150">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="0e32e-150">username</span></span> | <span data-ttu-id="0e32e-151">Nome do usuário que tem acesso ao servidor SAP</span><span class="sxs-lookup"><span data-stu-id="0e32e-151">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="0e32e-152">string</span><span class="sxs-lookup"><span data-stu-id="0e32e-152">string</span></span> | <span data-ttu-id="0e32e-153">Sim</span><span class="sxs-lookup"><span data-stu-id="0e32e-153">Yes</span></span>
<span data-ttu-id="0e32e-154">Senha</span><span class="sxs-lookup"><span data-stu-id="0e32e-154">password</span></span> | <span data-ttu-id="0e32e-155">Senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="0e32e-155">Password for the user.</span></span> | <span data-ttu-id="0e32e-156">string</span><span class="sxs-lookup"><span data-stu-id="0e32e-156">string</span></span> | <span data-ttu-id="0e32e-157">Sim</span><span class="sxs-lookup"><span data-stu-id="0e32e-157">Yes</span></span>
<span data-ttu-id="0e32e-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0e32e-158">gatewayName</span></span> | <span data-ttu-id="0e32e-159">O nome do gateway que o serviço Data Factory deve usar para se conectar à instância local do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="0e32e-160">string</span><span class="sxs-lookup"><span data-stu-id="0e32e-160">string</span></span> | <span data-ttu-id="0e32e-161">Sim</span><span class="sxs-lookup"><span data-stu-id="0e32e-161">Yes</span></span>
<span data-ttu-id="0e32e-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="0e32e-162">encryptedCredential</span></span> | <span data-ttu-id="0e32e-163">A cadeia de caracteres de credencial criptografada.</span><span class="sxs-lookup"><span data-stu-id="0e32e-163">The encrypted credential string.</span></span> | <span data-ttu-id="0e32e-164">string</span><span class="sxs-lookup"><span data-stu-id="0e32e-164">string</span></span> | <span data-ttu-id="0e32e-165">Não</span><span class="sxs-lookup"><span data-stu-id="0e32e-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="0e32e-166">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="0e32e-166">Dataset properties</span></span>
<span data-ttu-id="0e32e-167">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0e32e-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0e32e-168">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="0e32e-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0e32e-169">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="0e32e-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="0e32e-170">Não há propriedades específicas ao tipo com suporte para o conjunto de dados do SAP HANA do tipo **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0e32e-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="0e32e-171">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0e32e-171">Copy activity properties</span></span>
<span data-ttu-id="0e32e-172">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0e32e-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0e32e-173">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="0e32e-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="0e32e-174">Por outro lado, as propriedades disponíveis na seção **typeProperties** da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="0e32e-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="0e32e-175">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="0e32e-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="0e32e-176">Quando a fonte na atividade de cópia for do tipo **RelationalSource** (que inclui o SAP HANA), as seguintes propriedades estão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="0e32e-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="0e32e-177">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0e32e-177">Property</span></span> | <span data-ttu-id="0e32e-178">Descrição</span><span class="sxs-lookup"><span data-stu-id="0e32e-178">Description</span></span> | <span data-ttu-id="0e32e-179">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0e32e-179">Allowed values</span></span> | <span data-ttu-id="0e32e-180">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0e32e-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0e32e-181">query</span><span class="sxs-lookup"><span data-stu-id="0e32e-181">query</span></span> | <span data-ttu-id="0e32e-182">Especifica a consulta SQL para ler dados da instância do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-182">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="0e32e-183">Consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="0e32e-183">SQL query.</span></span> | <span data-ttu-id="0e32e-184">Sim</span><span class="sxs-lookup"><span data-stu-id="0e32e-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="0e32e-185">Exemplo de JSON: copiar dados do SAP HANA para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="0e32e-185">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="0e32e-186">O exemplo a seguir fornece as definições de JSON de exemplo que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0e32e-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0e32e-187">Este exemplo mostra como copiar dados de um SAP HANA local para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e32e-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="0e32e-188">No entanto, os dados podem ser copiados **diretamente** para qualquer um dos coletores listados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0e32e-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0e32e-189">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="0e32e-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="0e32e-190">Ele não inclui instruções passo a passo para criar o data factory.</span><span class="sxs-lookup"><span data-stu-id="0e32e-190">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="0e32e-191">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0e32e-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="0e32e-192">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="0e32e-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="0e32e-193">Um serviço vinculado do tipo [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0e32e-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="0e32e-194">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0e32e-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0e32e-195">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0e32e-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="0e32e-196">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0e32e-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0e32e-197">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0e32e-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0e32e-198">O exemplo copia dados de uma instância do SAP HANA para um Blob do Azure por hora.</span><span class="sxs-lookup"><span data-stu-id="0e32e-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="0e32e-199">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="0e32e-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="0e32e-200">Como uma primeira etapa, configure o gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="0e32e-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="0e32e-201">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="0e32e-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="0e32e-202">Serviço vinculado SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0e32e-202">SAP HANA linked service</span></span>
<span data-ttu-id="0e32e-203">Esse serviço vinculado vincula sua instância do SAP HANA à data factory.</span><span class="sxs-lookup"><span data-stu-id="0e32e-203">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="0e32e-204">A propriedade type é definida como **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="0e32e-204">The type property is set to **SapHana**.</span></span> <span data-ttu-id="0e32e-205">A seção typeProperties fornece informações de conexão para a instância do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-205">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="0e32e-206">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0e32e-206">Azure Storage linked service</span></span>
<span data-ttu-id="0e32e-207">O serviço vinculado vincula sua conta de Armazenamento do Azure à data factory.</span><span class="sxs-lookup"><span data-stu-id="0e32e-207">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="0e32e-208">A propriedade type é definida como **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="0e32e-208">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="0e32e-209">A seção typeProperties fornece informações de conexão para a conta do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e32e-209">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="0e32e-210">Conjunto de dados de entrada do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0e32e-210">SAP HANA input dataset</span></span>

<span data-ttu-id="0e32e-211">Esse conjunto de dados define o conjunto de dados do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-211">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="0e32e-212">Defina o tipo do conjunto de dados do Data Factory como **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0e32e-212">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="0e32e-213">No momento, você não especifica quaisquer propriedades específicas ao tipo para um conjunto de dados do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="0e32e-214">A consulta na definição da Atividade de Cópia especifica quais dados serão lidos da instância do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="0e32e-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="0e32e-215">Configurar a propriedade external como true informa ao serviço Data Factory que a tabela é externa ao Data Factory e não é produzida por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0e32e-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="0e32e-216">As propriedades de frequência e intervalo definem a agenda.</span><span class="sxs-lookup"><span data-stu-id="0e32e-216">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="0e32e-217">Nesse caso, os dados são lidos da instância do SAP HANA por hora.</span><span class="sxs-lookup"><span data-stu-id="0e32e-217">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="0e32e-218">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="0e32e-218">Azure Blob output dataset</span></span>
<span data-ttu-id="0e32e-219">Esse conjunto de dados define o conjunto de dados de saída do Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e32e-219">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="0e32e-220">A propriedade type é definida como AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="0e32e-220">The type property is set to AzureBlob.</span></span> <span data-ttu-id="0e32e-221">A seção typeProperties fornece o local onde os dados copiados da instância do SAP HANA serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="0e32e-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="0e32e-222">Os dados são gravados em um novo blob a cada hora (frequency: hora, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="0e32e-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0e32e-223">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="0e32e-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="0e32e-224">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="0e32e-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="0e32e-225">Pipeline com Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0e32e-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="0e32e-226">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0e32e-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="0e32e-227">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** (para a fonte do SAP HANA) e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0e32e-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="0e32e-228">A consulta SQL especificada para a propriedade **query** seleciona os dados na última hora para copiar.</span><span class="sxs-lookup"><span data-stu-id="0e32e-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="0e32e-229">Mapeamento de tipo para SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0e32e-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="0e32e-230">Conforme mencionado no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) , a Atividade de cópia executa conversões automáticas de tipo de fonte para tipos de coletor, com a abordagem em duas etapas descritas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e32e-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="0e32e-231">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="0e32e-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="0e32e-232">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="0e32e-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="0e32e-233">Ao mover dados do SAP HANA, os seguintes mapeamentos serão usados dos tipos do SAP HANA para os tipos do .NET.</span><span class="sxs-lookup"><span data-stu-id="0e32e-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="0e32e-234">Tipo SAP HANA</span><span class="sxs-lookup"><span data-stu-id="0e32e-234">SAP HANA Type</span></span> | <span data-ttu-id="0e32e-235">Tipo baseado no .NET</span><span class="sxs-lookup"><span data-stu-id="0e32e-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="0e32e-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="0e32e-236">TINYINT</span></span> | <span data-ttu-id="0e32e-237">Byte</span><span class="sxs-lookup"><span data-stu-id="0e32e-237">Byte</span></span>
<span data-ttu-id="0e32e-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="0e32e-238">SMALLINT</span></span> | <span data-ttu-id="0e32e-239">Int16</span><span class="sxs-lookup"><span data-stu-id="0e32e-239">Int16</span></span>
<span data-ttu-id="0e32e-240">INT</span><span class="sxs-lookup"><span data-stu-id="0e32e-240">INT</span></span> | <span data-ttu-id="0e32e-241">Int32</span><span class="sxs-lookup"><span data-stu-id="0e32e-241">Int32</span></span>
<span data-ttu-id="0e32e-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="0e32e-242">BIGINT</span></span> | <span data-ttu-id="0e32e-243">Int64</span><span class="sxs-lookup"><span data-stu-id="0e32e-243">Int64</span></span>
<span data-ttu-id="0e32e-244">REAL</span><span class="sxs-lookup"><span data-stu-id="0e32e-244">REAL</span></span> | <span data-ttu-id="0e32e-245">Single</span><span class="sxs-lookup"><span data-stu-id="0e32e-245">Single</span></span>
<span data-ttu-id="0e32e-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="0e32e-246">DOUBLE</span></span> | <span data-ttu-id="0e32e-247">Single</span><span class="sxs-lookup"><span data-stu-id="0e32e-247">Single</span></span>
<span data-ttu-id="0e32e-248">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="0e32e-248">DECIMAL</span></span> | <span data-ttu-id="0e32e-249">Decimal</span><span class="sxs-lookup"><span data-stu-id="0e32e-249">Decimal</span></span>
<span data-ttu-id="0e32e-250">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="0e32e-250">BOOLEAN</span></span> | <span data-ttu-id="0e32e-251">Byte</span><span class="sxs-lookup"><span data-stu-id="0e32e-251">Byte</span></span>
<span data-ttu-id="0e32e-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="0e32e-252">VARCHAR</span></span> | <span data-ttu-id="0e32e-253">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0e32e-253">String</span></span>
<span data-ttu-id="0e32e-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="0e32e-254">NVARCHAR</span></span> | <span data-ttu-id="0e32e-255">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0e32e-255">String</span></span>
<span data-ttu-id="0e32e-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="0e32e-256">CLOB</span></span> | <span data-ttu-id="0e32e-257">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0e32e-257">Byte[]</span></span>
<span data-ttu-id="0e32e-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="0e32e-258">ALPHANUM</span></span> | <span data-ttu-id="0e32e-259">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0e32e-259">String</span></span>
<span data-ttu-id="0e32e-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="0e32e-260">BLOB</span></span> | <span data-ttu-id="0e32e-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0e32e-261">Byte[]</span></span>
<span data-ttu-id="0e32e-262">DATE</span><span class="sxs-lookup"><span data-stu-id="0e32e-262">DATE</span></span> | <span data-ttu-id="0e32e-263">DateTime</span><span class="sxs-lookup"><span data-stu-id="0e32e-263">DateTime</span></span>
<span data-ttu-id="0e32e-264">TIME</span><span class="sxs-lookup"><span data-stu-id="0e32e-264">TIME</span></span> | <span data-ttu-id="0e32e-265">timespan</span><span class="sxs-lookup"><span data-stu-id="0e32e-265">TimeSpan</span></span>
<span data-ttu-id="0e32e-266">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="0e32e-266">TIMESTAMP</span></span> | <span data-ttu-id="0e32e-267">DateTime</span><span class="sxs-lookup"><span data-stu-id="0e32e-267">DateTime</span></span>
<span data-ttu-id="0e32e-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="0e32e-268">SECONDDATE</span></span> | <span data-ttu-id="0e32e-269">DateTime</span><span class="sxs-lookup"><span data-stu-id="0e32e-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="0e32e-270">Limitações conhecidas</span><span class="sxs-lookup"><span data-stu-id="0e32e-270">Known limitations</span></span>
<span data-ttu-id="0e32e-271">Há algumas limitações conhecidas ao copiar dados do SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="0e32e-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="0e32e-272">Cadeias de caracteres NVARCHAR são truncadas para o comprimento máximo de 4.000 caracteres Unicode</span><span class="sxs-lookup"><span data-stu-id="0e32e-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="0e32e-273">Não há suporte para SMALLDECIMAL</span><span class="sxs-lookup"><span data-stu-id="0e32e-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="0e32e-274">Não há suporte para VARBINARY</span><span class="sxs-lookup"><span data-stu-id="0e32e-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="0e32e-275">As datas válidas são entre 30/12/1899 e 31/12/9999</span><span class="sxs-lookup"><span data-stu-id="0e32e-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="0e32e-276">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="0e32e-276">Map source to sink columns</span></span>
<span data-ttu-id="0e32e-277">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="0e32e-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="0e32e-278">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="0e32e-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="0e32e-279">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="0e32e-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="0e32e-280">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="0e32e-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="0e32e-281">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="0e32e-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="0e32e-282">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="0e32e-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="0e32e-283">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="0e32e-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0e32e-284">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="0e32e-284">Performance and Tuning</span></span>
<span data-ttu-id="0e32e-285">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="0e32e-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
