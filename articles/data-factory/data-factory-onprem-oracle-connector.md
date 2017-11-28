---
title: "dados de aaaCopy para/da Oracle usando a fábrica de dados | Microsoft Docs"
description: "Saiba como toocopy dados de/para o banco de dados Oracle que está no local usando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="6ddd9-103">Copiar dados para dentro e fora do Oracle local usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6ddd9-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="6ddd9-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de/para o banco de dados Oracle local.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="6ddd9-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="6ddd9-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="6ddd9-106">Supported scenarios</span></span>
<span data-ttu-id="6ddd9-107">Você pode copiar dados **de um banco de dados Oracle** toohello repositórios de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="6ddd9-108">Você pode copiar dados de saudação armazenamentos de dados a seguir **tooan banco de dados Oracle**:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="6ddd9-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6ddd9-109">Prerequisites</span></span>
<span data-ttu-id="6ddd9-110">Fábrica de dados dá suporte a fontes de Oracle local tooon conexão usando Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="6ddd9-111">Consulte [Data Management Gateway](data-factory-data-management-gateway.md) toolearn artigo sobre o Gateway de gerenciamento de dados e [mover dados de local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artigo para obter instruções passo a passo sobre como configurar o gateway de saudação um pipeline de dados dados de toomove.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="6ddd9-112">Gateway é necessário mesmo que hello Oracle é hospedado em uma VM de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="6ddd9-113">Você pode instalar o gateway de saudação em Olá mesmo IaaS VM como Olá dados armazenar ou em uma máquina virtual diferente, contanto que o gateway Olá pode se conectar toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="6ddd9-114">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="6ddd9-115">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="6ddd9-115">Supported versions and installation</span></span>
<span data-ttu-id="6ddd9-116">Este conector Oracle dá suporte a duas versões de drivers:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="6ddd9-117">**Driver da Microsoft para Oracle (recomendado)**: inicial do Gateway de gerenciamento de dados versão 2.7, um driver Microsoft para Oracle é automaticamente instalado junto com o gateway Olá, portanto você não precisa tooadditionally identificador Olá driver em ordem tooestablish conectividade tooOracle e você também pode ter o melhor desempenho de cópia usando este driver.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="6ddd9-118">Há suporte para as versões abaixo de bancos de dados Oracle:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="6ddd9-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="6ddd9-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="6ddd9-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="6ddd9-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="6ddd9-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ddd9-124">Atualmente o driver da Microsoft para Oracle suporta apenas copiar dados do Oracle, mas não gravar tooOracle.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="6ddd9-125">E observe a capacidade de conexão de teste Olá no guia de diagnóstico do Gateway de gerenciamento de dados não oferece suporte a este driver.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="6ddd9-126">Como alternativa, você pode usar a conectividade de Olá Olá cópia Assistente toovalidate.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="6ddd9-127">**Provedor de dados Oracle para .NET:** você também pode escolher dados de toocopy toouse provedor de dados Oracle de / tooOracle.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="6ddd9-128">Esse componente está incluído nos [Componentes de Acesso a Dados do Oracle para Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="6ddd9-129">Instale a versão apropriada da saudação (32/64 bits) na máquina Olá onde Olá gateway está instalado.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="6ddd9-130">[Provedor de dados Oracle .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) pode acessar tooOracle banco de dados 10g versão 2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="6ddd9-131">Se você escolher "Instalação XCopy", execute as etapas no hello Readme. htm.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="6ddd9-132">Recomendamos que você escolha instalador Olá com a interface do usuário (não-XCopy um).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="6ddd9-133">Depois de instalar o provedor de saudação **reiniciar** Olá serviço de host do Gateway de gerenciamento de dados em seu computador usando os serviços miniaplicativo (ou) Gerenciador de configuração de Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="6ddd9-134">Se você usar o pipeline de cópia cópia Assistente tooauthor hello, o tipo de driver de saudação será determinado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="6ddd9-135">O driver da Microsoft será usado por padrão, a menos que sua versão do gateway seja menor do que 2.7 ou você escolher o Oracle como um coletor.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="6ddd9-136">Introdução</span><span class="sxs-lookup"><span data-stu-id="6ddd9-136">Getting started</span></span>
<span data-ttu-id="6ddd9-137">Você pode criar um pipeline com atividade de cópia que move dados de/para um banco de dados Oracle local por meio de ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="6ddd9-138">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="6ddd9-139">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="6ddd9-140">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="6ddd9-141">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="6ddd9-142">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="6ddd9-143">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-143">Create a **data factory**.</span></span> <span data-ttu-id="6ddd9-144">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="6ddd9-145">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="6ddd9-146">Por exemplo, se você estiver copiando dados de um banco de dados de Oralce tooan armazenamento de BLOBs do Azure, você criar duas toolink de serviços vinculados seu banco de dados Oracle e a fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="6ddd9-147">Para propriedades de serviço vinculado que tooOracle específico, consulte [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="6ddd9-148">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="6ddd9-149">Exemplo hello mencionado na última etapa do hello, você pode criar uma tabela de saudação do conjunto de dados toospecify no banco de dados Oracle que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="6ddd9-150">E, criar outro contêiner de blob do conjunto de dados toospecify hello e pasta Olá que contém dados saudação copiados da saudação banco de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="6ddd9-151">Para propriedades de conjunto de dados que tooOracle específico, consulte [propriedades de conjunto de dados](#dataset-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="6ddd9-152">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="6ddd9-153">Exemplo hello mencionado anteriormente, você usar OracleSource como uma origem e BlobSink como um coletor de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="6ddd9-154">Da mesma forma, se você está copiando do armazenamento de BLOBs do Azure tooOracle banco de dados, use BlobSource e OracleSink na atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="6ddd9-155">Para propriedades de atividade de cópia tooOracle específico no banco de dados, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="6ddd9-156">Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="6ddd9-157">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="6ddd9-158">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="6ddd9-159">Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um banco de dados do Oracle no local, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-oracle-database) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="6ddd9-160">Olá seções a seguir fornece detalhes sobre propriedades JSON que são entidades de fábrica de dados toodefine usado:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="6ddd9-161">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="6ddd9-161">Linked service properties</span></span>
<span data-ttu-id="6ddd9-162">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooOracle vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="6ddd9-163">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6ddd9-163">Property</span></span> | <span data-ttu-id="6ddd9-164">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ddd9-164">Description</span></span> | <span data-ttu-id="6ddd9-165">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ddd9-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ddd9-166">type</span><span class="sxs-lookup"><span data-stu-id="6ddd9-166">type</span></span> |<span data-ttu-id="6ddd9-167">propriedade de tipo Hello deve ser definida como: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="6ddd9-168">Sim</span><span class="sxs-lookup"><span data-stu-id="6ddd9-168">Yes</span></span> |
| <span data-ttu-id="6ddd9-169">driverType</span><span class="sxs-lookup"><span data-stu-id="6ddd9-169">driverType</span></span> | <span data-ttu-id="6ddd9-170">Especifique quais dados do driver toouse toocopy de / tooOracle banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="6ddd9-171">Valores permitidos são **Microsoft** ou **ODP** (padrão).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="6ddd9-172">Consulte [suporte para instalação e da versão](#supported-versions-and-installation) seção detalhes do driver.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="6ddd9-173">Não</span><span class="sxs-lookup"><span data-stu-id="6ddd9-173">No</span></span> |
| <span data-ttu-id="6ddd9-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="6ddd9-174">connectionString</span></span> | <span data-ttu-id="6ddd9-175">Especifique informações necessárias a instância de banco de dados Oracle toohello tooconnect para a propriedade connectionString de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="6ddd9-176">Sim</span><span class="sxs-lookup"><span data-stu-id="6ddd9-176">Yes</span></span> |
| <span data-ttu-id="6ddd9-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="6ddd9-177">gatewayName</span></span> | <span data-ttu-id="6ddd9-178">Nome do gateway de saudação que é usado tooconnect toohello servidor Oracle local</span><span class="sxs-lookup"><span data-stu-id="6ddd9-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="6ddd9-179">Sim</span><span class="sxs-lookup"><span data-stu-id="6ddd9-179">Yes</span></span> |

<span data-ttu-id="6ddd9-180">**Exemplo: usando o driver da Microsoft:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="6ddd9-181">**Exemplo: usando o driver ODP**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="6ddd9-182">Consulte também[este site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) para Olá formatos permitido.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="6ddd9-183">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="6ddd9-183">Dataset properties</span></span>
<span data-ttu-id="6ddd9-184">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="6ddd9-185">As seções, como estrutura, disponibilidade e política de um JSON do conjunto de dados, são parecidas para todos os tipos de conjunto de dados (Oracle, blob do Azure, tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="6ddd9-186">seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="6ddd9-187">seção de typeProperties Olá Olá conjunto de dados do tipo OracleTable tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="6ddd9-188">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6ddd9-188">Property</span></span> | <span data-ttu-id="6ddd9-189">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ddd9-189">Description</span></span> | <span data-ttu-id="6ddd9-190">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ddd9-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6ddd9-191">tableName</span><span class="sxs-lookup"><span data-stu-id="6ddd9-191">tableName</span></span> |<span data-ttu-id="6ddd9-192">Nome da tabela de saudação na Olá banco de dados Oracle que Olá serviço vinculado refere-se a.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="6ddd9-193">Não (se **oracleReaderQuery** de **OracleSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="6ddd9-194">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="6ddd9-194">Copy activity properties</span></span>
<span data-ttu-id="6ddd9-195">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="6ddd9-196">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="6ddd9-197">Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="6ddd9-198">Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="6ddd9-199">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="6ddd9-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="6ddd9-200">OracleSource</span></span>
<span data-ttu-id="6ddd9-201">Atividade de cópia, quando a fonte de saudação é do tipo **OracleSource** Olá propriedades a seguir está disponível em **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="6ddd9-202">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6ddd9-202">Property</span></span> | <span data-ttu-id="6ddd9-203">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ddd9-203">Description</span></span> | <span data-ttu-id="6ddd9-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="6ddd9-204">Allowed values</span></span> | <span data-ttu-id="6ddd9-205">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ddd9-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ddd9-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="6ddd9-206">oracleReaderQuery</span></span> |<span data-ttu-id="6ddd9-207">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="6ddd9-208">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-208">SQL query string.</span></span> <span data-ttu-id="6ddd9-209">Por exemplo: select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="6ddd9-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="6ddd9-210">Se não for especificado, Olá instrução SQL executada: selecione * de MyTable</span><span class="sxs-lookup"><span data-stu-id="6ddd9-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="6ddd9-211">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="6ddd9-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="6ddd9-212">OracleSink</span></span>
<span data-ttu-id="6ddd9-213">**OracleSink** dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="6ddd9-214">Propriedade</span><span class="sxs-lookup"><span data-stu-id="6ddd9-214">Property</span></span> | <span data-ttu-id="6ddd9-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ddd9-215">Description</span></span> | <span data-ttu-id="6ddd9-216">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="6ddd9-216">Allowed values</span></span> | <span data-ttu-id="6ddd9-217">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ddd9-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="6ddd9-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="6ddd9-218">writeBatchTimeout</span></span> |<span data-ttu-id="6ddd9-219">Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="6ddd9-220">timespan</span><span class="sxs-lookup"><span data-stu-id="6ddd9-220">timespan</span></span><br/><br/> <span data-ttu-id="6ddd9-221">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="6ddd9-222">Não</span><span class="sxs-lookup"><span data-stu-id="6ddd9-222">No</span></span> |
| <span data-ttu-id="6ddd9-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="6ddd9-223">writeBatchSize</span></span> |<span data-ttu-id="6ddd9-224">Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="6ddd9-225">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-225">Integer (number of rows)</span></span> |<span data-ttu-id="6ddd9-226">Não (padrão: 100)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-226">No (default: 100)</span></span> |
| <span data-ttu-id="6ddd9-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="6ddd9-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="6ddd9-228">Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="6ddd9-229">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-229">A query statement.</span></span> |<span data-ttu-id="6ddd9-230">Não</span><span class="sxs-lookup"><span data-stu-id="6ddd9-230">No</span></span> |
| <span data-ttu-id="6ddd9-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="6ddd9-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="6ddd9-232">Especifique o nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="6ddd9-233">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="6ddd9-234">Não</span><span class="sxs-lookup"><span data-stu-id="6ddd9-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="6ddd9-235">Exemplos JSON para copiar dados tooand do banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="6ddd9-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="6ddd9-236">Olá, exemplo a seguir fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="6ddd9-237">Eles mostram como dados toocopy / tooan Oracle banco de dados para/do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="6ddd9-238">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="6ddd9-239">Exemplo: Copiar dados de Oracle tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="6ddd9-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="6ddd9-240">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="6ddd9-241">Um serviço vinculado do tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6ddd9-242">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6ddd9-243">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6ddd9-244">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6ddd9-245">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) como fonte e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) como coletor.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="6ddd9-246">exemplo Hello copia dados de uma tabela em um blob de tooa do banco de dados de Oracle local por hora.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="6ddd9-247">Para obter mais informações sobre várias propriedades usadas no exemplo hello, consulte a documentação nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="6ddd9-248">**Serviço vinculado do Oracle:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="6ddd9-249">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="6ddd9-250">**Conjunto de dados de entrada do Oracle:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="6ddd9-251">exemplo Hello supõe que você criou uma tabela "MyTable" no Oracle e contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="6ddd9-252">Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
        },
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

<span data-ttu-id="6ddd9-253">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="6ddd9-254">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6ddd9-255">Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6ddd9-256">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            "format": {
                "type": "TextFormat",
                "columnDelimiter": "\t",
                "rowDelimiter": "\n"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="6ddd9-257">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="6ddd9-258">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é agendado toorun por hora.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="6ddd9-259">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**OracleSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="6ddd9-260">consulta SQL Olá especificada com **oracleReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="6ddd9-261">Exemplo: Copiar dados de Blob do Azure tooOracle</span><span class="sxs-lookup"><span data-stu-id="6ddd9-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="6ddd9-262">Este exemplo mostra como toocopy dados de um armazenamento de BLOBs do Azure tooan locais banco de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="6ddd9-263">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes de saudação mencionados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="6ddd9-264">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="6ddd9-265">Um serviço vinculado do tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="6ddd9-266">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="6ddd9-267">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="6ddd9-268">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="6ddd9-269">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) como fonte e [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) como coletor.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="6ddd9-270">exemplo Hello copia dados de uma tabela de tooa de blob no banco de dados Oracle local a cada hora.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="6ddd9-271">Para obter mais informações sobre várias propriedades usadas no exemplo hello, consulte a documentação nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="6ddd9-272">**Serviço vinculado do Oracle:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="6ddd9-273">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="6ddd9-274">**Conjunto de dados de entrada de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="6ddd9-275">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="6ddd9-276">Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="6ddd9-277">caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="6ddd9-278">"externo": "verdadeira" configuração informa o serviço de fábrica de dados de saudação que essa tabela é toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
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

<span data-ttu-id="6ddd9-279">**Conjunto de dados de saída Oracle:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="6ddd9-280">exemplo Hello pressupõe que você tenha criado uma tabela "MyTable" no Oracle.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="6ddd9-281">Criar tabela de saudação no Oracle com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="6ddd9-282">Novas linhas são adicionadas a tabela de toohello a cada hora.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-282">New rows are added toohello table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="6ddd9-283">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="6ddd9-284">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="6ddd9-285">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e hello **coletor** tipo está definido muito**OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a><span data-ttu-id="6ddd9-286">Dicas de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="6ddd9-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="6ddd9-287">Problema 1: Provedor de dados do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6ddd9-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="6ddd9-288">Veja a seguir Olá **mensagem de erro**:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="6ddd9-289">**Possíveis causas:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-289">**Possible causes:**</span></span>

1. <span data-ttu-id="6ddd9-290">Olá .NET Framework Data Provider for Oracle não foi instalado.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="6ddd9-291">Olá .NET Framework Data Provider for Oracle foi instalada too.NET Framework 2.0 e não for encontrado em pastas de saudação do .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="6ddd9-292">**Resolução/Solução Alternativa:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="6ddd9-293">Se você ainda não instalou Olá provedor .NET para Oracle, [instalá-lo](http://www.oracle.com/technetwork/topics/dotnet/downloads/) e repita o cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="6ddd9-294">Se você receber a mensagem de erro de saudação mesmo após a instalação do provedor de hello, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="6ddd9-295">Abra a configuração de máquina do .NET 2.0 na pasta de saudação: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="6ddd9-296">Procurar **provedor de dados Oracle para .NET**, e você deve ser capaz de toofind uma entrada conforme Olá seguindo o exemplo em **System. Data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Provedor de dados oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="6ddd9-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="6ddd9-297">”</span><span class="sxs-lookup"><span data-stu-id="6ddd9-297">”</span></span>
3. <span data-ttu-id="6ddd9-298">Copiar esse arquivo de Machine. config toohello entrada hello v 4.0 pasta a seguir: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config e alteração Olá versão too4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="6ddd9-299">Instalar "< caminho do instalado ODP.NET > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll" no cache de assembly global (GAC) do hello executando `gacutil /i [provider path]`. # # dicas de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="6ddd9-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="6ddd9-300">Problema 2: formatação de datetime</span><span class="sxs-lookup"><span data-stu-id="6ddd9-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="6ddd9-301">Veja a seguir Olá **mensagem de erro**:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="6ddd9-302">**Resolução/Solução Alternativa:**</span><span class="sxs-lookup"><span data-stu-id="6ddd9-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="6ddd9-303">Cadeia de caracteres de consulta de saudação tooadjust talvez seja necessário em sua atividade de cópia com base em como as datas são configuradas no banco de dados Oracle, conforme mostrado na seguinte Olá exemplo (usando a função to_date Olá):</span><span class="sxs-lookup"><span data-stu-id="6ddd9-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="6ddd9-304">Mapeamento de tipo para Oracle</span><span class="sxs-lookup"><span data-stu-id="6ddd9-304">Type mapping for Oracle</span></span>
<span data-ttu-id="6ddd9-305">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ddd9-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="6ddd9-306">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="6ddd9-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="6ddd9-307">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="6ddd9-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="6ddd9-308">Ao mover dados do Oracle, Olá mapeamentos a seguir é usada com too.NET tipo de dados do Oracle e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="6ddd9-309">Tipo de dados do Oracle</span><span class="sxs-lookup"><span data-stu-id="6ddd9-309">Oracle data type</span></span> | <span data-ttu-id="6ddd9-310">Tipo de dados do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6ddd9-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="6ddd9-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="6ddd9-311">BFILE</span></span> |<span data-ttu-id="6ddd9-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ddd9-312">Byte[]</span></span> |
| <span data-ttu-id="6ddd9-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="6ddd9-313">BLOB</span></span> |<span data-ttu-id="6ddd9-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ddd9-314">Byte[]</span></span> |
| <span data-ttu-id="6ddd9-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="6ddd9-315">CHAR</span></span> |<span data-ttu-id="6ddd9-316">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6ddd9-316">String</span></span> |
| <span data-ttu-id="6ddd9-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="6ddd9-317">CLOB</span></span> |<span data-ttu-id="6ddd9-318">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6ddd9-318">String</span></span> |
| <span data-ttu-id="6ddd9-319">DATE</span><span class="sxs-lookup"><span data-stu-id="6ddd9-319">DATE</span></span> |<span data-ttu-id="6ddd9-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ddd9-320">DateTime</span></span> |
| <span data-ttu-id="6ddd9-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="6ddd9-321">FLOAT</span></span> |<span data-ttu-id="6ddd9-322">Decimal, cadeia de caracteres (se precisão > 28)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="6ddd9-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="6ddd9-323">INTEGER</span></span> |<span data-ttu-id="6ddd9-324">Decimal, cadeia de caracteres (se precisão > 28)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="6ddd9-325">INTERVALO ano tooMONTH</span><span class="sxs-lookup"><span data-stu-id="6ddd9-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="6ddd9-326">Int32</span><span class="sxs-lookup"><span data-stu-id="6ddd9-326">Int32</span></span> |
| <span data-ttu-id="6ddd9-327">INTERVALO dia tooSECOND</span><span class="sxs-lookup"><span data-stu-id="6ddd9-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="6ddd9-328">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="6ddd9-328">TimeSpan</span></span> |
| <span data-ttu-id="6ddd9-329">LONG</span><span class="sxs-lookup"><span data-stu-id="6ddd9-329">LONG</span></span> |<span data-ttu-id="6ddd9-330">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6ddd9-330">String</span></span> |
| <span data-ttu-id="6ddd9-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="6ddd9-331">LONG RAW</span></span> |<span data-ttu-id="6ddd9-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ddd9-332">Byte[]</span></span> |
| <span data-ttu-id="6ddd9-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="6ddd9-333">NCHAR</span></span> |<span data-ttu-id="6ddd9-334">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6ddd9-334">String</span></span> |
| <span data-ttu-id="6ddd9-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="6ddd9-335">NCLOB</span></span> |<span data-ttu-id="6ddd9-336">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6ddd9-336">String</span></span> |
| <span data-ttu-id="6ddd9-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="6ddd9-337">NUMBER</span></span> |<span data-ttu-id="6ddd9-338">Decimal, cadeia de caracteres (se precisão > 28)</span><span class="sxs-lookup"><span data-stu-id="6ddd9-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="6ddd9-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="6ddd9-339">NVARCHAR2</span></span> |<span data-ttu-id="6ddd9-340">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6ddd9-340">String</span></span> |
| <span data-ttu-id="6ddd9-341">RAW</span><span class="sxs-lookup"><span data-stu-id="6ddd9-341">RAW</span></span> |<span data-ttu-id="6ddd9-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="6ddd9-342">Byte[]</span></span> |
| <span data-ttu-id="6ddd9-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="6ddd9-343">ROWID</span></span> |<span data-ttu-id="6ddd9-344">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6ddd9-344">String</span></span> |
| <span data-ttu-id="6ddd9-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="6ddd9-345">TIMESTAMP</span></span> |<span data-ttu-id="6ddd9-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ddd9-346">DateTime</span></span> |
| <span data-ttu-id="6ddd9-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="6ddd9-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="6ddd9-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ddd9-348">DateTime</span></span> |
| <span data-ttu-id="6ddd9-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="6ddd9-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="6ddd9-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="6ddd9-350">DateTime</span></span> |
| <span data-ttu-id="6ddd9-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="6ddd9-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="6ddd9-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="6ddd9-352">Number</span></span> |
| <span data-ttu-id="6ddd9-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="6ddd9-353">VARCHAR2</span></span> |<span data-ttu-id="6ddd9-354">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6ddd9-354">String</span></span> |
| <span data-ttu-id="6ddd9-355">XML</span><span class="sxs-lookup"><span data-stu-id="6ddd9-355">XML</span></span> |<span data-ttu-id="6ddd9-356">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="6ddd9-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="6ddd9-357">Tipo de dados **ano intervalo tooMONTH** e **tooSECOND de dia de intervalo** não são suportados ao usar o driver do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="6ddd9-358">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="6ddd9-358">Map source toosink columns</span></span>
<span data-ttu-id="6ddd9-359">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="6ddd9-360">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="6ddd9-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="6ddd9-361">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="6ddd9-362">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="6ddd9-363">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="6ddd9-364">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="6ddd9-365">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="6ddd9-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="6ddd9-366">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="6ddd9-366">Performance and Tuning</span></span>
<span data-ttu-id="6ddd9-367">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="6ddd9-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
