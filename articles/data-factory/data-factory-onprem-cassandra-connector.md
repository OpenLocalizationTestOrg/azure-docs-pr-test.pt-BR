---
title: Mover dados do Cassandra usando o Data Factory | Microsoft Docs
description: Saiba mais sobre como mover dados de um banco de dados Cassandra local usando o Azure Data Factory.
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
ms.openlocfilehash: f2b225bdbdf2880d26a6ab5f992301bf0a804b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="0d13f-103">Mover dados de um banco de dados Cassandra local usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0d13f-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="0d13f-104">Esse artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de um banco de dados Cassandra local.</span><span class="sxs-lookup"><span data-stu-id="0d13f-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Cassandra database.</span></span> <span data-ttu-id="0d13f-105">Ele se baseia no artigo [Atividades de Movimentação de Dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0d13f-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="0d13f-106">Você pode copiar dados de um armazenamento de dados local do Cassandra para qualquer armazenamento de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="0d13f-106">You can copy data from an on-premises Cassandra data store to any supported sink data store.</span></span> <span data-ttu-id="0d13f-107">Para obter uma lista de armazenamentos de dados com suporte da atividade de cópia, confira a tabela [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0d13f-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0d13f-108">Atualmente, o data factory dá suporte apenas à movimentação de dados de um armazenamento de dados Cassandra para outros armazenamentos de dados, mas não à movimentação de dados de outros armazenamentos de dados para um armazenamento de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="0d13f-108">Data factory currently supports only moving data from a Cassandra data store to other data stores, but not for moving data from other data stores to a Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="0d13f-109">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="0d13f-109">Supported versions</span></span>
<span data-ttu-id="0d13f-110">O conector Cassandra dá suporte às seguintes versões do Cassandra: 2.X.</span><span class="sxs-lookup"><span data-stu-id="0d13f-110">The Cassandra connector supports the following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d13f-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0d13f-111">Prerequisites</span></span>
<span data-ttu-id="0d13f-112">Para que o serviço Azure Data Factory consiga se conectar ao seu banco de dados Cassandra local, é necessário instalar o Gateway de Gerenciamento de Dados no mesmo computador que hospeda o banco de dados ou em um computador separado para evitar a concorrência por recursos com o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0d13f-112">For the Azure Data Factory service to be able to connect to your on-premises Cassandra database, you must install a Data Management Gateway on the same machine that hosts the database or on a separate machine to avoid competing for resources with the database.</span></span> <span data-ttu-id="0d13f-113">O Gateway de Gerenciamento de Dados é um componente que conecta as fontes de dados locais aos serviços de nuvem de uma maneira segura e gerenciada.</span><span class="sxs-lookup"><span data-stu-id="0d13f-113">Data Management Gateway is a component that connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="0d13f-114">Confira o artigo [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md) para obter todos os detalhes sobre o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="0d13f-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="0d13f-115">Consulte o artigo [Mover dados de pontos locais para a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções detalhadas sobre como configurar um pipeline de dados para o gateway a fim de mover dados.</span><span class="sxs-lookup"><span data-stu-id="0d13f-115">See [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="0d13f-116">Você deverá usar o gateway para se conectar a um banco de dados Cassandra mesmo se o banco de dados estiver hospedado na nuvem, por exemplo, em uma VM IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d13f-116">You must use the gateway to connect to a Cassandra database even if the database is hosted in the cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="0d13f-117">Você pode ter o gateway na mesma VM que hospeda o banco de dados ou em uma VM diferente, desde que o gateway possa se conectar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0d13f-117">Y You can have the gateway on the same VM that hosts the database or on a separate VM as long as the gateway can connect to the database.</span></span>  

<span data-ttu-id="0d13f-118">Quando você instala o gateway, ele instala automaticamente um driver ODBC do Microsoft Cassandra usado para se conectar ao banco de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="0d13f-118">When you install the gateway, it automatically installs a Microsoft Cassandra ODBC driver used to connect to Cassandra database.</span></span> <span data-ttu-id="0d13f-119">Portanto, não é necessário instalar nenhum driver manualmente no computador do gateway ao copiar dados do banco de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="0d13f-119">Therefore, you don't need to manually install any driver on the gateway machine when copying data from the Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="0d13f-120">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="0d13f-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0d13f-121">Introdução</span><span class="sxs-lookup"><span data-stu-id="0d13f-121">Getting started</span></span>
<span data-ttu-id="0d13f-122">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="0d13f-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="0d13f-123">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="0d13f-123">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="0d13f-124">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="0d13f-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="0d13f-125">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="0d13f-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0d13f-126">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0d13f-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0d13f-127">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="0d13f-127">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="0d13f-128">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="0d13f-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="0d13f-129">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="0d13f-129">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="0d13f-130">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="0d13f-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0d13f-131">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="0d13f-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="0d13f-132">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0d13f-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="0d13f-133">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um armazenamento de dados Cassandra local, confira a seção [Exemplo de JSON: Copiar dados do Cassandra para o Blob do Azure](#json-example-copy-data-from-cassandra-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="0d13f-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra to Azure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="0d13f-134">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas para um armazenamento de dados Cassandra:</span><span class="sxs-lookup"><span data-stu-id="0d13f-134">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0d13f-135">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="0d13f-135">Linked service properties</span></span>
<span data-ttu-id="0d13f-136">A tabela a seguir fornece a descrição de elementos JSON específicos para o serviço vinculado Cassandra.</span><span class="sxs-lookup"><span data-stu-id="0d13f-136">The following table provides description for JSON elements specific to Cassandra linked service.</span></span>

| <span data-ttu-id="0d13f-137">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0d13f-137">Property</span></span> | <span data-ttu-id="0d13f-138">Descrição</span><span class="sxs-lookup"><span data-stu-id="0d13f-138">Description</span></span> | <span data-ttu-id="0d13f-139">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0d13f-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d13f-140">type</span><span class="sxs-lookup"><span data-stu-id="0d13f-140">type</span></span> |<span data-ttu-id="0d13f-141">A propriedade type deve ser definida como: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="0d13f-141">The type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="0d13f-142">Sim</span><span class="sxs-lookup"><span data-stu-id="0d13f-142">Yes</span></span> |
| <span data-ttu-id="0d13f-143">host</span><span class="sxs-lookup"><span data-stu-id="0d13f-143">host</span></span> |<span data-ttu-id="0d13f-144">Um ou mais endereços IP ou nomes de host dos servidores Cassandra.</span><span class="sxs-lookup"><span data-stu-id="0d13f-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="0d13f-145">Especifique uma lista separada por vírgulas de endereços IP ou nomes de host para se conectar simultaneamente a todos os servidores.</span><span class="sxs-lookup"><span data-stu-id="0d13f-145">Specify a comma-separated list of IP addresses or host names to connect to all servers concurrently.</span></span> |<span data-ttu-id="0d13f-146">Sim</span><span class="sxs-lookup"><span data-stu-id="0d13f-146">Yes</span></span> |
| <span data-ttu-id="0d13f-147">porta</span><span class="sxs-lookup"><span data-stu-id="0d13f-147">port</span></span> |<span data-ttu-id="0d13f-148">A porta TCP usada pelo servidor Cassandra para ouvir conexões de cliente.</span><span class="sxs-lookup"><span data-stu-id="0d13f-148">The TCP port that the Cassandra server uses to listen for client connections.</span></span> |<span data-ttu-id="0d13f-149">Não, valor padrão: 9042</span><span class="sxs-lookup"><span data-stu-id="0d13f-149">No, default value: 9042</span></span> |
| <span data-ttu-id="0d13f-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0d13f-150">authenticationType</span></span> |<span data-ttu-id="0d13f-151">Básica, ou Anônima</span><span class="sxs-lookup"><span data-stu-id="0d13f-151">Basic, or Anonymous</span></span> |<span data-ttu-id="0d13f-152">Sim</span><span class="sxs-lookup"><span data-stu-id="0d13f-152">Yes</span></span> |
| <span data-ttu-id="0d13f-153">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="0d13f-153">username</span></span> |<span data-ttu-id="0d13f-154">Especifique o nome de usuário da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="0d13f-154">Specify user name for the user account.</span></span> |<span data-ttu-id="0d13f-155">Sim, se authenticationType for definida como Básica.</span><span class="sxs-lookup"><span data-stu-id="0d13f-155">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="0d13f-156">Senha</span><span class="sxs-lookup"><span data-stu-id="0d13f-156">password</span></span> |<span data-ttu-id="0d13f-157">Especifique a senha para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="0d13f-157">Specify password for the user account.</span></span> |<span data-ttu-id="0d13f-158">Sim, se authenticationType for definida como Básica.</span><span class="sxs-lookup"><span data-stu-id="0d13f-158">Yes, if authenticationType is set to Basic.</span></span> |
| <span data-ttu-id="0d13f-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0d13f-159">gatewayName</span></span> |<span data-ttu-id="0d13f-160">O nome do gateway que é usado para se conectar ao servidor Cassandra local.</span><span class="sxs-lookup"><span data-stu-id="0d13f-160">The name of the gateway that is used to connect to the on-premises Cassandra database.</span></span> |<span data-ttu-id="0d13f-161">Sim</span><span class="sxs-lookup"><span data-stu-id="0d13f-161">Yes</span></span> |
| <span data-ttu-id="0d13f-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="0d13f-162">encryptedCredential</span></span> |<span data-ttu-id="0d13f-163">Credencial criptografada pelo gateway.</span><span class="sxs-lookup"><span data-stu-id="0d13f-163">Credential encrypted by the gateway.</span></span> |<span data-ttu-id="0d13f-164">Não</span><span class="sxs-lookup"><span data-stu-id="0d13f-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="0d13f-165">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="0d13f-165">Dataset properties</span></span>
<span data-ttu-id="0d13f-166">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0d13f-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0d13f-167">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="0d13f-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0d13f-168">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="0d13f-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="0d13f-169">A seção typeProperties para o conjunto de dados do tipo **CassandraTable** tem as seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="0d13f-169">The typeProperties section for dataset of type **CassandraTable** has the following properties</span></span>

| <span data-ttu-id="0d13f-170">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0d13f-170">Property</span></span> | <span data-ttu-id="0d13f-171">Descrição</span><span class="sxs-lookup"><span data-stu-id="0d13f-171">Description</span></span> | <span data-ttu-id="0d13f-172">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0d13f-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d13f-173">keyspace</span><span class="sxs-lookup"><span data-stu-id="0d13f-173">keyspace</span></span> |<span data-ttu-id="0d13f-174">Nome do keyspace ou do esquema no banco de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="0d13f-174">Name of the keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="0d13f-175">Sim (se a **consulta** para **CassandraSource** não estiver definida).</span><span class="sxs-lookup"><span data-stu-id="0d13f-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="0d13f-176">tableName</span><span class="sxs-lookup"><span data-stu-id="0d13f-176">tableName</span></span> |<span data-ttu-id="0d13f-177">Nome da tabela no banco de dados Cassandra.</span><span class="sxs-lookup"><span data-stu-id="0d13f-177">Name of the table in Cassandra database.</span></span> |<span data-ttu-id="0d13f-178">Sim (se a **consulta** para **CassandraSource** não estiver definida).</span><span class="sxs-lookup"><span data-stu-id="0d13f-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="0d13f-179">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0d13f-179">Copy activity properties</span></span>
<span data-ttu-id="0d13f-180">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0d13f-180">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0d13f-181">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="0d13f-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="0d13f-182">Por outro lado, as propriedades disponíveis na seção typeProperties da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="0d13f-182">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="0d13f-183">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="0d13f-183">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="0d13f-184">Quando a fonte é do tipo **CassandraSource**, as seguintes propriedades estão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="0d13f-184">When source is of type **CassandraSource**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="0d13f-185">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0d13f-185">Property</span></span> | <span data-ttu-id="0d13f-186">Descrição</span><span class="sxs-lookup"><span data-stu-id="0d13f-186">Description</span></span> | <span data-ttu-id="0d13f-187">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0d13f-187">Allowed values</span></span> | <span data-ttu-id="0d13f-188">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0d13f-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d13f-189">query</span><span class="sxs-lookup"><span data-stu-id="0d13f-189">query</span></span> |<span data-ttu-id="0d13f-190">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="0d13f-190">Use the custom query to read data.</span></span> |<span data-ttu-id="0d13f-191">Consulta SQL-92 ou consulta CQL.</span><span class="sxs-lookup"><span data-stu-id="0d13f-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="0d13f-192">Veja [Referência ao CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="0d13f-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="0d13f-193">Ao usar a consulta SQL, especifique **keyspace name.table name** para representar a tabela que deseja consultar.</span><span class="sxs-lookup"><span data-stu-id="0d13f-193">When using SQL query, specify **keyspace name.table name** to represent the table you want to query.</span></span> |<span data-ttu-id="0d13f-194">Não (se tableName e keyspace no conjunto de dados estiverem definidos).</span><span class="sxs-lookup"><span data-stu-id="0d13f-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="0d13f-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="0d13f-195">consistencyLevel</span></span> |<span data-ttu-id="0d13f-196">O nível de consistência especifica quantas réplicas devem responder a uma solicitação de leitura antes de retornar dados ao aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="0d13f-196">The consistency level specifies how many replicas must respond to a read request before returning data to the client application.</span></span> <span data-ttu-id="0d13f-197">O Cassandra verifica o número especificado de réplicas de dados atender à solicitação de leitura.</span><span class="sxs-lookup"><span data-stu-id="0d13f-197">Cassandra checks the specified number of replicas for data to satisfy the read request.</span></span> |<span data-ttu-id="0d13f-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="0d13f-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="0d13f-199">Confira [Configuring data consistency (Configurando a consistência de dados)](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="0d13f-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="0d13f-200">Não.</span><span class="sxs-lookup"><span data-stu-id="0d13f-200">No.</span></span> <span data-ttu-id="0d13f-201">O valor padrão é ONE.</span><span class="sxs-lookup"><span data-stu-id="0d13f-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-to-azure-blob"></a><span data-ttu-id="0d13f-202">Exemplo JSON: copiar dados do Cassandra para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="0d13f-202">JSON example: Copy data from Cassandra to Azure Blob</span></span>
<span data-ttu-id="0d13f-203">Este exemplo fornece as definições de JSON de exemplo que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0d13f-203">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0d13f-204">Ele mostra como copiar dados de um banco de dados Cassandra local para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d13f-204">It shows how to copy data from an on-premises Cassandra database to an Azure Blob Storage.</span></span> <span data-ttu-id="0d13f-205">No entanto, os dados podem ser copiados para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0d13f-205">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d13f-206">Este exemplo fornece trechos de JSON.</span><span class="sxs-lookup"><span data-stu-id="0d13f-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="0d13f-207">Ele não inclui instruções passo a passo para criar o data factory.</span><span class="sxs-lookup"><span data-stu-id="0d13f-207">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="0d13f-208">Confira o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0d13f-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="0d13f-209">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="0d13f-209">The sample has the following data factory entities:</span></span>

* <span data-ttu-id="0d13f-210">Um serviço vinculado do tipo [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0d13f-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="0d13f-211">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0d13f-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="0d13f-212">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0d13f-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="0d13f-213">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0d13f-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="0d13f-214">O [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [CassandraSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0d13f-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0d13f-215">**Serviço vinculado Cassandra:**</span><span class="sxs-lookup"><span data-stu-id="0d13f-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="0d13f-216">Este exemplo usa o serviço vinculado **Cassandra** .</span><span class="sxs-lookup"><span data-stu-id="0d13f-216">This example uses the **Cassandra** linked service.</span></span> <span data-ttu-id="0d13f-217">Confira a seção [Serviço vinculado Cassandra](#linked-service-properties) para ver as propriedades compatíveis com esse serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="0d13f-217">See [Cassandra linked service](#linked-service-properties) section for the properties supported by this linked service.</span></span>  

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

<span data-ttu-id="0d13f-218">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="0d13f-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="0d13f-219">**Conjunto de dados de entrada do Cassandra:**</span><span class="sxs-lookup"><span data-stu-id="0d13f-219">**Cassandra input dataset:**</span></span>

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

<span data-ttu-id="0d13f-220">Configurar **external** como **true** informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0d13f-220">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="0d13f-221">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="0d13f-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="0d13f-222">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="0d13f-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

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

<span data-ttu-id="0d13f-223">**Atividade de cópia em um pipeline com origem Cassandra e coletor de Blob:**</span><span class="sxs-lookup"><span data-stu-id="0d13f-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="0d13f-224">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0d13f-224">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="0d13f-225">Na definição de JSON do pipeline, o tipo **source** está definido como **CassandraSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0d13f-225">In the pipeline JSON definition, the **source** type is set to **CassandraSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="0d13f-226">Confira [Propriedades do tipo RelationalSource](#copy-activity-properties) para obter a lista de propriedades permitidas pelo RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="0d13f-226">See [RelationalSource type properties](#copy-activity-properties) for the list of properties supported by the RelationalSource.</span></span>

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
            "description": "Copy from Cassandra to an Azure blob",
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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="0d13f-227">Mapeamento de tipo para Cassandra</span><span class="sxs-lookup"><span data-stu-id="0d13f-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="0d13f-228">Tipo Cassandra</span><span class="sxs-lookup"><span data-stu-id="0d13f-228">Cassandra Type</span></span> | <span data-ttu-id="0d13f-229">Tipo baseado no .Net</span><span class="sxs-lookup"><span data-stu-id="0d13f-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="0d13f-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="0d13f-230">ASCII</span></span> |<span data-ttu-id="0d13f-231">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d13f-231">String</span></span> |
| <span data-ttu-id="0d13f-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="0d13f-232">BIGINT</span></span> |<span data-ttu-id="0d13f-233">Int64</span><span class="sxs-lookup"><span data-stu-id="0d13f-233">Int64</span></span> |
| <span data-ttu-id="0d13f-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="0d13f-234">BLOB</span></span> |<span data-ttu-id="0d13f-235">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0d13f-235">Byte[]</span></span> |
| <span data-ttu-id="0d13f-236">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="0d13f-236">BOOLEAN</span></span> |<span data-ttu-id="0d13f-237">BOOLEAN</span><span class="sxs-lookup"><span data-stu-id="0d13f-237">Boolean</span></span> |
| <span data-ttu-id="0d13f-238">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="0d13f-238">DECIMAL</span></span> |<span data-ttu-id="0d13f-239">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="0d13f-239">Decimal</span></span> |
| <span data-ttu-id="0d13f-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="0d13f-240">DOUBLE</span></span> |<span data-ttu-id="0d13f-241">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="0d13f-241">Double</span></span> |
| <span data-ttu-id="0d13f-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="0d13f-242">FLOAT</span></span> |<span data-ttu-id="0d13f-243">Single</span><span class="sxs-lookup"><span data-stu-id="0d13f-243">Single</span></span> |
| <span data-ttu-id="0d13f-244">INET</span><span class="sxs-lookup"><span data-stu-id="0d13f-244">INET</span></span> |<span data-ttu-id="0d13f-245">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d13f-245">String</span></span> |
| <span data-ttu-id="0d13f-246">INT</span><span class="sxs-lookup"><span data-stu-id="0d13f-246">INT</span></span> |<span data-ttu-id="0d13f-247">Int32</span><span class="sxs-lookup"><span data-stu-id="0d13f-247">Int32</span></span> |
| <span data-ttu-id="0d13f-248">TEXT</span><span class="sxs-lookup"><span data-stu-id="0d13f-248">TEXT</span></span> |<span data-ttu-id="0d13f-249">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d13f-249">String</span></span> |
| <span data-ttu-id="0d13f-250">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="0d13f-250">TIMESTAMP</span></span> |<span data-ttu-id="0d13f-251">DateTime</span><span class="sxs-lookup"><span data-stu-id="0d13f-251">DateTime</span></span> |
| <span data-ttu-id="0d13f-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="0d13f-252">TIMEUUID</span></span> |<span data-ttu-id="0d13f-253">Guid</span><span class="sxs-lookup"><span data-stu-id="0d13f-253">Guid</span></span> |
| <span data-ttu-id="0d13f-254">UUID</span><span class="sxs-lookup"><span data-stu-id="0d13f-254">UUID</span></span> |<span data-ttu-id="0d13f-255">Guid</span><span class="sxs-lookup"><span data-stu-id="0d13f-255">Guid</span></span> |
| <span data-ttu-id="0d13f-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="0d13f-256">VARCHAR</span></span> |<span data-ttu-id="0d13f-257">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0d13f-257">String</span></span> |
| <span data-ttu-id="0d13f-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="0d13f-258">VARINT</span></span> |<span data-ttu-id="0d13f-259">DECIMAL</span><span class="sxs-lookup"><span data-stu-id="0d13f-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="0d13f-260">Para tipos de coleção (mapa, conjunto, lista, etc.), consulte a seção [Trabalhar com coleções usando tabela virtual](#work-with-collections-using-virtual-table) .</span><span class="sxs-lookup"><span data-stu-id="0d13f-260">For collection types (map, set, list, etc.), refer to [Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="0d13f-261">Não há suporte para tipos definidos pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="0d13f-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="0d13f-262">O comprimento da coluna Binário e os comprimentos da coluna Cadeia de Caracteres não pode ser maior que 4000.</span><span class="sxs-lookup"><span data-stu-id="0d13f-262">The length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="0d13f-263">Trabalhar com coleções usando tabela virtual</span><span class="sxs-lookup"><span data-stu-id="0d13f-263">Work with collections using virtual table</span></span>
<span data-ttu-id="0d13f-264">O Azure Data Factory usa um driver ODBC interno para se conectar ao banco de dados Cassandra e copiar dados dele.</span><span class="sxs-lookup"><span data-stu-id="0d13f-264">Azure Data Factory uses a built-in ODBC driver to connect to and copy data from your Cassandra database.</span></span> <span data-ttu-id="0d13f-265">Para tipos de coleção, incluindo mapa, conjunto e lista, o driver normaliza novamente os dados em tabelas virtuais correspondentes.</span><span class="sxs-lookup"><span data-stu-id="0d13f-265">For collection types including map, set and list, the driver renormalizes the data into corresponding virtual tables.</span></span> <span data-ttu-id="0d13f-266">Especificamente, se uma tabela contiver colunas de coleção, o driver vai gerar as seguintes tabelas virtuais:</span><span class="sxs-lookup"><span data-stu-id="0d13f-266">Specifically, if a table contains any collection columns, the driver generates the following virtual tables:</span></span>

* <span data-ttu-id="0d13f-267">Uma **tabela base**, que contém os mesmos dados da tabela real, exceto nas colunas de coleção.</span><span class="sxs-lookup"><span data-stu-id="0d13f-267">A **base table**, which contains the same data as the real table except for the collection columns.</span></span> <span data-ttu-id="0d13f-268">A tabela base usa o mesmo nome da tabela real que ela representa.</span><span class="sxs-lookup"><span data-stu-id="0d13f-268">The base table uses the same name as the real table that it represents.</span></span>
* <span data-ttu-id="0d13f-269">Uma **tabela virtual** para cada coluna de coleção, que expande os dados aninhados.</span><span class="sxs-lookup"><span data-stu-id="0d13f-269">A **virtual table** for each collection column, which expands the nested data.</span></span> <span data-ttu-id="0d13f-270">As tabelas virtuais que representam coleções são nomeadas usando o nome da tabela real, um separador "*vt*" e o nome da coluna.</span><span class="sxs-lookup"><span data-stu-id="0d13f-270">The virtual tables that represent collections are named using the name of the real table, a separator “*vt*” and the name of the column.</span></span>

<span data-ttu-id="0d13f-271">As tabelas virtuais se referem aos dados na tabela real, permitindo que o driver acesse dados desordenados.</span><span class="sxs-lookup"><span data-stu-id="0d13f-271">Virtual tables refer to the data in the real table, enabling the driver to access the denormalized data.</span></span> <span data-ttu-id="0d13f-272">Confira a seção Exemplo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="0d13f-272">See Example section for details.</span></span> <span data-ttu-id="0d13f-273">Você pode acessar o conteúdo das coleções de Cassandra consultando e unindo as tabelas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0d13f-273">You can access the content of Cassandra collections by querying and joining the virtual tables.</span></span>

<span data-ttu-id="0d13f-274">Você pode usar o [Assistente de Cópia](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) para exibir intuitivamente a lista de tabelas no banco de dados Cassandra (incluindo as tabelas virtuais) e visualizar os dados internos.</span><span class="sxs-lookup"><span data-stu-id="0d13f-274">You can use the [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) to intuitively view the list of tables in Cassandra database including the virtual tables, and preview the data inside.</span></span> <span data-ttu-id="0d13f-275">Também é possível construir uma consulta no Assistente de Cópia e validar para ver o resultado.</span><span class="sxs-lookup"><span data-stu-id="0d13f-275">You can also construct a query in the Copy Wizard and validate to see the result.</span></span>

### <a name="example"></a><span data-ttu-id="0d13f-276">Exemplo</span><span class="sxs-lookup"><span data-stu-id="0d13f-276">Example</span></span>
<span data-ttu-id="0d13f-277">Por exemplo, "ExampleTable" a seguir é uma tabela de banco de dados Cassandra que contém uma coluna de chave primária de inteiro chamada "pk_int", uma coluna de texto chamado valor, uma coluna de lista, uma coluna de mapa e uma coluna de conjunto (chamada "StringSet").</span><span class="sxs-lookup"><span data-stu-id="0d13f-277">For example, the following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="0d13f-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="0d13f-278">pk_int</span></span> | <span data-ttu-id="0d13f-279">Valor</span><span class="sxs-lookup"><span data-stu-id="0d13f-279">Value</span></span> | <span data-ttu-id="0d13f-280">Listar</span><span class="sxs-lookup"><span data-stu-id="0d13f-280">List</span></span> | <span data-ttu-id="0d13f-281">Mapa</span><span class="sxs-lookup"><span data-stu-id="0d13f-281">Map</span></span> | <span data-ttu-id="0d13f-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="0d13f-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="0d13f-283">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-283">1</span></span> |<span data-ttu-id="0d13f-284">"valor de exemplo 1"</span><span class="sxs-lookup"><span data-stu-id="0d13f-284">"sample value 1"</span></span> |<span data-ttu-id="0d13f-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="0d13f-285">["1", "2", "3"]</span></span> |<span data-ttu-id="0d13f-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="0d13f-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="0d13f-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="0d13f-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="0d13f-288">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-288">3</span></span> |<span data-ttu-id="0d13f-289">"valor de exemplo 3"</span><span class="sxs-lookup"><span data-stu-id="0d13f-289">"sample value 3"</span></span> |<span data-ttu-id="0d13f-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="0d13f-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="0d13f-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="0d13f-291">{"S1": "t"}</span></span> |<span data-ttu-id="0d13f-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="0d13f-292">{"A", "E"}</span></span> |

<span data-ttu-id="0d13f-293">O driver geraria várias tabelas virtuais para representar essa tabela única.</span><span class="sxs-lookup"><span data-stu-id="0d13f-293">The driver would generate multiple virtual tables to represent this single table.</span></span> <span data-ttu-id="0d13f-294">As colunas de chave estrangeira nas tabelas virtuais fazem referência às colunas de chave primário na tabela real e indicam à qual linha da tabela real a linha da tabela virtual corresponde.</span><span class="sxs-lookup"><span data-stu-id="0d13f-294">The foreign key columns in the virtual tables reference the primary key columns in the real table, and indicate which real table row the virtual table row corresponds to.</span></span>

<span data-ttu-id="0d13f-295">A primeira tabela virtual é a tabela base chamada "ExampleTable" e é mostrada na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="0d13f-295">The first virtual table is the base table named “ExampleTable” is shown in the following table.</span></span> <span data-ttu-id="0d13f-296">A tabela base contém os mesmos dados da tabela de banco de dados original, exceto para as coleções, que são omitidas da tabela e expandidas em outras tabelas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0d13f-296">The base table contains the same data as the original database table except for the collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="0d13f-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="0d13f-297">pk_int</span></span> | <span data-ttu-id="0d13f-298">Valor</span><span class="sxs-lookup"><span data-stu-id="0d13f-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="0d13f-299">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-299">1</span></span> |<span data-ttu-id="0d13f-300">"valor de exemplo 1"</span><span class="sxs-lookup"><span data-stu-id="0d13f-300">"sample value 1"</span></span> |
| <span data-ttu-id="0d13f-301">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-301">3</span></span> |<span data-ttu-id="0d13f-302">"valor de exemplo 3"</span><span class="sxs-lookup"><span data-stu-id="0d13f-302">"sample value 3"</span></span> |

<span data-ttu-id="0d13f-303">As tabelas a seguir mostram as tabelas virtuais que normalizam novamente os dados nas colunas Lista, Mapa e StringSet.</span><span class="sxs-lookup"><span data-stu-id="0d13f-303">The following tables show the virtual tables that renormalize the data from the List, Map, and StringSet columns.</span></span> <span data-ttu-id="0d13f-304">As colunas com nomes que terminam com "_index" ou "_key" indicam a posição dos dados na lista ou mapa original.</span><span class="sxs-lookup"><span data-stu-id="0d13f-304">The columns with names that end with “_index” or “_key” indicate the position of the data within the original list or map.</span></span> <span data-ttu-id="0d13f-305">As colunas com nomes que terminam com "_value" contêm os dados expandidos da coleção.</span><span class="sxs-lookup"><span data-stu-id="0d13f-305">The columns with names that end with “_value” contain the expanded data from the collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="0d13f-306">Tabela "ExampleTable_vt_List":</span><span class="sxs-lookup"><span data-stu-id="0d13f-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="0d13f-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="0d13f-307">pk_int</span></span> | <span data-ttu-id="0d13f-308">List_index</span><span class="sxs-lookup"><span data-stu-id="0d13f-308">List_index</span></span> | <span data-ttu-id="0d13f-309">List_value</span><span class="sxs-lookup"><span data-stu-id="0d13f-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d13f-310">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-310">1</span></span> |<span data-ttu-id="0d13f-311">0</span><span class="sxs-lookup"><span data-stu-id="0d13f-311">0</span></span> |<span data-ttu-id="0d13f-312">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-312">1</span></span> |
| <span data-ttu-id="0d13f-313">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-313">1</span></span> |<span data-ttu-id="0d13f-314">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-314">1</span></span> |<span data-ttu-id="0d13f-315">2</span><span class="sxs-lookup"><span data-stu-id="0d13f-315">2</span></span> |
| <span data-ttu-id="0d13f-316">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-316">1</span></span> |<span data-ttu-id="0d13f-317">2</span><span class="sxs-lookup"><span data-stu-id="0d13f-317">2</span></span> |<span data-ttu-id="0d13f-318">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-318">3</span></span> |
| <span data-ttu-id="0d13f-319">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-319">3</span></span> |<span data-ttu-id="0d13f-320">0</span><span class="sxs-lookup"><span data-stu-id="0d13f-320">0</span></span> |<span data-ttu-id="0d13f-321">100</span><span class="sxs-lookup"><span data-stu-id="0d13f-321">100</span></span> |
| <span data-ttu-id="0d13f-322">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-322">3</span></span> |<span data-ttu-id="0d13f-323">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-323">1</span></span> |<span data-ttu-id="0d13f-324">101</span><span class="sxs-lookup"><span data-stu-id="0d13f-324">101</span></span> |
| <span data-ttu-id="0d13f-325">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-325">3</span></span> |<span data-ttu-id="0d13f-326">2</span><span class="sxs-lookup"><span data-stu-id="0d13f-326">2</span></span> |<span data-ttu-id="0d13f-327">102</span><span class="sxs-lookup"><span data-stu-id="0d13f-327">102</span></span> |
| <span data-ttu-id="0d13f-328">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-328">3</span></span> |<span data-ttu-id="0d13f-329">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-329">3</span></span> |<span data-ttu-id="0d13f-330">103</span><span class="sxs-lookup"><span data-stu-id="0d13f-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="0d13f-331">Tabela "ExampleTable_vt_Map":</span><span class="sxs-lookup"><span data-stu-id="0d13f-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="0d13f-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="0d13f-332">pk_int</span></span> | <span data-ttu-id="0d13f-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="0d13f-333">Map_key</span></span> | <span data-ttu-id="0d13f-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="0d13f-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d13f-335">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-335">1</span></span> |<span data-ttu-id="0d13f-336">S1</span><span class="sxs-lookup"><span data-stu-id="0d13f-336">S1</span></span> |<span data-ttu-id="0d13f-337">O </span><span class="sxs-lookup"><span data-stu-id="0d13f-337">A</span></span> |
| <span data-ttu-id="0d13f-338">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-338">1</span></span> |<span data-ttu-id="0d13f-339">S2</span><span class="sxs-lookup"><span data-stu-id="0d13f-339">S2</span></span> |<span data-ttu-id="0d13f-340">b</span><span class="sxs-lookup"><span data-stu-id="0d13f-340">b</span></span> |
| <span data-ttu-id="0d13f-341">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-341">3</span></span> |<span data-ttu-id="0d13f-342">S1</span><span class="sxs-lookup"><span data-stu-id="0d13f-342">S1</span></span> |<span data-ttu-id="0d13f-343">t</span><span class="sxs-lookup"><span data-stu-id="0d13f-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="0d13f-344">Tabela "ExampleTable_vt_StringSet":</span><span class="sxs-lookup"><span data-stu-id="0d13f-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="0d13f-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="0d13f-345">pk_int</span></span> | <span data-ttu-id="0d13f-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="0d13f-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="0d13f-347">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-347">1</span></span> |<span data-ttu-id="0d13f-348">O </span><span class="sxs-lookup"><span data-stu-id="0d13f-348">A</span></span> |
| <span data-ttu-id="0d13f-349">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-349">1</span></span> |<span data-ttu-id="0d13f-350">b</span><span class="sxs-lookup"><span data-stu-id="0d13f-350">B</span></span> |
| <span data-ttu-id="0d13f-351">1</span><span class="sxs-lookup"><span data-stu-id="0d13f-351">1</span></span> |<span data-ttu-id="0d13f-352">C</span><span class="sxs-lookup"><span data-stu-id="0d13f-352">C</span></span> |
| <span data-ttu-id="0d13f-353">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-353">3</span></span> |<span data-ttu-id="0d13f-354">O </span><span class="sxs-lookup"><span data-stu-id="0d13f-354">A</span></span> |
| <span data-ttu-id="0d13f-355">3</span><span class="sxs-lookup"><span data-stu-id="0d13f-355">3</span></span> |<span data-ttu-id="0d13f-356">E</span><span class="sxs-lookup"><span data-stu-id="0d13f-356">E</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="0d13f-357">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="0d13f-357">Map source to sink columns</span></span>
<span data-ttu-id="0d13f-358">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="0d13f-358">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="0d13f-359">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="0d13f-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="0d13f-360">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="0d13f-360">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="0d13f-361">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="0d13f-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="0d13f-362">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="0d13f-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="0d13f-363">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="0d13f-363">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="0d13f-364">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="0d13f-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0d13f-365">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="0d13f-365">Performance and Tuning</span></span>
<span data-ttu-id="0d13f-366">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="0d13f-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
