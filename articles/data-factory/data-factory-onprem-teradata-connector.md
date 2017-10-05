---
title: Mover dados do Teradata usando o Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre o conector do Teradata para o serviço do Data Factory que permite mover dados do banco de dados Teradata"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 01edb32cd9e20d4199feac5b98a73aa06b74fec2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="0ac8f-103">Mover dados do Teradata usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0ac8f-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="0ac8f-104">Esse artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de um banco de dados Teradata local.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="0ac8f-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="0ac8f-106">Você pode copiar dados de um armazenamento de dados local do Teradata para qualquer armazenamento de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="0ac8f-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0ac8f-108">Atualmente, o data factory dá suporte apenas à movimentação de dados de um armazenamento de dados Teradata para outros armazenamentos de dados, mas não à movimentação de dados de outros armazenamentos de dados para um armazenamento de dados Teradata.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0ac8f-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0ac8f-109">Prerequisites</span></span>
<span data-ttu-id="0ac8f-110">O data factory dá suporte à conexão a fontes Teradata locais por meio do Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="0ac8f-111">Consulte o artigo [movendo dados entre pontos locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) para saber mais sobre o Gateway de gerenciamento de dados e obter instruções passo a passo de como configurar o gateway.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="0ac8f-112">O gateway é requerido mesmo que o banco de dados Teradata esteja hospedado em uma VM IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="0ac8f-113">Você pode instalar o gateway na mesma VM IaaS do armazenamento de dados ou em uma VM diferente, desde que o gateway possa conectar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="0ac8f-114">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="0ac8f-115">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="0ac8f-115">Supported versions and installation</span></span>
<span data-ttu-id="0ac8f-116">Para o Gateway de Gerenciamento de Dados se conectar ao banco de dados Teradata, você precisa instalar o [Provedor de dados .NET para Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versão 14 ou mais recente no mesmo sistema que o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="0ac8f-117">Há suporte para o Teradata versão 12 e mais recente.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0ac8f-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="0ac8f-118">Getting started</span></span>
<span data-ttu-id="0ac8f-119">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="0ac8f-120">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="0ac8f-121">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="0ac8f-122">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0ac8f-123">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0ac8f-124">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="0ac8f-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="0ac8f-125">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="0ac8f-126">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="0ac8f-127">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0ac8f-128">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="0ac8f-129">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="0ac8f-130">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um armazenamento de dados Teradata local, confira a seção [Exemplo de JSON: Copiar dados do Teradata para o Blob do Azure](#json-example-copy-data-from-teradata-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="0ac8f-131">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas para um armazenamento de dados Teradata:</span><span class="sxs-lookup"><span data-stu-id="0ac8f-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0ac8f-132">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="0ac8f-132">Linked service properties</span></span>
<span data-ttu-id="0ac8f-133">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado Teradata.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="0ac8f-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0ac8f-134">Property</span></span> | <span data-ttu-id="0ac8f-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ac8f-135">Description</span></span> | <span data-ttu-id="0ac8f-136">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0ac8f-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ac8f-137">type</span><span class="sxs-lookup"><span data-stu-id="0ac8f-137">type</span></span> |<span data-ttu-id="0ac8f-138">A propriedade do tipo deve ser definida como: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="0ac8f-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="0ac8f-139">Sim</span><span class="sxs-lookup"><span data-stu-id="0ac8f-139">Yes</span></span> |
| <span data-ttu-id="0ac8f-140">server</span><span class="sxs-lookup"><span data-stu-id="0ac8f-140">server</span></span> |<span data-ttu-id="0ac8f-141">Nome do servidor Teradata.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-141">Name of the Teradata server.</span></span> |<span data-ttu-id="0ac8f-142">Sim</span><span class="sxs-lookup"><span data-stu-id="0ac8f-142">Yes</span></span> |
| <span data-ttu-id="0ac8f-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ac8f-143">authenticationType</span></span> |<span data-ttu-id="0ac8f-144">Tipo de autenticação usado para se conectar ao banco de dados Teradata.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="0ac8f-145">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="0ac8f-146">Sim</span><span class="sxs-lookup"><span data-stu-id="0ac8f-146">Yes</span></span> |
| <span data-ttu-id="0ac8f-147">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="0ac8f-147">username</span></span> |<span data-ttu-id="0ac8f-148">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="0ac8f-149">Não</span><span class="sxs-lookup"><span data-stu-id="0ac8f-149">No</span></span> |
| <span data-ttu-id="0ac8f-150">Senha</span><span class="sxs-lookup"><span data-stu-id="0ac8f-150">password</span></span> |<span data-ttu-id="0ac8f-151">Especifique a senha da conta de usuário que você especificou para o nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="0ac8f-152">Não</span><span class="sxs-lookup"><span data-stu-id="0ac8f-152">No</span></span> |
| <span data-ttu-id="0ac8f-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ac8f-153">gatewayName</span></span> |<span data-ttu-id="0ac8f-154">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados Teradata local.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="0ac8f-155">Sim</span><span class="sxs-lookup"><span data-stu-id="0ac8f-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="0ac8f-156">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="0ac8f-156">Dataset properties</span></span>
<span data-ttu-id="0ac8f-157">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0ac8f-158">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0ac8f-159">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="0ac8f-160">Atualmente, não há nenhuma propriedade do tipo com suporte para o conjunto de dados Teradata.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="0ac8f-161">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="0ac8f-161">Copy activity properties</span></span>
<span data-ttu-id="0ac8f-162">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0ac8f-163">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="0ac8f-164">Por outro lado, as propriedades disponíveis na seção typeProperties da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="0ac8f-165">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="0ac8f-166">Quando a fonte é do tipo **RelationalSource** (que inclui o Teradata), as seguintes propriedades estão disponíveis na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="0ac8f-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="0ac8f-167">Propriedade</span><span class="sxs-lookup"><span data-stu-id="0ac8f-167">Property</span></span> | <span data-ttu-id="0ac8f-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="0ac8f-168">Description</span></span> | <span data-ttu-id="0ac8f-169">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="0ac8f-169">Allowed values</span></span> | <span data-ttu-id="0ac8f-170">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="0ac8f-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ac8f-171">query</span><span class="sxs-lookup"><span data-stu-id="0ac8f-171">query</span></span> |<span data-ttu-id="0ac8f-172">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-172">Use the custom query to read data.</span></span> |<span data-ttu-id="0ac8f-173">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-173">SQL query string.</span></span> <span data-ttu-id="0ac8f-174">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="0ac8f-175">Sim</span><span class="sxs-lookup"><span data-stu-id="0ac8f-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="0ac8f-176">Exemplo de JSON: copiar dados do Teradata para Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="0ac8f-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="0ac8f-177">O exemplo a seguir fornece as definições de JSON de exemplo que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0ac8f-178">Eles mostram como copiar dados do Teradata para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="0ac8f-179">No entanto, os dados podem ser copiados para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="0ac8f-180">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="0ac8f-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="0ac8f-181">Um serviço vinculado do tipo [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="0ac8f-182">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0ac8f-183">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="0ac8f-184">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0ac8f-185">O [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0ac8f-186">O exemplo copia dados de um resultado de consulta no banco de dados Teradata para um blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="0ac8f-187">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="0ac8f-188">Como uma primeira etapa, configure o gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="0ac8f-189">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="0ac8f-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="0ac8f-190">**Serviço Teradata vinculado:**</span><span class="sxs-lookup"><span data-stu-id="0ac8f-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="0ac8f-191">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="0ac8f-191">**Azure Blob storage linked service:**</span></span>

```json
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

<span data-ttu-id="0ac8f-192">**Conjunto de dados de entrada do Teradata:**</span><span class="sxs-lookup"><span data-stu-id="0ac8f-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="0ac8f-193">O exemplo supõe que você criou uma tabela "MyTable" no Teradata e que ela contém uma coluna chamada "timestamp" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="0ac8f-194">A configuração "external": "true" informa ao serviço Data Factory que a tabela é externa ao data factory e não é produzida por uma atividade no data factory.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
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

<span data-ttu-id="0ac8f-195">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="0ac8f-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="0ac8f-196">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0ac8f-197">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="0ac8f-198">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="0ac8f-199">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="0ac8f-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="0ac8f-200">O pipeline contém uma Atividade de Cópia configurada para usar os conjuntos de dados de entrada e saída, e está agendada para ser executada por hora.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="0ac8f-201">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="0ac8f-202">A consulta SQL especificada para a propriedade **query** seleciona os dados na última hora para copiar.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="0ac8f-203">Mapeamento de tipo para Teradata</span><span class="sxs-lookup"><span data-stu-id="0ac8f-203">Type mapping for Teradata</span></span>
<span data-ttu-id="0ac8f-204">Conforme mencionado no artigo sobre [atividades de movimentação de dados](data-factory-data-movement-activities.md) , a Atividade de Cópia executa conversões automáticas de tipos de fonte em tipos de coletor com a abordagem de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="0ac8f-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="0ac8f-205">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="0ac8f-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="0ac8f-206">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="0ac8f-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="0ac8f-207">Ao mover os dados para o Teradata, os seguintes mapeamentos são usados do tipo do Teradata para o tipo do .NET.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="0ac8f-208">Tipo de banco de dados Teradata</span><span class="sxs-lookup"><span data-stu-id="0ac8f-208">Teradata Database type</span></span> | <span data-ttu-id="0ac8f-209">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="0ac8f-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="0ac8f-210">Char</span><span class="sxs-lookup"><span data-stu-id="0ac8f-210">Char</span></span> |<span data-ttu-id="0ac8f-211">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-211">String</span></span> |
| <span data-ttu-id="0ac8f-212">Clob</span><span class="sxs-lookup"><span data-stu-id="0ac8f-212">Clob</span></span> |<span data-ttu-id="0ac8f-213">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-213">String</span></span> |
| <span data-ttu-id="0ac8f-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="0ac8f-214">Graphic</span></span> |<span data-ttu-id="0ac8f-215">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-215">String</span></span> |
| <span data-ttu-id="0ac8f-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="0ac8f-216">VarChar</span></span> |<span data-ttu-id="0ac8f-217">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-217">String</span></span> |
| <span data-ttu-id="0ac8f-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="0ac8f-218">VarGraphic</span></span> |<span data-ttu-id="0ac8f-219">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-219">String</span></span> |
| <span data-ttu-id="0ac8f-220">Blob</span><span class="sxs-lookup"><span data-stu-id="0ac8f-220">Blob</span></span> |<span data-ttu-id="0ac8f-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0ac8f-221">Byte[]</span></span> |
| <span data-ttu-id="0ac8f-222">Byte</span><span class="sxs-lookup"><span data-stu-id="0ac8f-222">Byte</span></span> |<span data-ttu-id="0ac8f-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0ac8f-223">Byte[]</span></span> |
| <span data-ttu-id="0ac8f-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="0ac8f-224">VarByte</span></span> |<span data-ttu-id="0ac8f-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="0ac8f-225">Byte[]</span></span> |
| <span data-ttu-id="0ac8f-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="0ac8f-226">BigInt</span></span> |<span data-ttu-id="0ac8f-227">Int64</span><span class="sxs-lookup"><span data-stu-id="0ac8f-227">Int64</span></span> |
| <span data-ttu-id="0ac8f-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="0ac8f-228">ByteInt</span></span> |<span data-ttu-id="0ac8f-229">Int16</span><span class="sxs-lookup"><span data-stu-id="0ac8f-229">Int16</span></span> |
| <span data-ttu-id="0ac8f-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="0ac8f-230">Decimal</span></span> |<span data-ttu-id="0ac8f-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="0ac8f-231">Decimal</span></span> |
| <span data-ttu-id="0ac8f-232">Duplo</span><span class="sxs-lookup"><span data-stu-id="0ac8f-232">Double</span></span> |<span data-ttu-id="0ac8f-233">Duplo</span><span class="sxs-lookup"><span data-stu-id="0ac8f-233">Double</span></span> |
| <span data-ttu-id="0ac8f-234">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="0ac8f-234">Integer</span></span> |<span data-ttu-id="0ac8f-235">Int32</span><span class="sxs-lookup"><span data-stu-id="0ac8f-235">Int32</span></span> |
| <span data-ttu-id="0ac8f-236">Número</span><span class="sxs-lookup"><span data-stu-id="0ac8f-236">Number</span></span> |<span data-ttu-id="0ac8f-237">Duplo</span><span class="sxs-lookup"><span data-stu-id="0ac8f-237">Double</span></span> |
| <span data-ttu-id="0ac8f-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="0ac8f-238">SmallInt</span></span> |<span data-ttu-id="0ac8f-239">Int16</span><span class="sxs-lookup"><span data-stu-id="0ac8f-239">Int16</span></span> |
| <span data-ttu-id="0ac8f-240">Data</span><span class="sxs-lookup"><span data-stu-id="0ac8f-240">Date</span></span> |<span data-ttu-id="0ac8f-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="0ac8f-241">DateTime</span></span> |
| <span data-ttu-id="0ac8f-242">Hora</span><span class="sxs-lookup"><span data-stu-id="0ac8f-242">Time</span></span> |<span data-ttu-id="0ac8f-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-243">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-244">Hora com fuso horário</span><span class="sxs-lookup"><span data-stu-id="0ac8f-244">Time With Time Zone</span></span> |<span data-ttu-id="0ac8f-245">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-245">String</span></span> |
| <span data-ttu-id="0ac8f-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="0ac8f-246">Timestamp</span></span> |<span data-ttu-id="0ac8f-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="0ac8f-247">DateTime</span></span> |
| <span data-ttu-id="0ac8f-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="0ac8f-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="0ac8f-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="0ac8f-249">DateTimeOffset</span></span> |
| <span data-ttu-id="0ac8f-250">Intervalo - dia</span><span class="sxs-lookup"><span data-stu-id="0ac8f-250">Interval Day</span></span> |<span data-ttu-id="0ac8f-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-251">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-252">Intervalo - dia para hora</span><span class="sxs-lookup"><span data-stu-id="0ac8f-252">Interval Day To Hour</span></span> |<span data-ttu-id="0ac8f-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-253">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-254">Intervalo - dia para minuto</span><span class="sxs-lookup"><span data-stu-id="0ac8f-254">Interval Day To Minute</span></span> |<span data-ttu-id="0ac8f-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-255">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-256">Interval Day To Second</span><span class="sxs-lookup"><span data-stu-id="0ac8f-256">Interval Day To Second</span></span> |<span data-ttu-id="0ac8f-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-257">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-258">Intervalo - hora</span><span class="sxs-lookup"><span data-stu-id="0ac8f-258">Interval Hour</span></span> |<span data-ttu-id="0ac8f-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-259">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-260">Intervalo - hora para minuto</span><span class="sxs-lookup"><span data-stu-id="0ac8f-260">Interval Hour To Minute</span></span> |<span data-ttu-id="0ac8f-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-261">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-262">Interval Hour To Second</span><span class="sxs-lookup"><span data-stu-id="0ac8f-262">Interval Hour To Second</span></span> |<span data-ttu-id="0ac8f-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-263">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="0ac8f-264">Interval Minute</span></span> |<span data-ttu-id="0ac8f-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-265">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-266">Interval Minute To Second</span><span class="sxs-lookup"><span data-stu-id="0ac8f-266">Interval Minute To Second</span></span> |<span data-ttu-id="0ac8f-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-267">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="0ac8f-268">Interval Second</span></span> |<span data-ttu-id="0ac8f-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="0ac8f-269">TimeSpan</span></span> |
| <span data-ttu-id="0ac8f-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="0ac8f-270">Interval Year</span></span> |<span data-ttu-id="0ac8f-271">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-271">String</span></span> |
| <span data-ttu-id="0ac8f-272">Interval Year To Month</span><span class="sxs-lookup"><span data-stu-id="0ac8f-272">Interval Year To Month</span></span> |<span data-ttu-id="0ac8f-273">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-273">String</span></span> |
| <span data-ttu-id="0ac8f-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="0ac8f-274">Interval Month</span></span> |<span data-ttu-id="0ac8f-275">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-275">String</span></span> |
| <span data-ttu-id="0ac8f-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="0ac8f-276">Period(Date)</span></span> |<span data-ttu-id="0ac8f-277">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-277">String</span></span> |
| <span data-ttu-id="0ac8f-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="0ac8f-278">Period(Time)</span></span> |<span data-ttu-id="0ac8f-279">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-279">String</span></span> |
| <span data-ttu-id="0ac8f-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="0ac8f-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="0ac8f-281">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-281">String</span></span> |
| <span data-ttu-id="0ac8f-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="0ac8f-282">Period(Timestamp)</span></span> |<span data-ttu-id="0ac8f-283">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-283">String</span></span> |
| <span data-ttu-id="0ac8f-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="0ac8f-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="0ac8f-285">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-285">String</span></span> |
| <span data-ttu-id="0ac8f-286">Xml</span><span class="sxs-lookup"><span data-stu-id="0ac8f-286">Xml</span></span> |<span data-ttu-id="0ac8f-287">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0ac8f-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="0ac8f-288">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="0ac8f-288">Map source to sink columns</span></span>
<span data-ttu-id="0ac8f-289">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="0ac8f-290">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="0ac8f-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="0ac8f-291">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="0ac8f-292">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="0ac8f-293">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="0ac8f-294">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="0ac8f-295">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="0ac8f-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0ac8f-296">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="0ac8f-296">Performance and Tuning</span></span>
<span data-ttu-id="0ac8f-297">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="0ac8f-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
