---
title: Mover dados do MySQL usando o Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como mover dados do banco de dados MySQL usando o Azure Data Factory
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
ms.openlocfilehash: 05159bfd98977d0b57b43fbc02e4579439f7ce4c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="358a6-103">Mover dados do MySQL usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="358a6-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="358a6-104">Esse artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de um banco de dados MySQL local.</span><span class="sxs-lookup"><span data-stu-id="358a6-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises MySQL database.</span></span> <span data-ttu-id="358a6-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="358a6-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="358a6-106">Você pode copiar dados de um armazenamento de dados local do MySQL para qualquer armazenamento de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="358a6-106">You can copy data from an on-premises MySQL data store to any supported sink data store.</span></span> <span data-ttu-id="358a6-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="358a6-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="358a6-108">Atualmente, o data factory dá suporte apenas à movimentação de dados de um armazenamento de dados MySQL para outros repositórios de dados, mas não à movimentação de dados de outros repositórios de dados para um armazenamento de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="358a6-108">Data factory currently supports only moving data from a MySQL data store to other data stores, but not for moving data from other data stores to an MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="358a6-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="358a6-109">Prerequisites</span></span>
<span data-ttu-id="358a6-110">O serviço Data Factory dá suporte à conexão com fontes MySQL locais usando o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="358a6-110">Data Factory service supports connecting to on-premises MySQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="358a6-111">Consulte o artigo [movendo dados entre pontos locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) para saber mais sobre o Gateway de gerenciamento de dados e obter instruções passo a passo de como configurar o gateway.</span><span class="sxs-lookup"><span data-stu-id="358a6-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="358a6-112">O gateway é requerido mesmo que o banco de dados MySQL esteja hospedado em uma máquina virtual (VM) IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="358a6-112">Gateway is required even if the MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="358a6-113">Você pode instalar o gateway na mesma VM do armazenamento de dados ou em uma VM diferente, desde que o gateway possa conectar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="358a6-113">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="358a6-114">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="358a6-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="358a6-115">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="358a6-115">Supported versions and installation</span></span>
<span data-ttu-id="358a6-116">Para o Gateway de Gerenciamento de Dados conectar-se ao Banco de Dados MySQL, você precisa instalar o [Conector do MySQL/Net para Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versão 6.6.5 ou superior) no mesmo sistema que o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="358a6-116">For Data Management Gateway to connect to the MySQL Database, you need to install the [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="358a6-117">Há suporte para o MySQL versão 5.1 e superior.</span><span class="sxs-lookup"><span data-stu-id="358a6-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="358a6-118">Se você encontrar o erro "A autenticação falhou porque a entidade remota fechou o fluxo de transporte.", considere atualizar o Conector do MySQL/Net para uma versão superior.</span><span class="sxs-lookup"><span data-stu-id="358a6-118">If you hit error on "Authentication failed because the remote party has closed the transport stream.", consider to upgrade the MySQL Connector/Net to higher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="358a6-119">Introdução</span><span class="sxs-lookup"><span data-stu-id="358a6-119">Getting started</span></span>
<span data-ttu-id="358a6-120">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="358a6-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="358a6-121">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="358a6-121">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="358a6-122">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="358a6-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="358a6-123">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="358a6-123">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="358a6-124">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="358a6-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="358a6-125">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="358a6-125">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="358a6-126">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="358a6-126">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="358a6-127">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="358a6-127">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="358a6-128">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="358a6-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="358a6-129">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="358a6-129">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="358a6-130">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="358a6-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="358a6-131">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um armazenamento de dados MySQL local, confira a seção [Exemplo de JSON: Copiar dados do MySQL para o Blob do Azure](#json-example-copy-data-from-mysql-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="358a6-131">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL to Azure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="358a6-132">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas para um armazenamento de dados MySQL:</span><span class="sxs-lookup"><span data-stu-id="358a6-132">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="358a6-133">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="358a6-133">Linked service properties</span></span>
<span data-ttu-id="358a6-134">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do MySQL.</span><span class="sxs-lookup"><span data-stu-id="358a6-134">The following table provides description for JSON elements specific to MySQL linked service.</span></span>

| <span data-ttu-id="358a6-135">Propriedade</span><span class="sxs-lookup"><span data-stu-id="358a6-135">Property</span></span> | <span data-ttu-id="358a6-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="358a6-136">Description</span></span> | <span data-ttu-id="358a6-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="358a6-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="358a6-138">type</span><span class="sxs-lookup"><span data-stu-id="358a6-138">type</span></span> |<span data-ttu-id="358a6-139">A propriedade do tipo deve ser definida como: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="358a6-139">The type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="358a6-140">Sim</span><span class="sxs-lookup"><span data-stu-id="358a6-140">Yes</span></span> |
| <span data-ttu-id="358a6-141">server</span><span class="sxs-lookup"><span data-stu-id="358a6-141">server</span></span> |<span data-ttu-id="358a6-142">Nome do servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="358a6-142">Name of the MySQL server.</span></span> |<span data-ttu-id="358a6-143">Sim</span><span class="sxs-lookup"><span data-stu-id="358a6-143">Yes</span></span> |
| <span data-ttu-id="358a6-144">database</span><span class="sxs-lookup"><span data-stu-id="358a6-144">database</span></span> |<span data-ttu-id="358a6-145">Nome do banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="358a6-145">Name of the MySQL database.</span></span> |<span data-ttu-id="358a6-146">Sim</span><span class="sxs-lookup"><span data-stu-id="358a6-146">Yes</span></span> |
| <span data-ttu-id="358a6-147">schema</span><span class="sxs-lookup"><span data-stu-id="358a6-147">schema</span></span> |<span data-ttu-id="358a6-148">Nome do esquema no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="358a6-148">Name of the schema in the database.</span></span> |<span data-ttu-id="358a6-149">Não</span><span class="sxs-lookup"><span data-stu-id="358a6-149">No</span></span> |
| <span data-ttu-id="358a6-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="358a6-150">authenticationType</span></span> |<span data-ttu-id="358a6-151">Tipo de autenticação usado para se conectar ao banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="358a6-151">Type of authentication used to connect to the MySQL database.</span></span> <span data-ttu-id="358a6-152">Os valores possíveis são: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="358a6-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="358a6-153">Sim</span><span class="sxs-lookup"><span data-stu-id="358a6-153">Yes</span></span> |
| <span data-ttu-id="358a6-154">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="358a6-154">username</span></span> |<span data-ttu-id="358a6-155">Especifique o nome de usuário para se conectar ao banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="358a6-155">Specify user name to connect to the MySQL database.</span></span> |<span data-ttu-id="358a6-156">Sim</span><span class="sxs-lookup"><span data-stu-id="358a6-156">Yes</span></span> |
| <span data-ttu-id="358a6-157">Senha</span><span class="sxs-lookup"><span data-stu-id="358a6-157">password</span></span> |<span data-ttu-id="358a6-158">Especifique a senha da conta de usuário que você especificou.</span><span class="sxs-lookup"><span data-stu-id="358a6-158">Specify password for the user account you specified.</span></span> |<span data-ttu-id="358a6-159">Sim</span><span class="sxs-lookup"><span data-stu-id="358a6-159">Yes</span></span> |
| <span data-ttu-id="358a6-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="358a6-160">gatewayName</span></span> |<span data-ttu-id="358a6-161">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados MySQL local.</span><span class="sxs-lookup"><span data-stu-id="358a6-161">Name of the gateway that the Data Factory service should use to connect to the on-premises MySQL database.</span></span> |<span data-ttu-id="358a6-162">Sim</span><span class="sxs-lookup"><span data-stu-id="358a6-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="358a6-163">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="358a6-163">Dataset properties</span></span>
<span data-ttu-id="358a6-164">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="358a6-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="358a6-165">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="358a6-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="358a6-166">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="358a6-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="358a6-167">A seção typeProperties de um conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados do MySQL) tem as propriedades a seguir</span><span class="sxs-lookup"><span data-stu-id="358a6-167">The typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has the following properties</span></span>

| <span data-ttu-id="358a6-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="358a6-168">Property</span></span> | <span data-ttu-id="358a6-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="358a6-169">Description</span></span> | <span data-ttu-id="358a6-170">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="358a6-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="358a6-171">tableName</span><span class="sxs-lookup"><span data-stu-id="358a6-171">tableName</span></span> |<span data-ttu-id="358a6-172">Nome da tabela na instância do Banco de Dados MySQL à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="358a6-172">Name of the table in the MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="358a6-173">Não (se **query** de **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="358a6-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="358a6-174">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="358a6-174">Copy activity properties</span></span>
<span data-ttu-id="358a6-175">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="358a6-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="358a6-176">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="358a6-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="358a6-177">Por outro lado, as propriedades disponíveis na seção **typeProperties** da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="358a6-177">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="358a6-178">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="358a6-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="358a6-179">Quando a fonte na atividade de cópia for do tipo **RelationalSource** (que inclui o MySQL), as seguintes propriedades estão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="358a6-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="358a6-180">Propriedade</span><span class="sxs-lookup"><span data-stu-id="358a6-180">Property</span></span> | <span data-ttu-id="358a6-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="358a6-181">Description</span></span> | <span data-ttu-id="358a6-182">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="358a6-182">Allowed values</span></span> | <span data-ttu-id="358a6-183">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="358a6-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="358a6-184">query</span><span class="sxs-lookup"><span data-stu-id="358a6-184">query</span></span> |<span data-ttu-id="358a6-185">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="358a6-185">Use the custom query to read data.</span></span> |<span data-ttu-id="358a6-186">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="358a6-186">SQL query string.</span></span> <span data-ttu-id="358a6-187">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="358a6-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="358a6-188">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="358a6-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-to-azure-blob"></a><span data-ttu-id="358a6-189">Exemplo de JSON: copiar dados do MySQL para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="358a6-189">JSON example: Copy data from MySQL to Azure Blob</span></span>
<span data-ttu-id="358a6-190">Este exemplo fornece as definições de JSON de exemplo que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="358a6-190">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="358a6-191">Ele mostra como copiar dados de um banco de dados MySQL local para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="358a6-191">It shows how to copy data from an on-premises MySQL database to an Azure Blob Storage.</span></span> <span data-ttu-id="358a6-192">No entanto, os dados podem ser copiados para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="358a6-192">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="358a6-193">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="358a6-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="358a6-194">Ele não inclui instruções passo a passo para criar o data factory.</span><span class="sxs-lookup"><span data-stu-id="358a6-194">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="358a6-195">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="358a6-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="358a6-196">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="358a6-196">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="358a6-197">Um serviço vinculado do tipo [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="358a6-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="358a6-198">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="358a6-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="358a6-199">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="358a6-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="358a6-200">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="358a6-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="358a6-201">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="358a6-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="358a6-202">O exemplo copia os dados de um resultado da consulta no banco de dados MySQL para um blob por hora.</span><span class="sxs-lookup"><span data-stu-id="358a6-202">The sample copies data from a query result in MySQL database to a blob hourly.</span></span> <span data-ttu-id="358a6-203">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="358a6-203">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="358a6-204">Como uma primeira etapa, configure o gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="358a6-204">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="358a6-205">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="358a6-205">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="358a6-206">**Serviço vinculado do MySQL:**</span><span class="sxs-lookup"><span data-stu-id="358a6-206">**MySQL linked service:**</span></span>

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

<span data-ttu-id="358a6-207">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="358a6-207">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="358a6-208">**Conjunto de dados de entrada do MySQL:**</span><span class="sxs-lookup"><span data-stu-id="358a6-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="358a6-209">O exemplo supõe que você criou uma tabela "MyTable" no MySQL e que ela contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="358a6-209">The sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="358a6-210">Configurar "external": "true" informa ao serviço Data Factory que a tabela é externa ao Data Factory e não é produzida por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="358a6-210">Setting “external”: ”true” informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="358a6-211">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="358a6-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="358a6-212">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="358a6-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="358a6-213">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="358a6-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="358a6-214">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="358a6-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="358a6-215">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="358a6-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="358a6-216">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="358a6-216">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="358a6-217">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="358a6-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="358a6-218">A consulta SQL especificada para a propriedade **query** seleciona os dados na última hora para copiar.</span><span class="sxs-lookup"><span data-stu-id="358a6-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="358a6-219">Mapeamento de tipo para MySQL</span><span class="sxs-lookup"><span data-stu-id="358a6-219">Type mapping for MySQL</span></span>
<span data-ttu-id="358a6-220">Conforme mencionado no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md) , a Atividade de cópia executa conversões automáticas de tipo de fonte para tipos de coletor, com a abordagem em duas etapas descritas a seguir:</span><span class="sxs-lookup"><span data-stu-id="358a6-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="358a6-221">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="358a6-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="358a6-222">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="358a6-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="358a6-223">Ao mover dados para o MySQL os seguintes mapeamentos serão usados dos tipos do MySQL para os tipos do .NET.</span><span class="sxs-lookup"><span data-stu-id="358a6-223">When moving data to MySQL, the following mappings are used from MySQL types to .NET types.</span></span>

| <span data-ttu-id="358a6-224">Tipo do Banco de Dados MySQL</span><span class="sxs-lookup"><span data-stu-id="358a6-224">MySQL Database type</span></span> | <span data-ttu-id="358a6-225">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="358a6-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="358a6-226">bigint unsigned</span><span class="sxs-lookup"><span data-stu-id="358a6-226">bigint unsigned</span></span> |<span data-ttu-id="358a6-227">Decimal</span><span class="sxs-lookup"><span data-stu-id="358a6-227">Decimal</span></span> |
| <span data-ttu-id="358a6-228">bigint</span><span class="sxs-lookup"><span data-stu-id="358a6-228">bigint</span></span> |<span data-ttu-id="358a6-229">Int64</span><span class="sxs-lookup"><span data-stu-id="358a6-229">Int64</span></span> |
| <span data-ttu-id="358a6-230">bit</span><span class="sxs-lookup"><span data-stu-id="358a6-230">bit</span></span> |<span data-ttu-id="358a6-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="358a6-231">Decimal</span></span> |
| <span data-ttu-id="358a6-232">blob</span><span class="sxs-lookup"><span data-stu-id="358a6-232">blob</span></span> |<span data-ttu-id="358a6-233">Byte[]</span><span class="sxs-lookup"><span data-stu-id="358a6-233">Byte[]</span></span> |
| <span data-ttu-id="358a6-234">bool</span><span class="sxs-lookup"><span data-stu-id="358a6-234">bool</span></span> |<span data-ttu-id="358a6-235">Booliano</span><span class="sxs-lookup"><span data-stu-id="358a6-235">Boolean</span></span> |
| <span data-ttu-id="358a6-236">char</span><span class="sxs-lookup"><span data-stu-id="358a6-236">char</span></span> |<span data-ttu-id="358a6-237">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="358a6-237">String</span></span> |
| <span data-ttu-id="358a6-238">data</span><span class="sxs-lookup"><span data-stu-id="358a6-238">date</span></span> |<span data-ttu-id="358a6-239">Datetime</span><span class="sxs-lookup"><span data-stu-id="358a6-239">Datetime</span></span> |
| <span data-ttu-id="358a6-240">Datetime</span><span class="sxs-lookup"><span data-stu-id="358a6-240">datetime</span></span> |<span data-ttu-id="358a6-241">Datetime</span><span class="sxs-lookup"><span data-stu-id="358a6-241">Datetime</span></span> |
| <span data-ttu-id="358a6-242">Decimal</span><span class="sxs-lookup"><span data-stu-id="358a6-242">decimal</span></span> |<span data-ttu-id="358a6-243">Decimal</span><span class="sxs-lookup"><span data-stu-id="358a6-243">Decimal</span></span> |
| <span data-ttu-id="358a6-244">double precision</span><span class="sxs-lookup"><span data-stu-id="358a6-244">double precision</span></span> |<span data-ttu-id="358a6-245">Duplo</span><span class="sxs-lookup"><span data-stu-id="358a6-245">Double</span></span> |
| <span data-ttu-id="358a6-246">Duplo</span><span class="sxs-lookup"><span data-stu-id="358a6-246">double</span></span> |<span data-ttu-id="358a6-247">Duplo</span><span class="sxs-lookup"><span data-stu-id="358a6-247">Double</span></span> |
| <span data-ttu-id="358a6-248">enum</span><span class="sxs-lookup"><span data-stu-id="358a6-248">enum</span></span> |<span data-ttu-id="358a6-249">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="358a6-249">String</span></span> |
| <span data-ttu-id="358a6-250">flutuante</span><span class="sxs-lookup"><span data-stu-id="358a6-250">float</span></span> |<span data-ttu-id="358a6-251">Single</span><span class="sxs-lookup"><span data-stu-id="358a6-251">Single</span></span> |
| <span data-ttu-id="358a6-252">int unsigned</span><span class="sxs-lookup"><span data-stu-id="358a6-252">int unsigned</span></span> |<span data-ttu-id="358a6-253">Int64</span><span class="sxs-lookup"><span data-stu-id="358a6-253">Int64</span></span> |
| <span data-ttu-id="358a6-254">int</span><span class="sxs-lookup"><span data-stu-id="358a6-254">int</span></span> |<span data-ttu-id="358a6-255">Int32</span><span class="sxs-lookup"><span data-stu-id="358a6-255">Int32</span></span> |
| <span data-ttu-id="358a6-256">integer unsigned</span><span class="sxs-lookup"><span data-stu-id="358a6-256">integer unsigned</span></span> |<span data-ttu-id="358a6-257">Int64</span><span class="sxs-lookup"><span data-stu-id="358a6-257">Int64</span></span> |
| <span data-ttu-id="358a6-258">inteiro</span><span class="sxs-lookup"><span data-stu-id="358a6-258">integer</span></span> |<span data-ttu-id="358a6-259">Int32</span><span class="sxs-lookup"><span data-stu-id="358a6-259">Int32</span></span> |
| <span data-ttu-id="358a6-260">long varbinary</span><span class="sxs-lookup"><span data-stu-id="358a6-260">long varbinary</span></span> |<span data-ttu-id="358a6-261">Byte[]</span><span class="sxs-lookup"><span data-stu-id="358a6-261">Byte[]</span></span> |
| <span data-ttu-id="358a6-262">long varchar</span><span class="sxs-lookup"><span data-stu-id="358a6-262">long varchar</span></span> |<span data-ttu-id="358a6-263">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="358a6-263">String</span></span> |
| <span data-ttu-id="358a6-264">longblob</span><span class="sxs-lookup"><span data-stu-id="358a6-264">longblob</span></span> |<span data-ttu-id="358a6-265">Byte[]</span><span class="sxs-lookup"><span data-stu-id="358a6-265">Byte[]</span></span> |
| <span data-ttu-id="358a6-266">longtext</span><span class="sxs-lookup"><span data-stu-id="358a6-266">longtext</span></span> |<span data-ttu-id="358a6-267">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="358a6-267">String</span></span> |
| <span data-ttu-id="358a6-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="358a6-268">mediumblob</span></span> |<span data-ttu-id="358a6-269">Byte[]</span><span class="sxs-lookup"><span data-stu-id="358a6-269">Byte[]</span></span> |
| <span data-ttu-id="358a6-270">mediumint unsigned</span><span class="sxs-lookup"><span data-stu-id="358a6-270">mediumint unsigned</span></span> |<span data-ttu-id="358a6-271">Int64</span><span class="sxs-lookup"><span data-stu-id="358a6-271">Int64</span></span> |
| <span data-ttu-id="358a6-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="358a6-272">mediumint</span></span> |<span data-ttu-id="358a6-273">Int32</span><span class="sxs-lookup"><span data-stu-id="358a6-273">Int32</span></span> |
| <span data-ttu-id="358a6-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="358a6-274">mediumtext</span></span> |<span data-ttu-id="358a6-275">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="358a6-275">String</span></span> |
| <span data-ttu-id="358a6-276">numérico</span><span class="sxs-lookup"><span data-stu-id="358a6-276">numeric</span></span> |<span data-ttu-id="358a6-277">Decimal</span><span class="sxs-lookup"><span data-stu-id="358a6-277">Decimal</span></span> |
| <span data-ttu-id="358a6-278">real</span><span class="sxs-lookup"><span data-stu-id="358a6-278">real</span></span> |<span data-ttu-id="358a6-279">Duplo</span><span class="sxs-lookup"><span data-stu-id="358a6-279">Double</span></span> |
| <span data-ttu-id="358a6-280">set</span><span class="sxs-lookup"><span data-stu-id="358a6-280">set</span></span> |<span data-ttu-id="358a6-281">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="358a6-281">String</span></span> |
| <span data-ttu-id="358a6-282">smallint unsigned</span><span class="sxs-lookup"><span data-stu-id="358a6-282">smallint unsigned</span></span> |<span data-ttu-id="358a6-283">Int32</span><span class="sxs-lookup"><span data-stu-id="358a6-283">Int32</span></span> |
| <span data-ttu-id="358a6-284">smallint</span><span class="sxs-lookup"><span data-stu-id="358a6-284">smallint</span></span> |<span data-ttu-id="358a6-285">Int16</span><span class="sxs-lookup"><span data-stu-id="358a6-285">Int16</span></span> |
| <span data-ttu-id="358a6-286">texto</span><span class="sxs-lookup"><span data-stu-id="358a6-286">text</span></span> |<span data-ttu-id="358a6-287">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="358a6-287">String</span></span> |
| <span data-ttu-id="358a6-288">tempo real</span><span class="sxs-lookup"><span data-stu-id="358a6-288">time</span></span> |<span data-ttu-id="358a6-289">timespan</span><span class="sxs-lookup"><span data-stu-id="358a6-289">TimeSpan</span></span> |
| <span data-ttu-id="358a6-290">timestamp</span><span class="sxs-lookup"><span data-stu-id="358a6-290">timestamp</span></span> |<span data-ttu-id="358a6-291">Datetime</span><span class="sxs-lookup"><span data-stu-id="358a6-291">Datetime</span></span> |
| <span data-ttu-id="358a6-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="358a6-292">tinyblob</span></span> |<span data-ttu-id="358a6-293">Byte[]</span><span class="sxs-lookup"><span data-stu-id="358a6-293">Byte[]</span></span> |
| <span data-ttu-id="358a6-294">tinyint unsigned</span><span class="sxs-lookup"><span data-stu-id="358a6-294">tinyint unsigned</span></span> |<span data-ttu-id="358a6-295">Int16</span><span class="sxs-lookup"><span data-stu-id="358a6-295">Int16</span></span> |
| <span data-ttu-id="358a6-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="358a6-296">tinyint</span></span> |<span data-ttu-id="358a6-297">Int16</span><span class="sxs-lookup"><span data-stu-id="358a6-297">Int16</span></span> |
| <span data-ttu-id="358a6-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="358a6-298">tinytext</span></span> |<span data-ttu-id="358a6-299">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="358a6-299">String</span></span> |
| <span data-ttu-id="358a6-300">varchar</span><span class="sxs-lookup"><span data-stu-id="358a6-300">varchar</span></span> |<span data-ttu-id="358a6-301">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="358a6-301">String</span></span> |
| <span data-ttu-id="358a6-302">year</span><span class="sxs-lookup"><span data-stu-id="358a6-302">year</span></span> |<span data-ttu-id="358a6-303">int</span><span class="sxs-lookup"><span data-stu-id="358a6-303">Int</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="358a6-304">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="358a6-304">Map source to sink columns</span></span>
<span data-ttu-id="358a6-305">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="358a6-305">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="358a6-306">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="358a6-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="358a6-307">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="358a6-307">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="358a6-308">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="358a6-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="358a6-309">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="358a6-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="358a6-310">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="358a6-310">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="358a6-311">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="358a6-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="358a6-312">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="358a6-312">Performance and Tuning</span></span>
<span data-ttu-id="358a6-313">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="358a6-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
