---
title: Copiar dados para dentro e fora do Oracle usando o Data Factory | Microsoft Docs
description: "Aprenda a copiar dados de/para o banco de dados da Oracle que está no local usando o Azure Data Factory."
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
ms.openlocfilehash: bb6af719fe6f1a30c5933ce4342a4c0c072f3ff4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="e901e-103">Copiar dados para dentro e fora do Oracle local usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e901e-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="e901e-104">Esse artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados para/de um banco de dados do Oracle local.</span><span class="sxs-lookup"><span data-stu-id="e901e-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="e901e-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="e901e-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="e901e-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="e901e-106">Supported scenarios</span></span>
<span data-ttu-id="e901e-107">Você pode copiar dados **de um banco de dados Oracle** para os seguintes armazenamentos de dados:</span><span class="sxs-lookup"><span data-stu-id="e901e-107">You can copy data **from an Oracle database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="e901e-108">Você pode copiar dados dos seguintes armazenamentos de dados **para um banco de dados Oracle**:</span><span class="sxs-lookup"><span data-stu-id="e901e-108">You can copy data from the following data stores **to an Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="e901e-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e901e-109">Prerequisites</span></span>
<span data-ttu-id="e901e-110">O Data Factory dá suporte à conexão com fontes Oracle locais usando o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="e901e-110">Data Factory supports connecting to on-premises Oracle sources using the Data Management Gateway.</span></span> <span data-ttu-id="e901e-111">Veja o artigo [Gateway de gerenciamento de dados](data-factory-data-management-gateway.md) para saber mais sobre o Gateway de Gerenciamento de Dados e o artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter instruções passo a passo sobre como configurar o gateway de um pipeline de dados para mover dados.</span><span class="sxs-lookup"><span data-stu-id="e901e-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article to learn about Data Management Gateway and [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up the gateway a data pipeline to move data.</span></span>

<span data-ttu-id="e901e-112">O gateway é requerido mesmo que o banco de dados Oracle esteja hospedado em uma VM IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="e901e-112">Gateway is required even if the Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="e901e-113">Você pode instalar o gateway na mesma VM IaaS do armazenamento de dados ou em uma VM diferente, desde que o gateway possa conectar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e901e-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="e901e-114">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="e901e-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="e901e-115">Instalação e versões com suporte</span><span class="sxs-lookup"><span data-stu-id="e901e-115">Supported versions and installation</span></span>
<span data-ttu-id="e901e-116">Este conector Oracle dá suporte a duas versões de drivers:</span><span class="sxs-lookup"><span data-stu-id="e901e-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="e901e-117">**Driver da Microsoft para Oracle (recomendado)**: iniciando do gateway de gerenciamento de dados versão 2.7, um driver da Microsoft para Oracle é automaticamente instalado junto com o gateway, de modo que você não precisa manipular adicionalmente o driver para estabelecer a conectividade para o Oracle e você também pode ter melhor desempenho de cópia usando este driver.</span><span class="sxs-lookup"><span data-stu-id="e901e-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with the gateway, so you don't need to additionally handle the driver in order to establish connectivity to Oracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="e901e-118">Há suporte para as versões abaixo de bancos de dados Oracle:</span><span class="sxs-lookup"><span data-stu-id="e901e-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="e901e-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="e901e-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="e901e-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="e901e-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="e901e-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="e901e-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="e901e-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="e901e-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="e901e-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="e901e-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e901e-124">Atualmente o driver da Microsoft para Oracle suporta apenas copiando dados do Oracle, mas não gravar no Oracle.</span><span class="sxs-lookup"><span data-stu-id="e901e-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing to Oracle.</span></span> <span data-ttu-id="e901e-125">E observe que a capacidade de conexão de teste na guia Diagnóstico de Gateway de gerenciamento de dados não oferece suporte a este driver.</span><span class="sxs-lookup"><span data-stu-id="e901e-125">And note the test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="e901e-126">Como alternativa, você pode usar o Assistente para copiar para validar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="e901e-126">Alternatively, you can use the copy wizard to validate the connectivity.</span></span>
>

