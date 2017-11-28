---
title: aaaMove dados de armazenamentos de dados ODBC | Microsoft Docs
description: "Saiba mais sobre como os dados toomove de dados ODBC armazena utilizando a fábrica de dados do Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="51ee0-103">Mover dados de armazenamentos de dados ODBC usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="51ee0-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="51ee0-104">Este artigo explica como armazenar toouse hello atividade de cópia em dados de toomove do Azure Data Factory de um local de dados ODBC.</span><span class="sxs-lookup"><span data-stu-id="51ee0-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="51ee0-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ee0-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="51ee0-106">Você pode copiar dados de um repositório de dados ODBC dados repositório tooany suportada coletor.</span><span class="sxs-lookup"><span data-stu-id="51ee0-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="51ee0-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="51ee0-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="51ee0-108">Fábrica de dados atualmente suporta apenas mover tooother repositórios de dados de repositório de dados de uma data ODBC, mas não para movimentação de dados de repositório de dados ODBC de tooan para repositórios de outros dados.</span><span class="sxs-lookup"><span data-stu-id="51ee0-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="51ee0-109">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="51ee0-109">Enabling connectivity</span></span>
<span data-ttu-id="51ee0-110">Serviço da fábrica de dados oferece suporte a fontes ODBC conexão local tooon usando Olá Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="51ee0-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="51ee0-111">Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ee0-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="51ee0-112">Use o armazenamento de dados ODBC Olá gateway tooconnect tooan mesmo se ele estiver hospedado em uma VM de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="51ee0-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="51ee0-113">Você pode instalar o gateway de saudação em Olá mesmo local do computador ou Olá VM do Azure como armazenamento de dados ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="51ee0-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="51ee0-114">No entanto, recomendamos que você instale o gateway de saudação em um computador separado/Azure IaaS VM tooavoid contenção de recursos e para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="51ee0-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="51ee0-115">Quando você instalar o gateway de saudação em um computador separado, máquina Olá deve ser tooaccess capaz de máquina de saudação com armazenamento de dados ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="51ee0-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="51ee0-116">Olá Data Management Gateway, além de também é necessário o driver ODBC do tooinstall Olá para Olá repositório de dados no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="51ee0-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="51ee0-117">Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.</span><span class="sxs-lookup"><span data-stu-id="51ee0-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="51ee0-118">Introdução</span><span class="sxs-lookup"><span data-stu-id="51ee0-118">Getting started</span></span>
<span data-ttu-id="51ee0-119">Você pode criar um pipeline com uma atividade de cópia que mova dados de um repositório de dados ODBC usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="51ee0-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="51ee0-120">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="51ee0-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="51ee0-121">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="51ee0-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="51ee0-122">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="51ee0-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="51ee0-123">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="51ee0-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="51ee0-124">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="51ee0-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="51ee0-125">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="51ee0-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="51ee0-126">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="51ee0-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="51ee0-127">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="51ee0-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="51ee0-128">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="51ee0-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="51ee0-129">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ee0-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="51ee0-130">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados ODBC, consulte [exemplo JSON: tooAzure Blob do repositório de dados de cópia de dados ODBC](#json-example-copy-data-from-odbc-data-store-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="51ee0-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="51ee0-131">Olá seções a seguir fornece detalhes sobre propriedades JSON de repositório de dados usado toodefine fábrica de dados entidades tooODBC específico:</span><span class="sxs-lookup"><span data-stu-id="51ee0-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="51ee0-132">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="51ee0-132">Linked service properties</span></span>
<span data-ttu-id="51ee0-133">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooODBC vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="51ee0-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="51ee0-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="51ee0-134">Property</span></span> | <span data-ttu-id="51ee0-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="51ee0-135">Description</span></span> | <span data-ttu-id="51ee0-136">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="51ee0-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51ee0-137">type</span><span class="sxs-lookup"><span data-stu-id="51ee0-137">type</span></span> |<span data-ttu-id="51ee0-138">propriedade de tipo Hello deve ser definida como: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="51ee0-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="51ee0-139">Sim</span><span class="sxs-lookup"><span data-stu-id="51ee0-139">Yes</span></span> |
| <span data-ttu-id="51ee0-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="51ee0-140">connectionString</span></span> |<span data-ttu-id="51ee0-141">Olá credencial de acesso não parte de cadeia de caracteres de conexão hello e opcional criptografados credencial.</span><span class="sxs-lookup"><span data-stu-id="51ee0-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="51ee0-142">Consulte exemplos Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="51ee0-142">See examples in hello following sections.</span></span> |<span data-ttu-id="51ee0-143">Sim</span><span class="sxs-lookup"><span data-stu-id="51ee0-143">Yes</span></span> |
| <span data-ttu-id="51ee0-144">credencial</span><span class="sxs-lookup"><span data-stu-id="51ee0-144">credential</span></span> |<span data-ttu-id="51ee0-145">parte de credencial de acesso Olá de cadeia de caracteres de conexão de saudação especificada no formato de valor de propriedade específica do driver.</span><span class="sxs-lookup"><span data-stu-id="51ee0-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="51ee0-146">Exemplo: "Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;".</span><span class="sxs-lookup"><span data-stu-id="51ee0-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="51ee0-147">Não</span><span class="sxs-lookup"><span data-stu-id="51ee0-147">No</span></span> |
| <span data-ttu-id="51ee0-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="51ee0-148">authenticationType</span></span> |<span data-ttu-id="51ee0-149">Tipo de autenticação usado o repositório de dados ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="51ee0-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="51ee0-150">Os valores possíveis são: Anonymous e Basic.</span><span class="sxs-lookup"><span data-stu-id="51ee0-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="51ee0-151">Sim</span><span class="sxs-lookup"><span data-stu-id="51ee0-151">Yes</span></span> |
| <span data-ttu-id="51ee0-152">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="51ee0-152">username</span></span> |<span data-ttu-id="51ee0-153">Especifique o nome de usuário se você estiver usando a autenticação Básica.</span><span class="sxs-lookup"><span data-stu-id="51ee0-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="51ee0-154">Não</span><span class="sxs-lookup"><span data-stu-id="51ee0-154">No</span></span> |
| <span data-ttu-id="51ee0-155">Senha</span><span class="sxs-lookup"><span data-stu-id="51ee0-155">password</span></span> |<span data-ttu-id="51ee0-156">Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ee0-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="51ee0-157">Não</span><span class="sxs-lookup"><span data-stu-id="51ee0-157">No</span></span> |
| <span data-ttu-id="51ee0-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="51ee0-158">gatewayName</span></span> |<span data-ttu-id="51ee0-159">Nome do gateway Olá Olá serviço da fábrica de dados deve usar armazenamento de dados ODBC tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="51ee0-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="51ee0-160">Sim</span><span class="sxs-lookup"><span data-stu-id="51ee0-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="51ee0-161">Usando a autenticação Básica</span><span class="sxs-lookup"><span data-stu-id="51ee0-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="51ee0-162">Usando a autenticação Básica com credenciais criptografadas</span><span class="sxs-lookup"><span data-stu-id="51ee0-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="51ee0-163">Você pode criptografar credenciais Olá Olá [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (1.0 versão do Azure PowerShell) ou [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 versão ou anterior do hello PowerShell do Azure).</span><span class="sxs-lookup"><span data-stu-id="51ee0-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="51ee0-164">Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="51ee0-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="51ee0-165">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="51ee0-165">Dataset properties</span></span>
<span data-ttu-id="51ee0-166">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="51ee0-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="51ee0-167">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="51ee0-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="51ee0-168">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ee0-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="51ee0-169">Olá typeProperties seção de conjunto de dados do tipo **RelationalTable** (que inclui o conjunto de dados do ODBC) tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="51ee0-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="51ee0-170">Propriedade</span><span class="sxs-lookup"><span data-stu-id="51ee0-170">Property</span></span> | <span data-ttu-id="51ee0-171">Descrição</span><span class="sxs-lookup"><span data-stu-id="51ee0-171">Description</span></span> | <span data-ttu-id="51ee0-172">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="51ee0-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51ee0-173">tableName</span><span class="sxs-lookup"><span data-stu-id="51ee0-173">tableName</span></span> |<span data-ttu-id="51ee0-174">Nome da tabela de saudação no repositório de dados ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="51ee0-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="51ee0-175">Sim</span><span class="sxs-lookup"><span data-stu-id="51ee0-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="51ee0-176">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="51ee0-176">Copy activity properties</span></span>
<span data-ttu-id="51ee0-177">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="51ee0-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="51ee0-178">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="51ee0-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="51ee0-179">As propriedades disponíveis no hello **typeProperties** seção de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="51ee0-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="51ee0-180">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="51ee0-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="51ee0-181">Atividade de cópia, quando a fonte é do tipo **RelationalSource** (que inclui ODBC), Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="51ee0-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="51ee0-182">Propriedade</span><span class="sxs-lookup"><span data-stu-id="51ee0-182">Property</span></span> | <span data-ttu-id="51ee0-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="51ee0-183">Description</span></span> | <span data-ttu-id="51ee0-184">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="51ee0-184">Allowed values</span></span> | <span data-ttu-id="51ee0-185">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="51ee0-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="51ee0-186">query</span><span class="sxs-lookup"><span data-stu-id="51ee0-186">query</span></span> |<span data-ttu-id="51ee0-187">Use dados de tooread Olá consulta personalizada.</span><span class="sxs-lookup"><span data-stu-id="51ee0-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="51ee0-188">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="51ee0-188">SQL query string.</span></span> <span data-ttu-id="51ee0-189">Por exemplo: select * from MyTable.</span><span class="sxs-lookup"><span data-stu-id="51ee0-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="51ee0-190">Sim</span><span class="sxs-lookup"><span data-stu-id="51ee0-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="51ee0-191">Exemplo JSON: tooAzure Blob do repositório de dados de cópia de dados ODBC</span><span class="sxs-lookup"><span data-stu-id="51ee0-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="51ee0-192">Este exemplo fornece definições de JSON que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="51ee0-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="51ee0-193">Ele mostra como tooan armazenamento de BLOBs do Azure da fonte de dados de toocopy do ODBC.</span><span class="sxs-lookup"><span data-stu-id="51ee0-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="51ee0-194">No entanto, os dados podem ser tooany copiado de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="51ee0-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="51ee0-195">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="51ee0-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="51ee0-196">Um serviço vinculado do tipo [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="51ee0-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="51ee0-197">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="51ee0-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="51ee0-198">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="51ee0-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="51ee0-199">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="51ee0-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="51ee0-200">Um [pipeline](data-factory-create-pipelines.md) com Atividade de Cópia que usa [RelationalSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="51ee0-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="51ee0-201">exemplo Hello copia dados de um resultado de consulta em um repositório de dados ODBC tooa blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="51ee0-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="51ee0-202">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ee0-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="51ee0-203">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="51ee0-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="51ee0-204">Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="51ee0-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="51ee0-205">**Serviço vinculado do ODBC** Este exemplo usa Olá autenticação básica.</span><span class="sxs-lookup"><span data-stu-id="51ee0-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="51ee0-206">Veja a seção [Serviço vinculado a ODBC](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="51ee0-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="51ee0-207">**Serviço vinculado de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="51ee0-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="51ee0-208">**Conjunto de dados de entrada do ODBC**</span><span class="sxs-lookup"><span data-stu-id="51ee0-208">**ODBC input dataset**</span></span>

<span data-ttu-id="51ee0-209">exemplo Hello supõe que você criou uma tabela "MyTable" em um banco de dados ODBC e contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="51ee0-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="51ee0-210">Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="51ee0-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

<span data-ttu-id="51ee0-211">**Conjunto de dados de saída de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="51ee0-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="51ee0-212">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="51ee0-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="51ee0-213">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="51ee0-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="51ee0-214">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="51ee0-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="51ee0-215">**Atividade de cópia em um pipeline com origem ODBC (RelationalSource) e coletor Blob (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="51ee0-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="51ee0-216">pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="51ee0-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="51ee0-217">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**RelationalSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="51ee0-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="51ee0-218">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="51ee0-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
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
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="51ee0-219">Mapeamento de tipos para ODBC</span><span class="sxs-lookup"><span data-stu-id="51ee0-219">Type mapping for ODBC</span></span>
<span data-ttu-id="51ee0-220">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="51ee0-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="51ee0-221">Converter nativo tipos too.NET do tipo de origem</span><span class="sxs-lookup"><span data-stu-id="51ee0-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="51ee0-222">Converter do tipo de coletor de toonative de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="51ee0-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="51ee0-223">Ao mover dados de armazenamentos de dados ODBC, tipos de dados ODBC são tipos de too.NET mapeadas conforme mencionado em Olá [mapeamentos de tipo de dados ODBC](https://msdn.microsoft.com/library/cc668763.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="51ee0-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="51ee0-224">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="51ee0-224">Map source toosink columns</span></span>
<span data-ttu-id="51ee0-225">toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="51ee0-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="51ee0-226">Leitura repetida de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="51ee0-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="51ee0-227">Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="51ee0-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="51ee0-228">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="51ee0-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="51ee0-229">Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="51ee0-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="51ee0-230">Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada.</span><span class="sxs-lookup"><span data-stu-id="51ee0-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="51ee0-231">Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="51ee0-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="51ee0-232">Repositório GE Historian</span><span class="sxs-lookup"><span data-stu-id="51ee0-232">GE Historian store</span></span>
<span data-ttu-id="51ee0-233">Criar um toolink de serviço vinculado de ODBC um [GE Proficy historiador (agora historiador GE)](http://www.geautomation.com/products/proficy-historian) tooan data factory do Azure do repositório de dados conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="51ee0-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="51ee0-234">Instalar o Gateway de gerenciamento de dados em uma máquina local e registrar gateway Olá Olá portal.</span><span class="sxs-lookup"><span data-stu-id="51ee0-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="51ee0-235">gateway Olá instalado no computador local usa o driver ODBC Olá para GE historiador tooconnect toohello repositório de dados historiador GE.</span><span class="sxs-lookup"><span data-stu-id="51ee0-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="51ee0-236">Portanto, instale o driver Olá se ele não estiver instalado no computador do gateway hello.</span><span class="sxs-lookup"><span data-stu-id="51ee0-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="51ee0-237">Veja a seção [Habilitando a conectividade](#enabling-connectivity) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="51ee0-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="51ee0-238">Antes de usar Olá GE historiador armazenar em uma solução de fábrica de dados, verifique se gateway Olá pode se conectar a toohello repositório de dados usando as instruções na próxima seção, Olá.</span><span class="sxs-lookup"><span data-stu-id="51ee0-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="51ee0-239">Artigo de saudação de leitura desde o início de saudação para uma visão geral detalhada do uso de dados ODBC armazena como repositórios de dados de origem em uma operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="51ee0-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="51ee0-240">Solucionar problemas de conectividade</span><span class="sxs-lookup"><span data-stu-id="51ee0-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="51ee0-241">tootroubleshoot problemas de conexão, use Olá **diagnóstico** guia de **Gerenciador de configuração de Gateway de gerenciamento de dados**.</span><span class="sxs-lookup"><span data-stu-id="51ee0-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="51ee0-242">Iniciar o **Gerenciador de Configuração de Gateway de Gerenciamento de Dados**.</span><span class="sxs-lookup"><span data-stu-id="51ee0-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="51ee0-243">Você pode executar "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" diretamente (ou) pesquisa para **Gateway** toofind um link muito**Microsoft Data Management Gateway** aplicativo conforme Olá a imagem a seguir.</span><span class="sxs-lookup"><span data-stu-id="51ee0-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![Gateway de pesquisa](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="51ee0-245">Alternar toohello **diagnóstico** guia.</span><span class="sxs-lookup"><span data-stu-id="51ee0-245">Switch toohello **Diagnostics** tab.</span></span>

    ![Diagnóstico de gateway](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="51ee0-247">Selecione Olá **tipo** de dados armazenar (serviço vinculado).</span><span class="sxs-lookup"><span data-stu-id="51ee0-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="51ee0-248">Especifique **autenticação** e digite **credenciais** (ou) Insira **cadeia de caracteres de conexão** que é o repositório de dados de toohello tooconnect usado.</span><span class="sxs-lookup"><span data-stu-id="51ee0-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="51ee0-249">Clique em **Testar conexão** tootest Olá conexão toohello dados repositório.</span><span class="sxs-lookup"><span data-stu-id="51ee0-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="51ee0-250">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="51ee0-250">Performance and Tuning</span></span>
<span data-ttu-id="51ee0-251">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="51ee0-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
