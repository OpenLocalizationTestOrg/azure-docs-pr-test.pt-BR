---
title: Mover dados do Sybase usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como mover dados do banco de dados Sybase usando o Azure Data Factory.
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
ms.openlocfilehash: 617e604b220b8bc1c452e67da83f733448e16c0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="2563a-103">Mover dados do Sybase usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2563a-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="2563a-104">Esse artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de um banco de dados Sybase local.</span><span class="sxs-lookup"><span data-stu-id="2563a-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="2563a-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="2563a-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="2563a-106">Você pode copiar dados de um armazenamento de dados local do Sybase para qualquer armazenamento de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="2563a-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="2563a-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2563a-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="2563a-108">Atualmente, o data factory dá suporte apenas à movimentação de dados de um armazenamento de dados Sybase para outros armazenamentos de dados, mas não à movimentação de dados de outros armazenamentos de dados para um armazenamento de dados Sybase.</span><span class="sxs-lookup"><span data-stu-id="2563a-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2563a-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2563a-109">Prerequisites</span></span>
<span data-ttu-id="2563a-110">O serviço Data Factory dá suporte à conexão com fontes Sybase locais usando o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="2563a-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="2563a-111">Consulte o artigo [movendo dados entre pontos locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) para saber mais sobre o Gateway de gerenciamento de dados e obter instruções passo a passo de como configurar o gateway.</span><span class="sxs-lookup"><span data-stu-id="2563a-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="2563a-112">O gateway é requerido mesmo que o banco de dados Sybase esteja hospedado em uma VM IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="2563a-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="2563a-113">Você pode instalar o gateway na mesma VM IaaS do armazenamento de dados ou em uma VM diferente, desde que o gateway possa conectar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2563a-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="2563a-114">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="2563a-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="2563a-115">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="2563a-115">Supported versions and installation</span></span>
<span data-ttu-id="2563a-116">Para que o Gateway de Gerenciamento de Dados se conecte ao Banco de Dados Sybase, você precisa instalar o [provedor de dados para o Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 ou superior no mesmo sistema que o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="2563a-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="2563a-117">Há suporte para o Sybase versão 16 e superior.</span><span class="sxs-lookup"><span data-stu-id="2563a-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="2563a-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="2563a-118">Getting started</span></span>
<span data-ttu-id="2563a-119">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="2563a-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="2563a-120">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="2563a-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="2563a-121">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="2563a-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="2563a-122">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="2563a-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="2563a-123">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="2563a-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="2563a-124">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="2563a-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="2563a-125">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="2563a-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="2563a-126">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="2563a-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="2563a-127">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="2563a-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="2563a-128">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="2563a-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="2563a-129">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="2563a-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="2563a-130">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um armazenamento de dados Sybase local, confira a seção [Exemplo de JSON: Copiar dados do Sybase para o Blob do Azure](#json-example-copy-data-from-sybase-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2563a-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="2563a-131">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas para um armazenamento de dados Sybase:</span><span class="sxs-lookup"><span data-stu-id="2563a-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="2563a-132">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="2563a-132">Linked service properties</span></span>
<span data-ttu-id="2563a-133">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado Sybase.</span><span class="sxs-lookup"><span data-stu-id="2563a-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="2563a-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2563a-134">Property</span></span> | <span data-ttu-id="2563a-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="2563a-135">Description</span></span> | <span data-ttu-id="2563a-136">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2563a-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2563a-137">type</span><span class="sxs-lookup"><span data-stu-id="2563a-137">type</span></span> |<span data-ttu-id="2563a-138">A propriedade do tipo deve ser definida como: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="2563a-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="2563a-139">Sim</span><span class="sxs-lookup"><span data-stu-id="2563a-139">Yes</span></span> |
| <span data-ttu-id="2563a-140">server</span><span class="sxs-lookup"><span data-stu-id="2563a-140">server</span></span> |<span data-ttu-id="2563a-141">Nome do servidor do Sybase.</span><span class="sxs-lookup"><span data-stu-id="2563a-141">Name of the Sybase server.</span></span> |<span data-ttu-id="2563a-142">Sim</span><span class="sxs-lookup"><span data-stu-id="2563a-142">Yes</span></span> |
| <span data-ttu-id="2563a-143">database</span><span class="sxs-lookup"><span data-stu-id="2563a-143">database</span></span> |<span data-ttu-id="2563a-144">Nome do banco de dados do Sybase.</span><span class="sxs-lookup"><span data-stu-id="2563a-144">Name of the Sybase database.</span></span> |<span data-ttu-id="2563a-145">Sim</span><span class="sxs-lookup"><span data-stu-id="2563a-145">Yes</span></span> |
| <span data-ttu-id="2563a-146">schema</span><span class="sxs-lookup"><span data-stu-id="2563a-146">schema</span></span> |<span data-ttu-id="2563a-147">Nome do esquema no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2563a-147">Name of the schema in the database.</span></span> |<span data-ttu-id="2563a-148">Não</span><span class="sxs-lookup"><span data-stu-id="2563a-148">No</span></span> |
| <span data-ttu-id="2563a-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="2563a-149">authenticationType</span></span> |<span data-ttu-id="2563a-150">Tipo de autenticação usado para se conectar ao banco de dados Sybase.</span><span class="sxs-lookup"><span data-stu-id="2563a-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="2563a-151">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="2563a-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="2563a-152">Sim</span><span class="sxs-lookup"><span data-stu-id="2563a-152">Yes</span></span> |
| <span data-ttu-id="2563a-153">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="2563a-153">username</span></span> |<span data-ttu-id="2563a-154">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="2563a-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="2563a-155">Não</span><span class="sxs-lookup"><span data-stu-id="2563a-155">No</span></span> |
| <span data-ttu-id="2563a-156">Senha</span><span class="sxs-lookup"><span data-stu-id="2563a-156">password</span></span> |<span data-ttu-id="2563a-157">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="2563a-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="2563a-158">Não</span><span class="sxs-lookup"><span data-stu-id="2563a-158">No</span></span> |
| <span data-ttu-id="2563a-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="2563a-159">gatewayName</span></span> |<span data-ttu-id="2563a-160">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados local do Sybase.</span><span class="sxs-lookup"><span data-stu-id="2563a-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="2563a-161">Sim</span><span class="sxs-lookup"><span data-stu-id="2563a-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="2563a-162">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="2563a-162">Dataset properties</span></span>
<span data-ttu-id="2563a-163">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="2563a-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="2563a-164">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="2563a-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="2563a-165">A seção typeProperties é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="2563a-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="2563a-166">A seção **typeProperties** do conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados Sybase) tem as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="2563a-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="2563a-167">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2563a-167">Property</span></span> | <span data-ttu-id="2563a-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="2563a-168">Description</span></span> | <span data-ttu-id="2563a-169">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2563a-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2563a-170">tableName</span><span class="sxs-lookup"><span data-stu-id="2563a-170">tableName</span></span> |<span data-ttu-id="2563a-171">Nome da tabela na instância do banco de dados Sybase à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="2563a-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="2563a-172">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="2563a-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="2563a-173">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="2563a-173">Copy activity properties</span></span>
<span data-ttu-id="2563a-174">Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, consulte o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="2563a-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="2563a-175">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="2563a-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="2563a-176">Por outro lado, as propriedades disponíveis na seção typeProperties da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="2563a-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="2563a-177">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="2563a-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="2563a-178">Quando a fonte for do tipo **RelationalSource** (que inclui o Sybase), as seguintes propriedades estarão disponíveis na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="2563a-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="2563a-179">Propriedade</span><span class="sxs-lookup"><span data-stu-id="2563a-179">Property</span></span> | <span data-ttu-id="2563a-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="2563a-180">Description</span></span> | <span data-ttu-id="2563a-181">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="2563a-181">Allowed values</span></span> | <span data-ttu-id="2563a-182">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="2563a-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="2563a-183">query</span><span class="sxs-lookup"><span data-stu-id="2563a-183">query</span></span> |<span data-ttu-id="2563a-184">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="2563a-184">Use the custom query to read data.</span></span> |<span data-ttu-id="2563a-185">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="2563a-185">SQL query string.</span></span> <span data-ttu-id="2563a-186">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="2563a-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="2563a-187">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="2563a-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="2563a-188">Exemplo de JSON: copiar dados do Sybase para Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="2563a-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="2563a-189">O exemplo a seguir fornece as definições de JSON de exemplo que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2563a-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="2563a-190">Eles mostram como copiar dados do banco de dados Sybase para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2563a-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="2563a-191">No entanto, os dados podem ser copiados para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2563a-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="2563a-192">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="2563a-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="2563a-193">Um serviço vinculado do tipo [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2563a-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="2563a-194">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="2563a-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="2563a-195">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2563a-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="2563a-196">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="2563a-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="2563a-197">O [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="2563a-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="2563a-198">O exemplo copia dados de um resultado de consulta no banco de dados Sybase para um blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="2563a-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="2563a-199">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="2563a-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="2563a-200">Como uma primeira etapa, configure o gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="2563a-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="2563a-201">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="2563a-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="2563a-202">**Serviço vinculado Sybase:**</span><span class="sxs-lookup"><span data-stu-id="2563a-202">**Sybase linked service:**</span></span>

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

<span data-ttu-id="2563a-203">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="2563a-203">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="2563a-204">**Conjunto de dados de entrada do Sybase:**</span><span class="sxs-lookup"><span data-stu-id="2563a-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="2563a-205">O exemplo supõe que você criou uma tabela "MyTable" no Sybase e que ela contém uma coluna chamada "timestamp" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="2563a-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="2563a-206">Configurar "external": true informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2563a-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="2563a-207">Observe que o **tipo** do serviço vinculado está definido como: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="2563a-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

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

<span data-ttu-id="2563a-208">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="2563a-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="2563a-209">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="2563a-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="2563a-210">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="2563a-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="2563a-211">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="2563a-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="2563a-212">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="2563a-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="2563a-213">O pipeline contém uma Atividade de Cópia configurada para usar os conjuntos de dados de entrada e saída, e está agendada para ser executada por hora.</span><span class="sxs-lookup"><span data-stu-id="2563a-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="2563a-214">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="2563a-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="2563a-215">A consulta SQL especificada para a propriedade **query** seleciona os dados da tabela DBA.Orders no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2563a-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

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

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="2563a-216">Mapeamento de tipo para Sybase</span><span class="sxs-lookup"><span data-stu-id="2563a-216">Type mapping for Sybase</span></span>
<span data-ttu-id="2563a-217">Como mencionado no artigo sobre as [Atividades de Movimentação de Dados](data-factory-data-movement-activities.md) , a atividade de Cópia executa conversões automáticas dos tipos de fonte nos tipos de coletor com a seguinte abordagem de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="2563a-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="2563a-218">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="2563a-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="2563a-219">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="2563a-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="2563a-220">Sybase dá suporte a T-SQL e tipos T-SQL.</span><span class="sxs-lookup"><span data-stu-id="2563a-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="2563a-221">Para uma tabela de mapeamento de tipos do SQL para tipo do .NET, veja o artigo [Conector SQL do Azure](data-factory-azure-sql-connector.md) .</span><span class="sxs-lookup"><span data-stu-id="2563a-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="2563a-222">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="2563a-222">Map source to sink columns</span></span>
<span data-ttu-id="2563a-223">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="2563a-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="2563a-224">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="2563a-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="2563a-225">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="2563a-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="2563a-226">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="2563a-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="2563a-227">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="2563a-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="2563a-228">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="2563a-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="2563a-229">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="2563a-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="2563a-230">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="2563a-230">Performance and Tuning</span></span>
<span data-ttu-id="2563a-231">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="2563a-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