- <span data-ttu-id="e901e-127">**Provedor de dados Oracle para .NET:** também é possível usar o provedor de dados Oracle para copiar dados de/para Oracle.</span><span class="sxs-lookup"><span data-stu-id="e901e-127">**Oracle Data Provider for .NET:** you can also choose to use Oracle Data Provider to copy data from/to Oracle.</span></span> <span data-ttu-id="e901e-128">Esse componente está incluído nos [Componentes de Acesso a Dados do Oracle para Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e901e-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="e901e-129">Instale a versão adequada (32/64 bits) no computador em que o gateway está instalado.</span><span class="sxs-lookup"><span data-stu-id="e901e-129">Install the appropriate version (32/64 bit) on the machine where the gateway is installed.</span></span> <span data-ttu-id="e901e-130">[O Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) pode acessar o Oracle Database 10g Release 2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e901e-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access to Oracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="e901e-131">Se você escolher "Instalação de XCopy", siga as etapas no readme.htm.</span><span class="sxs-lookup"><span data-stu-id="e901e-131">If you choose “XCopy Installation”, follow steps in the readme.htm.</span></span> <span data-ttu-id="e901e-132">É recomendável escolher o instalador com IU (não XCopy).</span><span class="sxs-lookup"><span data-stu-id="e901e-132">We recommend you choose the installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="e901e-133">Depois de instalar o provedor, **reinicie** o serviço de Host do Gateway de Gerenciamento de Dados no seu computador usando o miniaplicativo Serviços (ou) o Gerenciador de Configuração do Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="e901e-133">After installing the provider, **restart** the Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="e901e-134">Se você usar o assistente de cópia para criar o pipeline de cópia, o tipo de driver será determinado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e901e-134">If you use copy wizard to author the copy pipeline, the driver type will be auto-determined.</span></span> <span data-ttu-id="e901e-135">O driver da Microsoft será usado por padrão, a menos que sua versão do gateway seja menor do que 2.7 ou você escolher o Oracle como um coletor.</span><span class="sxs-lookup"><span data-stu-id="e901e-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e901e-136">Introdução</span><span class="sxs-lookup"><span data-stu-id="e901e-136">Getting started</span></span>
<span data-ttu-id="e901e-137">Você pode criar um pipeline com atividade de cópia que move dados de/para um banco de dados Oracle local por meio de ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="e901e-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="e901e-138">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="e901e-138">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="e901e-139">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="e901e-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="e901e-140">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="e901e-140">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e901e-141">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="e901e-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="e901e-142">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="e901e-142">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="e901e-143">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="e901e-143">Create a **data factory**.</span></span> <span data-ttu-id="e901e-144">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="e901e-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="e901e-145">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="e901e-145">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="e901e-146">Por exemplo, se você estiver copiando dados de um banco de dados Oracle para um armazenamento de blobs do Azure, crie dois serviços vinculados para vincular seu banco de dados Oracle e conta de armazenamento do Azure ao data factory.</span><span class="sxs-lookup"><span data-stu-id="e901e-146">For example, if you are copying data from an Oralce database to an Azure blob storage, you create two linked services to link your Oracle database and Azure storage account to your data factory.</span></span> <span data-ttu-id="e901e-147">Para propriedades do serviço vinculado específicas do Oracle, consulte a seção [propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-147">For linked service properties that are specific to Oracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="e901e-148">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="e901e-148">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="e901e-149">No exemplo mencionado na última etapa, você cria um conjunto de dados para especificar a tabela no banco de dados Oracle que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="e901e-149">In the example mentioned in the last step, you create a dataset to specify the table in your Oracle database that contains the input data.</span></span> <span data-ttu-id="e901e-150">Em seguida, você cria outro conjunto de dados para especificar o contêiner de blob e a pasta que contém os dados copiados do banco de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="e901e-150">And, you create another dataset to specify the blob container and the folder that holds the data copied from the Oracle database.</span></span> <span data-ttu-id="e901e-151">Para propriedades de conjunto de dados específicas do Oracle, consulte a seção [propriedades do conjunto de dados](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-151">For dataset properties that are specific to Oracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="e901e-152">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="e901e-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="e901e-153">No exemplo mencionado anteriormente, você usa OracleSource como fonte e BlobSink como coletor para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="e901e-153">In the example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="e901e-154">De modo similar, se você estiver copiando do Armazenamento de Blobs do Azure para o banco de dados Oracle, use BlobSource e OracleSink na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="e901e-154">Similarly, if you are copying from Azure Blob Storage to Oracle Database, you use BlobSource and OracleSink in the copy activity.</span></span> <span data-ttu-id="e901e-155">Para propriedades da atividade de cópia específicas do banco de dados Oracle, consulte a seção [propriedades da atividade de cópia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-155">For copy activity properties that are specific to Oracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="e901e-156">Para obter detalhes sobre como usar um armazenamento de dados como uma origem ou um coletor, clique no link na seção anterior para o seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="e901e-156">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="e901e-157">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="e901e-157">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="e901e-158">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e901e-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="e901e-159">Para obter exemplos com definições de JSON das entidades do Data Factory usadas para copiar dados bidirecionalmente em um banco de dados do Oracle local, confira a seção [Exemplos de JSON](#json-examples-for-copying-data-to-and-from-oracle-database) neste artigo.</span><span class="sxs-lookup"><span data-stu-id="e901e-159">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="e901e-160">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory:</span><span class="sxs-lookup"><span data-stu-id="e901e-160">The following sections provide details about JSON properties that are used to define Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="e901e-161">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="e901e-161">Linked service properties</span></span>
<span data-ttu-id="e901e-162">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do Oracle.</span><span class="sxs-lookup"><span data-stu-id="e901e-162">The following table provides description for JSON elements specific to Oracle linked service.</span></span>

| <span data-ttu-id="e901e-163">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e901e-163">Property</span></span> | <span data-ttu-id="e901e-164">Descrição</span><span class="sxs-lookup"><span data-stu-id="e901e-164">Description</span></span> | <span data-ttu-id="e901e-165">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e901e-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e901e-166">type</span><span class="sxs-lookup"><span data-stu-id="e901e-166">type</span></span> |<span data-ttu-id="e901e-167">A propriedade do tipo deve ser definida como: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="e901e-167">The type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="e901e-168">Sim</span><span class="sxs-lookup"><span data-stu-id="e901e-168">Yes</span></span> |
| <span data-ttu-id="e901e-169">driverType</span><span class="sxs-lookup"><span data-stu-id="e901e-169">driverType</span></span> | <span data-ttu-id="e901e-170">Especifique qual driver a ser usado para copiar dados de/para o banco de dados Oracle.</span><span class="sxs-lookup"><span data-stu-id="e901e-170">Specify which driver to use to copy data from/to Oracle Database.</span></span> <span data-ttu-id="e901e-171">Valores permitidos são **Microsoft** ou **ODP** (padrão).</span><span class="sxs-lookup"><span data-stu-id="e901e-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="e901e-172">Consulte [suporte para instalação e da versão](#supported-versions-and-installation) seção detalhes do driver.</span><span class="sxs-lookup"><span data-stu-id="e901e-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="e901e-173">Não</span><span class="sxs-lookup"><span data-stu-id="e901e-173">No</span></span> |
| <span data-ttu-id="e901e-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="e901e-174">connectionString</span></span> | <span data-ttu-id="e901e-175">Especifique as informações necessárias para se conectar à instância do Banco de Dados Oracle para a propriedade connectionString.</span><span class="sxs-lookup"><span data-stu-id="e901e-175">Specify information needed to connect to the Oracle Database instance for the connectionString property.</span></span> | <span data-ttu-id="e901e-176">Sim</span><span class="sxs-lookup"><span data-stu-id="e901e-176">Yes</span></span> |
| <span data-ttu-id="e901e-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="e901e-177">gatewayName</span></span> | <span data-ttu-id="e901e-178">Nome do gateway usado para conectar o servidor Oracle local</span><span class="sxs-lookup"><span data-stu-id="e901e-178">Name of the gateway that that is used to connect to the on-premises Oracle server</span></span> |<span data-ttu-id="e901e-179">Sim</span><span class="sxs-lookup"><span data-stu-id="e901e-179">Yes</span></span> |

<span data-ttu-id="e901e-180">**Exemplo: usando o driver da Microsoft:**</span><span class="sxs-lookup"><span data-stu-id="e901e-180">**Example: using Microsoft driver:**</span></span>
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

<span data-ttu-id="e901e-181">**Exemplo: usando o driver ODP**</span><span class="sxs-lookup"><span data-stu-id="e901e-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="e901e-182">Consulte [este site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) para conferir os formatos permitidos.</span><span class="sxs-lookup"><span data-stu-id="e901e-182">Refer to [this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for the allowed formats.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="e901e-183">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="e901e-183">Dataset properties</span></span>
<span data-ttu-id="e901e-184">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="e901e-184">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e901e-185">As seções, como estrutura, disponibilidade e política de um JSON do conjunto de dados, são parecidas para todos os tipos de conjunto de dados (Oracle, blob do Azure, tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="e901e-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e901e-186">A seção typeProperties é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="e901e-186">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="e901e-187">A seção typeProperties do conjunto de dados do tipo OracleTable tem as propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="e901e-187">The typeProperties section for the dataset of type OracleTable has the following properties:</span></span>

| <span data-ttu-id="e901e-188">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e901e-188">Property</span></span> | <span data-ttu-id="e901e-189">Descrição</span><span class="sxs-lookup"><span data-stu-id="e901e-189">Description</span></span> | <span data-ttu-id="e901e-190">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e901e-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e901e-191">tableName</span><span class="sxs-lookup"><span data-stu-id="e901e-191">tableName</span></span> |<span data-ttu-id="e901e-192">Nome da tabela no Banco de Dados Oracle à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="e901e-192">Name of the table in the Oracle Database that the linked service refers to.</span></span> |<span data-ttu-id="e901e-193">Não (se **oracleReaderQuery** de **OracleSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="e901e-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="e901e-194">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="e901e-194">Copy activity properties</span></span>
<span data-ttu-id="e901e-195">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="e901e-195">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e901e-196">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="e901e-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="e901e-197">A Atividade de cópia usa apenas uma entrada e produz apenas uma saída.</span><span class="sxs-lookup"><span data-stu-id="e901e-197">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="e901e-198">Por outro lado, as propriedades disponíveis na seção typeProperties da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="e901e-198">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="e901e-199">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="e901e-199">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="e901e-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="e901e-200">OracleSource</span></span>
<span data-ttu-id="e901e-201">Na Atividade de Cópia, quando a fonte é do tipo **OracleSource**, as seguintes propriedades estão disponíveis na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="e901e-201">In Copy activity, when the source is of type **OracleSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="e901e-202">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e901e-202">Property</span></span> | <span data-ttu-id="e901e-203">Descrição</span><span class="sxs-lookup"><span data-stu-id="e901e-203">Description</span></span> | <span data-ttu-id="e901e-204">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="e901e-204">Allowed values</span></span> | <span data-ttu-id="e901e-205">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e901e-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e901e-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="e901e-206">oracleReaderQuery</span></span> |<span data-ttu-id="e901e-207">Utiliza a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="e901e-207">Use the custom query to read data.</span></span> |<span data-ttu-id="e901e-208">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="e901e-208">SQL query string.</span></span> <span data-ttu-id="e901e-209">Por exemplo: select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="e901e-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="e901e-210">Se não for especificada, a instrução SQL que é executada é: select * from MyTable</span><span class="sxs-lookup"><span data-stu-id="e901e-210">If not specified, the SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="e901e-211">Não (se **tableName** de **dataset** for especificado)</span><span class="sxs-lookup"><span data-stu-id="e901e-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="e901e-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="e901e-212">OracleSink</span></span>
<span data-ttu-id="e901e-213">**OracleSink** é compatível com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="e901e-213">**OracleSink** supports the following properties:</span></span>

| <span data-ttu-id="e901e-214">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e901e-214">Property</span></span> | <span data-ttu-id="e901e-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="e901e-215">Description</span></span> | <span data-ttu-id="e901e-216">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="e901e-216">Allowed values</span></span> | <span data-ttu-id="e901e-217">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e901e-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e901e-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e901e-218">writeBatchTimeout</span></span> |<span data-ttu-id="e901e-219">Tempo de espera para a operação de inserção em lotes ser concluída antes de atingir o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="e901e-219">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="e901e-220">timespan</span><span class="sxs-lookup"><span data-stu-id="e901e-220">timespan</span></span><br/><br/> <span data-ttu-id="e901e-221">Exemplo: "00:30:00" (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="e901e-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="e901e-222">Não</span><span class="sxs-lookup"><span data-stu-id="e901e-222">No</span></span> |
| <span data-ttu-id="e901e-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e901e-223">writeBatchSize</span></span> |<span data-ttu-id="e901e-224">Insere dados na tabela SQL quando o tamanho do buffer atinge writeBatchSize.</span><span class="sxs-lookup"><span data-stu-id="e901e-224">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="e901e-225">Inteiro (número de linhas)</span><span class="sxs-lookup"><span data-stu-id="e901e-225">Integer (number of rows)</span></span> |<span data-ttu-id="e901e-226">Não (padrão: 100)</span><span class="sxs-lookup"><span data-stu-id="e901e-226">No (default: 100)</span></span> |
| <span data-ttu-id="e901e-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="e901e-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="e901e-228">Especifique uma consulta da Atividade de Cópia a executar para que os dados de uma fatia específica sejam removidos.</span><span class="sxs-lookup"><span data-stu-id="e901e-228">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="e901e-229">Uma instrução de consulta.</span><span class="sxs-lookup"><span data-stu-id="e901e-229">A query statement.</span></span> |<span data-ttu-id="e901e-230">Não</span><span class="sxs-lookup"><span data-stu-id="e901e-230">No</span></span> |
| <span data-ttu-id="e901e-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="e901e-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="e901e-232">Especifique o nome de coluna para a Atividade de Cópia a ser preenchido com o identificador de fatia gerado automaticamente, que é usado para limpar dados de uma fatia específica quando executado novamente.</span><span class="sxs-lookup"><span data-stu-id="e901e-232">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="e901e-233">Nome de uma coluna com tipo de dados de binário (32).</span><span class="sxs-lookup"><span data-stu-id="e901e-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="e901e-234">Não</span><span class="sxs-lookup"><span data-stu-id="e901e-234">No</span></span> |

## <a name="json-examples-for-copying-data-to-and-from-oracle-database"></a><span data-ttu-id="e901e-235">Exemplos JSON para copiar de dados de e para o banco de dados Oracle</span><span class="sxs-lookup"><span data-stu-id="e901e-235">JSON examples for copying data to and from Oracle database</span></span>
<span data-ttu-id="e901e-236">O exemplo a seguir fornece as definições de JSON de exemplo que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e901e-236">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e901e-237">Eles mostram como copiar dados de/para um banco de dados Oracle de/para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e901e-237">They show how to copy data from/to an Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="e901e-238">No entanto, os dados podem ser copiados para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e901e-238">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-to-azure-blob"></a><span data-ttu-id="e901e-239">Exemplo: copiar dados do Oracle para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="e901e-239">Example: Copy data from Oracle to Azure Blob</span></span>

<span data-ttu-id="e901e-240">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="e901e-240">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="e901e-241">Um serviço vinculado do tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="e901e-242">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e901e-243">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e901e-244">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e901e-245">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) como fonte e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) como coletor.</span><span class="sxs-lookup"><span data-stu-id="e901e-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="e901e-246">O exemplo copia os dados de uma tabela em um banco de dados Oracle local para um blob por hora.</span><span class="sxs-lookup"><span data-stu-id="e901e-246">The sample copies data from a table in an on-premises Oracle database to a blob hourly.</span></span> <span data-ttu-id="e901e-247">Para obter mais informações sobre as várias propriedades usadas no exemplo, consulte a documentação nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="e901e-247">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="e901e-248">**Serviço vinculado do Oracle:**</span><span class="sxs-lookup"><span data-stu-id="e901e-248">**Oracle linked service:**</span></span>

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

<span data-ttu-id="e901e-249">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="e901e-249">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="e901e-250">**Conjunto de dados de entrada do Oracle:**</span><span class="sxs-lookup"><span data-stu-id="e901e-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="e901e-251">O exemplo supõe que você criou uma tabela "MyTable" no Oracle e que ela contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="e901e-251">The sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="e901e-252">Configurar “external”: “true” informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e901e-252">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="e901e-253">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="e901e-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e901e-254">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="e901e-254">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e901e-255">O caminho de pasta e nome de arquivo para o blob são avaliados dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="e901e-255">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="e901e-256">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="e901e-256">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="e901e-257">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="e901e-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="e901e-258">O pipeline contém uma Atividade de Cópia configurada para usar os conjuntos de dados de entrada e saída, e está agendada para ser executada por hora.</span><span class="sxs-lookup"><span data-stu-id="e901e-258">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="e901e-259">Na definição JSON do pipeline, o tipo **source** está definido como **OracleSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e901e-259">In the pipeline JSON definition, the **source** type is set to **OracleSource** and **sink** type is set to **BlobSink**.</span></span>  <span data-ttu-id="e901e-260">A consulta SQL especificada com a propriedade **oracleReaderQuery** seleciona os dados na última hora para copiar.</span><span class="sxs-lookup"><span data-stu-id="e901e-260">The SQL query specified with **oracleReaderQuery** property selects the data in the past hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-oracle"></a><span data-ttu-id="e901e-261">Exemplo: Copiar dados do Blob do Azure para o Oracle</span><span class="sxs-lookup"><span data-stu-id="e901e-261">Example: Copy data from Azure Blob to Oracle</span></span>
<span data-ttu-id="e901e-262">Este exemplo mostra como copiar dados de um Armazenamento de Blobs do Azure para um banco de dados Oracle local.</span><span class="sxs-lookup"><span data-stu-id="e901e-262">This sample shows how to copy data from an Azure Blob Storage to an on-premises Oracle database.</span></span> <span data-ttu-id="e901e-263">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes indicadas [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e901e-263">However, data can be copied **directly** from any of the sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="e901e-264">O exemplo tem as seguintes entidades de data factory:</span><span class="sxs-lookup"><span data-stu-id="e901e-264">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="e901e-265">Um serviço vinculado do tipo [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="e901e-266">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e901e-267">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e901e-268">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e901e-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e901e-269">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) como fonte e [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) como coletor.</span><span class="sxs-lookup"><span data-stu-id="e901e-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="e901e-270">O exemplo copia dados de um blob para uma tabela em um banco de dados Oracle local de hora em hora.</span><span class="sxs-lookup"><span data-stu-id="e901e-270">The sample copies data from a blob to a table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="e901e-271">Para obter mais informações sobre as várias propriedades usadas no exemplo, consulte a documentação nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="e901e-271">For more information on various properties used in the sample, see documentation in sections following the samples.</span></span>

<span data-ttu-id="e901e-272">**Serviço vinculado do Oracle:**</span><span class="sxs-lookup"><span data-stu-id="e901e-272">**Oracle linked service:**</span></span>
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

<span data-ttu-id="e901e-273">**Serviço vinculado do armazenamento de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="e901e-273">**Azure Blob storage linked service:**</span></span>
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

<span data-ttu-id="e901e-274">**Conjunto de dados de entrada de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="e901e-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="e901e-275">Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="e901e-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e901e-276">O caminho de pasta e nome de arquivo para o blob são avaliados dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="e901e-276">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="e901e-277">O caminho da pasta usa a parte do ano, mês e dia da hora de início e o nome de arquivo usa a parte da hora de início.</span><span class="sxs-lookup"><span data-stu-id="e901e-277">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="e901e-278">A configuração “external”: ”true” informa ao serviço Data Factory que essa é uma tabela externa do data factory e não é produzida por uma atividade no data factory.</span><span class="sxs-lookup"><span data-stu-id="e901e-278">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="e901e-279">**Conjunto de dados de saída Oracle:**</span><span class="sxs-lookup"><span data-stu-id="e901e-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="e901e-280">O exemplo pressupõe que você tenha criado uma tabela "MyTable" no Oracle.</span><span class="sxs-lookup"><span data-stu-id="e901e-280">The sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="e901e-281">Crie a tabela no Oracle com o mesmo número de colunas que você espera que o arquivo CSV de Blob contenha.</span><span class="sxs-lookup"><span data-stu-id="e901e-281">Create the table in Oracle with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="e901e-282">Novas linhas são adicionadas à tabela a cada hora.</span><span class="sxs-lookup"><span data-stu-id="e901e-282">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="e901e-283">**Pipeline com Atividade de cópia:**</span><span class="sxs-lookup"><span data-stu-id="e901e-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="e901e-284">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="e901e-284">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="e901e-285">Na definição JSON do pipeline, o tipo **source** está definido como **BlobSource** e o tipo **sink** está definido como **OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="e901e-285">In the pipeline JSON definition, the **source** type is set to **BlobSource** and the **sink** type is set to **OracleSink**.</span></span>  

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


## <a name="troubleshooting-tips"></a><span data-ttu-id="e901e-286">Dicas de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="e901e-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="e901e-287">Problema 1: Provedor de dados do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e901e-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="e901e-288">Se você vir a seguinte **mensagem de erro**:</span><span class="sxs-lookup"><span data-stu-id="e901e-288">You see the following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable to find the requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="e901e-289">**Possíveis causas:**</span><span class="sxs-lookup"><span data-stu-id="e901e-289">**Possible causes:**</span></span>

1. <span data-ttu-id="e901e-290">O provedor de dados .NET Framework para Oracle não foi instalado.</span><span class="sxs-lookup"><span data-stu-id="e901e-290">The .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="e901e-291">O provedor de dados .NET Framework para Oracle foi instalado no .NET Framework 2.0 e não foi encontrado nas pastas .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="e901e-291">The .NET Framework Data Provider for Oracle was installed to .NET Framework 2.0 and is not found in the .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="e901e-292">**Resolução/Solução Alternativa:**</span><span class="sxs-lookup"><span data-stu-id="e901e-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="e901e-293">Se você não instalou o Provedor do .NET para o Oracle, [instale-o](http://www.oracle.com/technetwork/topics/dotnet/downloads/) e repita o cenário.</span><span class="sxs-lookup"><span data-stu-id="e901e-293">If you haven't installed the .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry the scenario.</span></span>
2. <span data-ttu-id="e901e-294">Se você receber a mensagem de erro mesmo depois de instalar o provedor, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e901e-294">If you get the error message even after installing the provider, do the following steps:</span></span>
   1. <span data-ttu-id="e901e-295">Abra a configuração do computador do .NET 2.0 na pasta: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="e901e-295">Open machine config of .NET 2.0 from the folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="e901e-296">Procure **Provedor de Dados Oracle para .NET**, e você poderá encontrar uma entrada, conforme mostrado no exemplo a seguir em **system.data** -> **DbProviderFactories**: "<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Provedor de Dados Oracle para .NET</span><span class="sxs-lookup"><span data-stu-id="e901e-296">Search for **Oracle Data Provider for .NET**, and you should be able to find an entry as shown in the following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="e901e-297">”</span><span class="sxs-lookup"><span data-stu-id="e901e-297">”</span></span>
3. <span data-ttu-id="e901e-298">Copie esta entrada no arquivo machine.config na seguinte pasta v4.0: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config e altere a versão para 4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="e901e-298">Copy this entry to the machine.config file in the following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change the version to 4.xxx.x.x.</span></span>
4. <span data-ttu-id="e901e-299">Instale “<Caminho Instalado do ODP.NET> \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” no GAC (cache de assembly global), executando `gacutil /i [provider path]`.## Dicas de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="e901e-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into the global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="e901e-300">Problema 2: formatação de datetime</span><span class="sxs-lookup"><span data-stu-id="e901e-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="e901e-301">Se você vir a seguinte **mensagem de erro**:</span><span class="sxs-lookup"><span data-stu-id="e901e-301">You see the following **error message**:</span></span>

    Message=Operation failed in Oracle Database with the following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="e901e-302">**Resolução/Solução Alternativa:**</span><span class="sxs-lookup"><span data-stu-id="e901e-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="e901e-303">Talvez seja necessário ajustar a cadeia de caracteres de consulta em sua atividade de cópia com base em como as datas são configuradas no banco de dados Oracle, conforme mostrado no exemplo a seguir (usando a função to_date):</span><span class="sxs-lookup"><span data-stu-id="e901e-303">You may need to adjust the query string in your copy activity based on how dates are configured in your Oracle database, as shown in the following sample (using the to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="e901e-304">Mapeamento de tipo para Oracle</span><span class="sxs-lookup"><span data-stu-id="e901e-304">Type mapping for Oracle</span></span>
<span data-ttu-id="e901e-305">Como mencionado no artigo sobre as [atividades da movimentação de dados](data-factory-data-movement-activities.md) , a atividade de Cópia executa conversões automáticas dos tipos de fonte nos tipos de coletor com a seguinte abordagem de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="e901e-305">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="e901e-306">Converter de tipos de fonte nativos para o tipo .NET</span><span class="sxs-lookup"><span data-stu-id="e901e-306">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="e901e-307">Converter do tipo .NET para o tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="e901e-307">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="e901e-308">Ao mover dados do Oracle, os seguintes mapeamentos são usados do tipo de dados do Oracle para o tipo .NET e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="e901e-308">When moving data from Oracle, the following mappings are used from Oracle data type to .NET type and vice versa.</span></span>

| <span data-ttu-id="e901e-309">Tipo de dados do Oracle</span><span class="sxs-lookup"><span data-stu-id="e901e-309">Oracle data type</span></span> | <span data-ttu-id="e901e-310">Tipo de dados do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="e901e-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="e901e-311">BFILE</span><span class="sxs-lookup"><span data-stu-id="e901e-311">BFILE</span></span> |<span data-ttu-id="e901e-312">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e901e-312">Byte[]</span></span> |
| <span data-ttu-id="e901e-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="e901e-313">BLOB</span></span> |<span data-ttu-id="e901e-314">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e901e-314">Byte[]</span></span> |
| <span data-ttu-id="e901e-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="e901e-315">CHAR</span></span> |<span data-ttu-id="e901e-316">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e901e-316">String</span></span> |
| <span data-ttu-id="e901e-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="e901e-317">CLOB</span></span> |<span data-ttu-id="e901e-318">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e901e-318">String</span></span> |
| <span data-ttu-id="e901e-319">DATE</span><span class="sxs-lookup"><span data-stu-id="e901e-319">DATE</span></span> |<span data-ttu-id="e901e-320">DateTime</span><span class="sxs-lookup"><span data-stu-id="e901e-320">DateTime</span></span> |
| <span data-ttu-id="e901e-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="e901e-321">FLOAT</span></span> |<span data-ttu-id="e901e-322">Decimal, cadeia de caracteres (se precisão > 28)</span><span class="sxs-lookup"><span data-stu-id="e901e-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="e901e-323">INTEGER</span><span class="sxs-lookup"><span data-stu-id="e901e-323">INTEGER</span></span> |<span data-ttu-id="e901e-324">Decimal, cadeia de caracteres (se precisão > 28)</span><span class="sxs-lookup"><span data-stu-id="e901e-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="e901e-325">INTERVAL YEAR TO MONTH</span><span class="sxs-lookup"><span data-stu-id="e901e-325">INTERVAL YEAR TO MONTH</span></span> |<span data-ttu-id="e901e-326">Int32</span><span class="sxs-lookup"><span data-stu-id="e901e-326">Int32</span></span> |
| <span data-ttu-id="e901e-327">INTERVAL DAY TO SECOND</span><span class="sxs-lookup"><span data-stu-id="e901e-327">INTERVAL DAY TO SECOND</span></span> |<span data-ttu-id="e901e-328">timespan</span><span class="sxs-lookup"><span data-stu-id="e901e-328">TimeSpan</span></span> |
| <span data-ttu-id="e901e-329">LONG</span><span class="sxs-lookup"><span data-stu-id="e901e-329">LONG</span></span> |<span data-ttu-id="e901e-330">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e901e-330">String</span></span> |
| <span data-ttu-id="e901e-331">LONG RAW</span><span class="sxs-lookup"><span data-stu-id="e901e-331">LONG RAW</span></span> |<span data-ttu-id="e901e-332">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e901e-332">Byte[]</span></span> |
| <span data-ttu-id="e901e-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="e901e-333">NCHAR</span></span> |<span data-ttu-id="e901e-334">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e901e-334">String</span></span> |
| <span data-ttu-id="e901e-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="e901e-335">NCLOB</span></span> |<span data-ttu-id="e901e-336">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e901e-336">String</span></span> |
| <span data-ttu-id="e901e-337">NUMBER</span><span class="sxs-lookup"><span data-stu-id="e901e-337">NUMBER</span></span> |<span data-ttu-id="e901e-338">Decimal, cadeia de caracteres (se precisão > 28)</span><span class="sxs-lookup"><span data-stu-id="e901e-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="e901e-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="e901e-339">NVARCHAR2</span></span> |<span data-ttu-id="e901e-340">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e901e-340">String</span></span> |
| <span data-ttu-id="e901e-341">RAW</span><span class="sxs-lookup"><span data-stu-id="e901e-341">RAW</span></span> |<span data-ttu-id="e901e-342">Byte[]</span><span class="sxs-lookup"><span data-stu-id="e901e-342">Byte[]</span></span> |
| <span data-ttu-id="e901e-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="e901e-343">ROWID</span></span> |<span data-ttu-id="e901e-344">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e901e-344">String</span></span> |
| <span data-ttu-id="e901e-345">TIMESTAMP</span><span class="sxs-lookup"><span data-stu-id="e901e-345">TIMESTAMP</span></span> |<span data-ttu-id="e901e-346">DateTime</span><span class="sxs-lookup"><span data-stu-id="e901e-346">DateTime</span></span> |
| <span data-ttu-id="e901e-347">TIMESTAMP WITH LOCAL TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="e901e-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="e901e-348">DateTime</span><span class="sxs-lookup"><span data-stu-id="e901e-348">DateTime</span></span> |
| <span data-ttu-id="e901e-349">TIMESTAMP WITH TIME ZONE</span><span class="sxs-lookup"><span data-stu-id="e901e-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="e901e-350">DateTime</span><span class="sxs-lookup"><span data-stu-id="e901e-350">DateTime</span></span> |
| <span data-ttu-id="e901e-351">UNSIGNED INTEGER</span><span class="sxs-lookup"><span data-stu-id="e901e-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="e901e-352">NUMBER</span><span class="sxs-lookup"><span data-stu-id="e901e-352">Number</span></span> |
| <span data-ttu-id="e901e-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="e901e-353">VARCHAR2</span></span> |<span data-ttu-id="e901e-354">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e901e-354">String</span></span> |
| <span data-ttu-id="e901e-355">XML</span><span class="sxs-lookup"><span data-stu-id="e901e-355">XML</span></span> |<span data-ttu-id="e901e-356">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e901e-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="e901e-357">Tipo de dados **intervalo ano para mês** e **intervalo dia para segundo** não têm suporte ao usar o driver da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e901e-357">Data type **INTERVAL YEAR TO MONTH** and **INTERVAL DAY TO SECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="e901e-358">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="e901e-358">Map source to sink columns</span></span>
<span data-ttu-id="e901e-359">Para saber mais sobre mapeamento de colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="e901e-359">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="e901e-360">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="e901e-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="e901e-361">Ao copiar dados de armazenamentos de dados relacionais, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="e901e-361">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="e901e-362">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="e901e-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="e901e-363">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="e901e-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="e901e-364">Quando uma fatia é executada novamente, seja de que maneira for, você precisa garantir que os mesmos dados sejam lidos não importa quantas vezes uma fatia seja executada.</span><span class="sxs-lookup"><span data-stu-id="e901e-364">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="e901e-365">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="e901e-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e901e-366">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="e901e-366">Performance and Tuning</span></span>
<span data-ttu-id="e901e-367">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="e901e-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
