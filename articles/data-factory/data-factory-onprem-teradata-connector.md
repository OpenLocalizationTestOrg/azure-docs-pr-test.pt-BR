---
title: dados de aaaMove da Teradata usando o Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre o conector de Teradata para Olá serviço da fábrica de dados que permite mover dados do banco de dados Teradata"
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
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="b0a87-103">Mover dados do Teradata usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b0a87-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="b0a87-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de banco de dados Teradata local.</span><span class="sxs-lookup"><span data-stu-id="b0a87-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="b0a87-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0a87-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="b0a87-106">Você pode copiar dados de um repositório de dados local Teradata dados repositório tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="b0a87-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="b0a87-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="b0a87-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="b0a87-108">Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de um de dados Teradata, mas não para mover os dados do repositório de dados de Teradata outros dados repositórios tooa.</span><span class="sxs-lookup"><span data-stu-id="b0a87-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b0a87-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b0a87-109">Prerequisites</span></span>
<span data-ttu-id="b0a87-110">Fábrica de dados oferece suporte a fontes de Teradata local tooon conexão via Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="b0a87-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="b0a87-111">Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0a87-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="b0a87-112">Gateway é necessário mesmo que hello Teradata é hospedado em uma VM de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a87-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="b0a87-113">Você pode instalar o gateway de saudação em Olá mesmo IaaS VM como Olá dados armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b0a87-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="b0a87-114">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="b0a87-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="b0a87-115">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="b0a87-115">Supported versions and installation</span></span>
<span data-ttu-id="b0a87-116">Para Gateway de gerenciamento de dados tooconnect toohello banco de dados Teradata, você precisa Olá tooinstall [.NET Data Provider para Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versão 14 ou acima em Olá mesmo sistema como Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="b0a87-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="b0a87-117">Há suporte para o Teradata versão 12 e mais recente.</span><span class="sxs-lookup"><span data-stu-id="b0a87-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b0a87-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="b0a87-118">Getting started</span></span>
<span data-ttu-id="b0a87-119">Você pode criar um pipeline com atividade de cópia que mova dados de um armazenamento de dados local Cassandra usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="b0a87-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="b0a87-120">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="b0a87-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="b0a87-121">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="b0a87-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="b0a87-122">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="b0a87-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b0a87-123">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="b0a87-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="b0a87-124">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0a87-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="b0a87-125">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="b0a87-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="b0a87-126">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="b0a87-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="b0a87-127">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="b0a87-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b0a87-128">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="b0a87-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="b0a87-129">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0a87-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="b0a87-130">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados Teradata local, consulte [exemplo JSON: copiar dados de Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="b0a87-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="b0a87-131">Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados de Teradata toodefine usado Data Factory entidades tooa específico:</span><span class="sxs-lookup"><span data-stu-id="b0a87-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b0a87-132">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="b0a87-132">Linked service properties</span></span>
<span data-ttu-id="b0a87-133">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooTeradata vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="b0a87-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="b0a87-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b0a87-134">Property</span></span> | <span data-ttu-id="b0a87-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="b0a87-135">Description</span></span> | <span data-ttu-id="b0a87-136">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b0a87-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b0a87-137">type</span><span class="sxs-lookup"><span data-stu-id="b0a87-137">type</span></span> |<span data-ttu-id="b0a87-138">propriedade de tipo Hello deve ser definida como: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="b0a87-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="b0a87-139">Sim</span><span class="sxs-lookup"><span data-stu-id="b0a87-139">Yes</span></span> |
| <span data-ttu-id="b0a87-140">server</span><span class="sxs-lookup"><span data-stu-id="b0a87-140">server</span></span> |<span data-ttu-id="b0a87-141">Nome do servidor de Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="b0a87-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="b0a87-142">Sim</span><span class="sxs-lookup"><span data-stu-id="b0a87-142">Yes</span></span> |
| <span data-ttu-id="b0a87-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="b0a87-143">authenticationType</span></span> |<span data-ttu-id="b0a87-144">Tipo de autenticação usado o banco de dados do tooconnect toohello Teradata.</span><span class="sxs-lookup"><span data-stu-id="b0a87-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="b0a87-145">Os valores possíveis são: Anonymous, Basic e Windows.</span><span class="sxs-lookup"><span data-stu-id="b0a87-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="b0a87-146">Sim</span><span class="sxs-lookup"><span data-stu-id="b0a87-146">Yes</span></span> |
| <span data-ttu-id="b0a87-147">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="b0a87-147">username</span></span> |<span data-ttu-id="b0a87-148">Especifique o nome de usuário se você estiver usando a autenticação Basic ou Windows.</span><span class="sxs-lookup"><span data-stu-id="b0a87-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="b0a87-149">Não</span><span class="sxs-lookup"><span data-stu-id="b0a87-149">No</span></span> |
| <span data-ttu-id="b0a87-150">Senha</span><span class="sxs-lookup"><span data-stu-id="b0a87-150">password</span></span> |<span data-ttu-id="b0a87-151">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0a87-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="b0a87-152">Não</span><span class="sxs-lookup"><span data-stu-id="b0a87-152">No</span></span> |
| <span data-ttu-id="b0a87-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="b0a87-153">gatewayName</span></span> |<span data-ttu-id="b0a87-154">Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local Teradata.</span><span class="sxs-lookup"><span data-stu-id="b0a87-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="b0a87-155">Sim</span><span class="sxs-lookup"><span data-stu-id="b0a87-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="b0a87-156">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="b0a87-156">Dataset properties</span></span>
<span data-ttu-id="b0a87-157">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b0a87-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b0a87-158">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="b0a87-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b0a87-159">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0a87-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="b0a87-160">No momento, não há nenhuma propriedade de tipo com suporte para o conjunto de dados de Teradata hello.</span><span class="sxs-lookup"><span data-stu-id="b0a87-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="b0a87-161">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="b0a87-161">Copy activity properties</span></span>
<span data-ttu-id="b0a87-162">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b0a87-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b0a87-163">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="b0a87-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="b0a87-164">Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="b0a87-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="b0a87-165">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="b0a87-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="b0a87-166">Quando a fonte de saudação é do tipo **RelationalSource** (que inclui Teradata), Olá propriedades a seguir está disponível em **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="b0a87-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="b0a87-167">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b0a87-167">Property</span></span> | <span data-ttu-id="b0a87-168">Descrição</span><span class="sxs-lookup"><span data-stu-id="b0a87-168">Description</span></span> | <span data-ttu-id="b0a87-169">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="b0a87-169">Allowed values</span></span> | <span data-ttu-id="b0a87-170">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b0a87-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b0a87-171">query</span><span class="sxs-lookup"><span data-stu-id="b0a87-171">query</span></span> |<span data-ttu-id="b0a87-172">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="b0a87-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="b0a87-173">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="b0a87-173">SQL query string.</span></span> <span data-ttu-id="b0a87-174">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="b0a87-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="b0a87-175">Sim</span><span class="sxs-lookup"><span data-stu-id="b0a87-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="b0a87-176">Exemplo JSON: copiar dados de Teradata tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="b0a87-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="b0a87-177">Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b0a87-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b0a87-178">Eles mostram como toocopy dados de Teradata tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="b0a87-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="b0a87-179">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0a87-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="b0a87-180">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0a87-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="b0a87-181">Um serviço vinculado do tipo [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b0a87-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="b0a87-182">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b0a87-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b0a87-183">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b0a87-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="b0a87-184">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b0a87-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b0a87-185">Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b0a87-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b0a87-186">exemplo Hello copia dados de um resultado de consulta no blob de tooa do banco de dados Teradata, a cada hora.</span><span class="sxs-lookup"><span data-stu-id="b0a87-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="b0a87-187">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0a87-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="b0a87-188">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0a87-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="b0a87-189">Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b0a87-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b0a87-190">**Serviço Teradata vinculado:**</span><span class="sxs-lookup"><span data-stu-id="b0a87-190">**Teradata linked service:**</span></span>

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

<span data-ttu-id="b0a87-191">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="b0a87-191">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="b0a87-192">**Conjunto de dados de entrada do Teradata:**</span><span class="sxs-lookup"><span data-stu-id="b0a87-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="b0a87-193">exemplo Hello supõe que você criou uma tabela "MyTable" em Teradata e contém uma coluna chamada "timestamp" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="b0a87-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="b0a87-194">Definindo "externo": true informa o serviço de fábrica de dados de saudação tabela Olá toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="b0a87-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="b0a87-195">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="b0a87-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="b0a87-196">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="b0a87-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b0a87-197">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="b0a87-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="b0a87-198">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="b0a87-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="b0a87-199">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="b0a87-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="b0a87-200">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é agendado toorun por hora.</span><span class="sxs-lookup"><span data-stu-id="b0a87-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="b0a87-201">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b0a87-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="b0a87-202">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="b0a87-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="b0a87-203">Mapeamento de tipo para Teradata</span><span class="sxs-lookup"><span data-stu-id="b0a87-203">Type mapping for Teradata</span></span>
<span data-ttu-id="b0a87-204">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, hello atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0a87-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="b0a87-205">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="b0a87-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="b0a87-206">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="b0a87-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="b0a87-207">Ao mover dados tooTeradata, hello mapeamentos a seguir são usados de tipo de too.NET do tipo Teradata.</span><span class="sxs-lookup"><span data-stu-id="b0a87-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="b0a87-208">Tipo de banco de dados Teradata</span><span class="sxs-lookup"><span data-stu-id="b0a87-208">Teradata Database type</span></span> | <span data-ttu-id="b0a87-209">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="b0a87-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="b0a87-210">Char</span><span class="sxs-lookup"><span data-stu-id="b0a87-210">Char</span></span> |<span data-ttu-id="b0a87-211">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-211">String</span></span> |
| <span data-ttu-id="b0a87-212">Clob</span><span class="sxs-lookup"><span data-stu-id="b0a87-212">Clob</span></span> |<span data-ttu-id="b0a87-213">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-213">String</span></span> |
| <span data-ttu-id="b0a87-214">Graphic</span><span class="sxs-lookup"><span data-stu-id="b0a87-214">Graphic</span></span> |<span data-ttu-id="b0a87-215">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-215">String</span></span> |
| <span data-ttu-id="b0a87-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="b0a87-216">VarChar</span></span> |<span data-ttu-id="b0a87-217">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-217">String</span></span> |
| <span data-ttu-id="b0a87-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="b0a87-218">VarGraphic</span></span> |<span data-ttu-id="b0a87-219">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-219">String</span></span> |
| <span data-ttu-id="b0a87-220">Blob</span><span class="sxs-lookup"><span data-stu-id="b0a87-220">Blob</span></span> |<span data-ttu-id="b0a87-221">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b0a87-221">Byte[]</span></span> |
| <span data-ttu-id="b0a87-222">Byte</span><span class="sxs-lookup"><span data-stu-id="b0a87-222">Byte</span></span> |<span data-ttu-id="b0a87-223">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b0a87-223">Byte[]</span></span> |
| <span data-ttu-id="b0a87-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="b0a87-224">VarByte</span></span> |<span data-ttu-id="b0a87-225">Byte[]</span><span class="sxs-lookup"><span data-stu-id="b0a87-225">Byte[]</span></span> |
| <span data-ttu-id="b0a87-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="b0a87-226">BigInt</span></span> |<span data-ttu-id="b0a87-227">Int64</span><span class="sxs-lookup"><span data-stu-id="b0a87-227">Int64</span></span> |
| <span data-ttu-id="b0a87-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="b0a87-228">ByteInt</span></span> |<span data-ttu-id="b0a87-229">Int16</span><span class="sxs-lookup"><span data-stu-id="b0a87-229">Int16</span></span> |
| <span data-ttu-id="b0a87-230">Decimal</span><span class="sxs-lookup"><span data-stu-id="b0a87-230">Decimal</span></span> |<span data-ttu-id="b0a87-231">Decimal</span><span class="sxs-lookup"><span data-stu-id="b0a87-231">Decimal</span></span> |
| <span data-ttu-id="b0a87-232">Duplo</span><span class="sxs-lookup"><span data-stu-id="b0a87-232">Double</span></span> |<span data-ttu-id="b0a87-233">Duplo</span><span class="sxs-lookup"><span data-stu-id="b0a87-233">Double</span></span> |
| <span data-ttu-id="b0a87-234">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="b0a87-234">Integer</span></span> |<span data-ttu-id="b0a87-235">Int32</span><span class="sxs-lookup"><span data-stu-id="b0a87-235">Int32</span></span> |
| <span data-ttu-id="b0a87-236">Número</span><span class="sxs-lookup"><span data-stu-id="b0a87-236">Number</span></span> |<span data-ttu-id="b0a87-237">Duplo</span><span class="sxs-lookup"><span data-stu-id="b0a87-237">Double</span></span> |
| <span data-ttu-id="b0a87-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b0a87-238">SmallInt</span></span> |<span data-ttu-id="b0a87-239">Int16</span><span class="sxs-lookup"><span data-stu-id="b0a87-239">Int16</span></span> |
| <span data-ttu-id="b0a87-240">Data</span><span class="sxs-lookup"><span data-stu-id="b0a87-240">Date</span></span> |<span data-ttu-id="b0a87-241">DateTime</span><span class="sxs-lookup"><span data-stu-id="b0a87-241">DateTime</span></span> |
| <span data-ttu-id="b0a87-242">Hora</span><span class="sxs-lookup"><span data-stu-id="b0a87-242">Time</span></span> |<span data-ttu-id="b0a87-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-243">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-244">Hora com fuso horário</span><span class="sxs-lookup"><span data-stu-id="b0a87-244">Time With Time Zone</span></span> |<span data-ttu-id="b0a87-245">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-245">String</span></span> |
| <span data-ttu-id="b0a87-246">Timestamp</span><span class="sxs-lookup"><span data-stu-id="b0a87-246">Timestamp</span></span> |<span data-ttu-id="b0a87-247">DateTime</span><span class="sxs-lookup"><span data-stu-id="b0a87-247">DateTime</span></span> |
| <span data-ttu-id="b0a87-248">Timestamp With Time Zone</span><span class="sxs-lookup"><span data-stu-id="b0a87-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="b0a87-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="b0a87-249">DateTimeOffset</span></span> |
| <span data-ttu-id="b0a87-250">Intervalo - dia</span><span class="sxs-lookup"><span data-stu-id="b0a87-250">Interval Day</span></span> |<span data-ttu-id="b0a87-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-251">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-252">Intervalo dia tooHour</span><span class="sxs-lookup"><span data-stu-id="b0a87-252">Interval Day tooHour</span></span> |<span data-ttu-id="b0a87-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-253">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-254">Intervalo dia tooMinute</span><span class="sxs-lookup"><span data-stu-id="b0a87-254">Interval Day tooMinute</span></span> |<span data-ttu-id="b0a87-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-255">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-256">Intervalo dia tooSecond</span><span class="sxs-lookup"><span data-stu-id="b0a87-256">Interval Day tooSecond</span></span> |<span data-ttu-id="b0a87-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-257">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-258">Intervalo - hora</span><span class="sxs-lookup"><span data-stu-id="b0a87-258">Interval Hour</span></span> |<span data-ttu-id="b0a87-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-259">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-260">TooMinute de hora do intervalo</span><span class="sxs-lookup"><span data-stu-id="b0a87-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="b0a87-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-261">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-262">TooSecond de hora do intervalo</span><span class="sxs-lookup"><span data-stu-id="b0a87-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="b0a87-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-263">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-264">Interval Minute</span><span class="sxs-lookup"><span data-stu-id="b0a87-264">Interval Minute</span></span> |<span data-ttu-id="b0a87-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-265">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-266">TooSecond minutos de intervalo</span><span class="sxs-lookup"><span data-stu-id="b0a87-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="b0a87-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-267">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-268">Interval Second</span><span class="sxs-lookup"><span data-stu-id="b0a87-268">Interval Second</span></span> |<span data-ttu-id="b0a87-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b0a87-269">TimeSpan</span></span> |
| <span data-ttu-id="b0a87-270">Interval Year</span><span class="sxs-lookup"><span data-stu-id="b0a87-270">Interval Year</span></span> |<span data-ttu-id="b0a87-271">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-271">String</span></span> |
| <span data-ttu-id="b0a87-272">Intervalo ano tooMonth</span><span class="sxs-lookup"><span data-stu-id="b0a87-272">Interval Year tooMonth</span></span> |<span data-ttu-id="b0a87-273">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-273">String</span></span> |
| <span data-ttu-id="b0a87-274">Interval Month</span><span class="sxs-lookup"><span data-stu-id="b0a87-274">Interval Month</span></span> |<span data-ttu-id="b0a87-275">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-275">String</span></span> |
| <span data-ttu-id="b0a87-276">Period(Date)</span><span class="sxs-lookup"><span data-stu-id="b0a87-276">Period(Date)</span></span> |<span data-ttu-id="b0a87-277">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-277">String</span></span> |
| <span data-ttu-id="b0a87-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="b0a87-278">Period(Time)</span></span> |<span data-ttu-id="b0a87-279">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-279">String</span></span> |
| <span data-ttu-id="b0a87-280">Period(Time With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="b0a87-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="b0a87-281">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-281">String</span></span> |
| <span data-ttu-id="b0a87-282">Period(Timestamp)</span><span class="sxs-lookup"><span data-stu-id="b0a87-282">Period(Timestamp)</span></span> |<span data-ttu-id="b0a87-283">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-283">String</span></span> |
| <span data-ttu-id="b0a87-284">Period(Timestamp With Time Zone)</span><span class="sxs-lookup"><span data-stu-id="b0a87-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="b0a87-285">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-285">String</span></span> |
| <span data-ttu-id="b0a87-286">Xml</span><span class="sxs-lookup"><span data-stu-id="b0a87-286">Xml</span></span> |<span data-ttu-id="b0a87-287">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="b0a87-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="b0a87-288">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="b0a87-288">Map source toosink columns</span></span>
<span data-ttu-id="b0a87-289">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b0a87-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="b0a87-290">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="b0a87-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="b0a87-291">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="b0a87-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="b0a87-292">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="b0a87-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b0a87-293">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="b0a87-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="b0a87-294">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="b0a87-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="b0a87-295">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="b0a87-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b0a87-296">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="b0a87-296">Performance and Tuning</span></span>
<span data-ttu-id="b0a87-297">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="b0a87-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
